# User-Level Claude Instructions

## GenAI Workflow Logging

When working on any project that contains a `WORKFLOW_LOG.md` file:

- **Suggest logging** at natural decision points: after agreeing on an approach, completing a major implementation step, resolving a significant issue, or before a meaningful git commit. Say something like: "This feels like a good point to log — want to run `/log`?"
- **Do not log every turn.** Only meaningful stages where a decision was made or significant output was produced.
- **Log format** is defined at the top of `WORKFLOW_LOG.md` in each project. Follow it strictly.
- When the user runs `/log`, help them complete the next entry based on recent conversation context, pre-filling what you can and asking only what's unclear.
- **Default log location**: `G:/My Drive/Colab Notebooks/genai-workflow-meta/WORKFLOW_LOG.md` when no project-specific log exists. If a project has its own `WORKFLOW_LOG.md` in its root, use that instead.
- **Log is append-only**: never edit existing entries; only add new ones.
- **Field taxonomy to use when filling entries**:
  - Initiator: User / Assistant / Joint
  - User Engagement: High / Medium / Low
  - User Action Type: Problem framing / Constraint setting / Scope rejection / Target definition / Evaluation criteria / Planning & sequencing / Structuring / Approval only / Meta-analysis
  - Input Modality: File attachment / URL / Named reference / Search instruction / In-conversation text / In-conversation artifact
  - Decision Dependency: User-critical / User-influenced / Assistant-driven
