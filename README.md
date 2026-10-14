# Pairing Gears

An [Agent Skill](https://agentskills.io) that guides you through coding tasks one step at a time. You choose how much help you get, from Socratic hints to a full implementation, so you keep the reasoning you want to do yourself.

Works with Claude Code, Cursor, GitHub Copilot, Codex and any other agent that reads `SKILL.md` skills.

## Install

```bash
npx skills add gianfrancodemarco/pairing-gears -g
```

This installs the skill for your user account, not one project, and asks which agents to set it up for. It needs Node.js.

In Claude Code you can also install it as a plugin:

```
/plugin install pairing-gears --marketplace gianfrancodemarco/pairing-gears
```

Start a new agent session afterwards so it picks up the skill. For a manual install, see [Manual install](#manual-install).

## Levels

| Level | Mode | What the agent does |
| --- | --- | --- |
| 1 | Socratic coach | Asks one question or gives one conceptual hint. No code, commands or file locations. |
| 2 | Navigator (default) | Points to the relevant file or decision and gives the next step. No code. |
| 3 | Mentor | Explains the approach, edge cases and APIs, with pseudocode or partial examples. |
| 4 | Pair programmer | Gives exact snippets, commands and tests for you to apply. |
| 5 | Implementation agent | Makes the change, verifies it and reports back. |

At levels 1 to 4 the agent gives one step, waits for you to try it, checks your result, and only then moves on. If you're stuck, it offers to raise the level instead of quietly doing more. You can always ask for one thing directly, such as "show me the code", without changing the level.

## Example

The same bug, "the cart total is wrong when a discount code is applied", at three levels:

> **Level 1:** What should happen to the total if two discounts apply to the same item? Find where the code decides that.

> **Level 2:** Look at `applyDiscounts` in `cart/pricing.ts`. Percentage discounts are applied after fixed ones, so their order changes the result. Write a test with one of each and check that it fails.

> **Level 4:** Add this test to `cart/pricing.test.ts`:
> ```ts
> it("applies percentage before fixed discounts", () => {
>   expect(total([item(100)], [pct(10), fixed(5)])).toBe(85);
> });
> ```
> Then sort the discounts by type at the top of `applyDiscounts`.

To use it, say things like:

- "Guide me through this at level 1."
- "Use Pairing Gears level 2; I want to write the code."
- "Increase to level 4 for this failing test."
- "Do this part for me, then go back to level 2."

## Manual install

Copy or link the `skills/pairing-gears/` folder into your agent's user-level skills directory:

| Agent | Directory |
| --- | --- |
| Claude Code | `~/.claude/skills/` |
| Cursor | `~/.cursor/skills/` or `~/.agents/skills/` |
| GitHub Copilot (VS Code) | `~/.copilot/skills/` or `~/.agents/skills/` |
| Codex | `~/.agents/skills/` |

macOS / Linux:

```bash
git clone https://github.com/gianfrancodemarco/pairing-gears.git ~/pairing-gears
mkdir -p ~/.agents/skills ~/.claude/skills
ln -s ~/pairing-gears/skills/pairing-gears ~/.agents/skills/pairing-gears
ln -s ~/pairing-gears/skills/pairing-gears ~/.claude/skills/pairing-gears
```

Windows (PowerShell). This copies the folder, because symlinks need admin rights or Developer Mode:

```powershell
git clone https://github.com/gianfrancodemarco/pairing-gears.git "$HOME\pairing-gears"
foreach ($d in "$HOME\.agents\skills", "$HOME\.claude\skills") {
  New-Item -ItemType Directory -Force $d | Out-Null
  Copy-Item -Recurse "$HOME\pairing-gears\skills\pairing-gears" $d
}
```

## License

[MIT](LICENSE)
