<!-- CONFIG
archive_cadence: monthly
tail_lines: 120
-->

Review the recent conversation and help the user complete the next workflow log entry.

## Step 1: Read config

Read the CONFIG block at the top of this file. Extract:
- `archive_cadence` — how often to archive (monthly / quarterly / annually)
- `tail_lines` — how many lines to read from the tail of the log file

## Step 2: Determine the target log file

Check the current working directory for a `WORKFLOW_LOG.md` file.

- **If found**: use it. This is a project-specific log.
- **If not found**: check if the working directory is the Colab Notebooks root or a cross-project context. If so, use the global log at `G:/My Drive/Colab Notebooks/genai-workflow-meta/WORKFLOW_LOG.md`.
- **If ambiguous** (e.g., a project sub-folder with no log yet): ask the user — "Should I create a project-specific `WORKFLOW_LOG.md` here, or log to the global one?"

## Step 3: Efficient log read

Do NOT read the entire log file. Instead:
1. Read the first 35 lines only — to get the format header and field taxonomy.
2. Read the last `tail_lines` lines only — to find the last Stage ID and get recent entry context (approximately the last 3 entries).

Use these two reads to determine the next Stage ID (increment from the last entry) and understand recent context.

## Step 4: Check archive condition

Check the date of the most recent entry in the tail.

- If `archive_cadence` is `monthly`: check if any entries in the tail are from a prior calendar month relative to today.
- If `archive_cadence` is `quarterly`: check if any entries are from a prior calendar quarter.
- If `archive_cadence` is `annually`: check if any entries are from a prior calendar year.

If the archive condition is met, notify the user before proceeding:

> "Entries from [prior period] are present. Per your `monthly` archive cadence, I can move them to `WORKFLOW_LOG_YYYY_MM.md` and keep the current file lean. Do this now, or skip?"

If the user says yes:
- Create `WORKFLOW_LOG_YYYY_MM.md` (or appropriate filename) in the same folder, containing the format header + all entries from that period.
- Remove those entries from `WORKFLOW_LOG.md`, keeping the format header intact.
- Remind the user to commit both files.

If the user says skip, proceed without archiving.

## Step 5: Pre-fill the entry draft

Review the recent conversation and draft the next entry using bullet point format. Use the following taxonomy strictly:

- **Phase**: Planning / Implementation / Debugging / Review / Other
- **Initiator**: User / Assistant / Joint
- **User Engagement**: High / Medium / Low
- **User Action Type**: Problem framing / Constraint setting / Scope rejection / Target definition / Evaluation criteria / Planning & sequencing / Structuring / Approval only / Meta-analysis
- **Input Modality**: File attachment / URL / Named reference / Search instruction / In-conversation text / In-conversation artifact
- **Decision Dependency**: User-critical / User-influenced / Assistant-driven
- **Reason for deviation**: Disagreement / Missing context / Ambiguity / Quality / Other (only if Decision Dependency is User-critical or User-influenced)

Format each entry as:

```
### S0N — Stage Name — YYYY-MM-DD

- **Phase**: ...
- **Initiator**: ...
- **User Engagement**: ...
- **User Action Type**: ...
- **Input Modality**: ...
- **Prompt summary**: ...
- **AI output summary**: ...
- **Decision Dependency**: ...
- **Reason for deviation**: ...
- **Outcome**: ...
- **Notes**: ...
```

Pre-fill every field you can confidently infer. For fields requiring user judgment — especially **User Action Type**, **Decision Dependency**, and **Reason for deviation** — provide your best guess and flag it clearly for the user to confirm or correct.

## Step 6: Show the draft and get confirmation

Present the full draft entry to the user. Ask them to:
- Confirm it as-is, or
- Correct any fields before it is written

Do not write anything until the user explicitly approves.

## Step 7: Append and remind

Once approved, append the entry to the log file. Then remind the user to commit the log along with any related project changes.

## Rules

- Append-only: never edit existing entries
- No speculation about intent: describe what happened factually
- Decision Dependency cannot be left blank
- Never read more of the log file than specified in CONFIG
