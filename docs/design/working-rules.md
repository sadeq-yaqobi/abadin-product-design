# Abadin — working rules (set by the owner)

## Where design work happens

- Every request to design something or change a design in this project is implemented in the Abadin Figma file in Sadeq's team:
  https://www.figma.com/design/Qwx3QpLbhwbouq12QLvAL5
- Design work is not done in a Claude artifact or Claude Design unless the owner explicitly asks for Claude's own artifact.
- For Figma work, the `abadin-figma-design` skill applies.
- If Figma is unavailable (for example, the plan's MCP call limit is reached), stop and report the blocker. Do not fall back to an artifact without asking.

## Design widths (responsive delivery policy)

| Width | Role |
|---|---|
| `1440` | Full-page Desktop design |
| `375` | Full-page Mobile design |
| `1280` | Targeted narrower-desktop validation |
| `360` | Targeted mobile validation |
| `320` | Targeted narrow-mobile stress validation |

- No full-page design is made at `1280`, `360` or `320` by default.
- These widths are for targeted validation. Build a section, state or problem frame only when it is needed to show a real layout or interaction difference, or a failure.
- Document intermediate responsive behaviour between the primary widths where it matters.
- An untested width or state is never reported as `PASS` or validated.
- This policy matches the «Responsive design and delivery» section of [`skills/abadin-figma-design/SKILL.md`](../../skills/abadin-figma-design/SKILL.md).

## Tasks and review

- Tasks come directly from the owner.
- There is no ChatGPT task definition or ChatGPT/CLS review step.
- Do not request external review before or after a task.
