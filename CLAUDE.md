# E.C.H.O. — Experiential Collaborative Hub Orchestrator

## Project overview

A multiplayer immersive narrative experience powered by a single LLM. One GM prompt
drives the entire experience — players don't need AI. They read DMs from the GM and
respond naturally. The GM relays their responses to the LLM, which generates the next
chapter. No application code — pure prompt engineering.

Based on the echo game type from E.C.H.O. v1.0, with key innovations:
dynamic echo mechanic, sensory memory, echo crossweave, and personal finale.

All narrative output is in **Dutch**. All documentation and prompt structure is in **English**.

## Files

- `prompt.md` — The master prompt (the Game Master loads this into their LLM session)
- `spelers-uitleg.md` — Dutch player guide (posted in the group before the game starts)
- `gamemaster-uitleg.md` — Dutch GM guide (step-by-step instructions for the Game Master)
- `README.md` — How to play and design rationale

## Conventions

- Prompt structure follows MVC pattern: Model (state/rules), View (output templates), Controller (flow logic)
- XML-style tags for prompt sections (`<CORE_DIRECTIVES>`, `<MODEL>`, `<VIEW>`, `<CONTROLLER>`)
- Behavior rules prefixed: `BHV:+` (must), `BHV:!` (prohibit), `BHV:~` (prefer)
- Output templates prefixed: `OUT:TYPE_NAME`
- Player-facing text: Dutch. Structural labels and documentation: English
- Dividers: ━ (U+2501), exactly 36 characters
