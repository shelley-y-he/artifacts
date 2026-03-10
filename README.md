# artifacts

Shareable system file backups for GenAI workflow tooling.

## Purpose

Stores copies of configuration files, scripts, and skill definitions so they can be versioned, shared, and reproduced across machines or team members.

## Structure

Each subfolder corresponds to a project or system:

| Folder | Contents |
|---|---|
| `genai-workflow-meta/` | Workflow logging system: Claude rule (`CLAUDE.md`), `/log` skill, PostToolUse hook script, and Claude Code settings |

## Usage

To replicate the workflow logging setup on a new machine, copy the files from `genai-workflow-meta/` to their respective locations:

| File | Destination |
|---|---|
| `CLAUDE.md` | `~/.claude/CLAUDE.md` |
| `log_skill.md` | `~/.claude/commands/log.md` |
| `tool_audit.py` | `~/.claude/hooks/tool_audit.py` |
| `settings.json` | `~/.claude/settings.json` |
