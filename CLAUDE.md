# E.C.H.O. — Experiential Collaborative Hub Orchestrator

## Project overview

A multiplayer immersive narrative experience powered by LLMs. Two meta prompts form a
hub-and-spoke system: one GM hub prompt orchestrates the world, and one player spoke
template is personalized per player. No application code — pure prompt engineering.

Based on the echo game type from E.C.H.O. v1.0, with key innovations:
dynamic echo mechanic, sensory memory, echo crossweave, and personal finale.

All narrative output is in **Dutch**. All documentation and prompt structure is in **English**.

## Files

- `prompt.md` — GM hub prompt (the Game Master loads this into their LLM session)
- `prompt-player.md` — Player spoke template (GM's LLM fills the `{{PLACEHOLDERS}}` and generates one per player)
- `README.md` — How to play and design rationale

## Conventions

- Prompt structure follows MVC pattern: Model (state/rules), View (output templates), Controller (flow logic)
- XML-style tags for prompt sections (`<CORE_DIRECTIVES>`, `<MODEL>`, `<VIEW>`, `<CONTROLLER>`)
- Behavior rules prefixed: `BHV:+` (must), `BHV:!` (prohibit), `BHV:~` (prefer)
- Output templates prefixed: `OUT:TYPE_NAME`
- Player-facing text: Dutch. Structural labels and documentation: English
- Dividers: ━ (U+2501), exactly 36 characters
