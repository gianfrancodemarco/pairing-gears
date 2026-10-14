# Pairing Gears

An [Agent Skill](https://agentskills.io) that guides you through software-development tasks one step at a time. You pick how much help you get, from 1 (Socratic hints) to 5 (the agent implements it), so you keep the reasoning you want to do yourself.

| Level | Mode | What the agent does |
| --- | --- | --- |
| 1 | Socratic coach | One question or conceptual hint. No code, commands or file locations. |
| 2 | Navigator (default) | Points to the relevant file or decision and the next step. No code. |
| 3 | Mentor | Explains the approach, edge cases and APIs. Pseudocode or partial examples. |
| 4 | Pair programmer | Exact snippets, commands and tests for you to apply. |
| 5 | Implementation agent | Makes the change, verifies it and reports back. |

## Usage

- "Guide me through this at level 1."
- "Use Pairing Gears level 2; I want to write the code."
- "Increase to level 4 for this failing test."
- "Do this part for me, then go back to level 2."

## Install

The skill is the folder `skills/pairing-gears/`. Put it in your agent's user-level skills directory:

| Agent | Directory |
| --- | --- |
| Claude Code | `~/.claude/skills/` |
| Cursor | `~/.cursor/skills/` or `~/.agents/skills/` |
| VS Code (GitHub Copilot) | `~/.copilot/skills/` or `~/.agents/skills/` |
| Codex | `~/.agents/skills/` |

macOS / Linux:

```bash
git clone https://github.com/gianfrancodemarco/pairing-gears.git ~/pairing-gears
mkdir -p ~/.agents/skills ~/.claude/skills
ln -s ~/pairing-gears/skills/pairing-gears ~/.agents/skills/pairing-gears
ln -s ~/pairing-gears/skills/pairing-gears ~/.claude/skills/pairing-gears
```

Windows (PowerShell; copies instead of symlinking, which needs admin or Developer Mode):

```powershell
git clone https://github.com/gianfrancodemarco/pairing-gears.git "$HOME\pairing-gears"
foreach ($d in "$HOME\.agents\skills", "$HOME\.claude\skills") {
  New-Item -ItemType Directory -Force $d | Out-Null
  Copy-Item -Recurse "$HOME\pairing-gears\skills\pairing-gears" $d
}
```

Start a new agent session afterwards so it picks up the skill.
