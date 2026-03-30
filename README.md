# E.C.H.O.

**Experiential Collaborative Hub Orchestrator**

An immersive multiplayer narrative experience for 2-6 players, powered by any advanced LLM.

---

Players are assigned roles — **Observer**, **Listener**, **Keeper**, or **Anchor** — each perceiving a different slice of the same reality. A mystery unfolds through their choices. No one has the full picture alone. The answer only assembles when all perspectives combine.

```
                    ┌──────────────────────┐
                    │   GM's LLM Session   │
                    │   loads: gm-prompt.md │
                    │   sees: everything    │
                    └──────────┬───────────┘
                               │
          ┌────────────┬───────┴───────┬────────────┐
          │ DM         │ DM           │ DM         │ DM
          ▼            ▼              ▼            ▼
   ┌────────────┐┌────────────┐┌────────────┐┌────────────┐
   │  Observer   ││  Listener  ││  Keeper    ││  Anchor    │
   │  sees layout││ hears clues││finds objects││senses mood │
   │decides where││ decides who││decides what││decides when│
   └────────────┘└────────────┘└────────────┘└────────────┘
```

One person runs the prompt as **Game Master**. Players don't need AI — they read DMs, make decisions, and respond. The GM relays their choices. The LLM generates the next chapter with consequences.

## Quick Start

1. Copy the prompt from the code block in [`gm-prompt.md`](gm-prompt.md)
2. Paste into a fresh LLM session (Claude, ChatGPT, Gemini)
3. `/players 3 Alex, Sam, Jordan` — register players
4. `START` — guided world creation: pick a setting, shape the mystery, set the pace
5. DM the intake questions to each player
6. `PROFILE PLAYER_1: [answers]` — register and assign roles
7. `WELCOME PLAYER_1` — send personalized welcome via DM
8. Players read, decide, respond. Relay with `ACTION PLAYER_1: [choice]`
9. All players responded → next chapter generates for everyone
10. `/finale` at convergence → the mystery resolves
11. `/end` → every player receives a personal game report via DM

## Roles

| Role | Perceives | Decides on |
|------|-----------|------------|
| **Observer** | Visual details, spatial layout, patterns, light, written text, marks | Where to go, what to examine, what to read |
| **Listener** | Sounds, voices, rhythms, silences, recordings | Who or what to trust, what signals mean, whether to respond |
| **Keeper** | Objects, textures, mechanisms, traces, tools | What to take, use, leave behind, or combine |
| **Anchor** | Atmosphere, temperature shifts, instinct, timing, wrongness | When to act, wait, or warn, what feels off |

Roles are assigned automatically based on intake answers. The GM can override.

## How Decisions Work

Each chapter ends with a concrete, role-appropriate choice. The Observer picks which corridor to investigate. The Listener decides whether to trust the recording. The Keeper chooses which object to take. Every choice has consequences that shape the next chapter.

After each decision, E.C.H.O. extracts **signals** — sensory details and decision outcomes — and stores them per player. These signals progressively bleed into other players' realities through **crossweave**:

| Phase | Chapters | Effect |
|-------|----------|--------|
| **HINT** | 1-2 | Other players referenced as distant presences |
| **BLEED** | 3-4 | Unexplained clues from others' decisions appear in your scene |
| **MERGE** | Convergence | Others' choices directly affect your reality |
| **REVEAL** | Finale | All signals converge — the mystery resolves, names appear |

## Features

- **Mystery-driven plot** with a narrative arc and real stakes
- **Unique session title** generated for each game
- **Multilingual** — each player chooses their language; internals are English
- **Image prompts** on every chapter, copy-pasteable into any image generator
- **Timestamps** on every action — narrative reflects real elapsed time
- **Persistent state** — `/save` and `/load` for zero-loss session transfer
- **Raw state access** — `/state` dumps the full engine state as JSON
- **Synchronized rounds** — all players advance together
- **Guided world creation** — pick from generated settings, shape the mystery, set the pace
- **Public recruitment** — generate a printable flyer with QR code to recruit strangers via WhatsApp/Signal/Discord
- **Post-game reports** — every player gets a personal debrief: their decisions, their impact, the full picture

## GM Commands

| Command | Description |
|---------|-------------|
| `/players [2-6] [names]` | Register players |
| `/theme [text]` | Set a theme (optional) |
| `/turns [N]` | Set max turns per player |
| `/recruit [link]` | Generate printable flyer with QR code to recruit players |
| `START` | Generate the world |
| `PROFILE [ID]: [answers]` | Register profile, assign role |
| `WELCOME [ID]` | Generate personalized welcome |
| `ACTION [ID]: [text]` | Relay a player's decision |
| `/status` | Session status and player insights |
| `/state` | Full raw state dump (JSON) |
| `/state [ID]` | Single player state dump |
| `/pulse` | In-story group progress update |
| `/rest` | Day-closing story beat |
| `/hint [ID]` | Nudge a stuck player |
| `/save` | Export state for session transfer |
| `/load` | Import saved state |
| `/finale` | Trigger the shared ending |
| `/end` | End session with summary |

## Documentation

| File | Description |
|------|-------------|
| [`gm-prompt.md`](gm-prompt.md) | The complete GM prompt — copy and paste into any LLM |
| [`gm-guide.md`](gm-guide.md) | Detailed guide for Game Masters |
| [`player-guide.md`](player-guide.md) | Quick reference for players |

## Requirements

- Any advanced LLM chat interface (Claude, ChatGPT, Gemini, etc.)
- A messaging platform for DMs (WhatsApp, Signal, Telegram, Discord, etc.)
- 2-6 players + 1 Game Master

## License

[MIT](LICENSE)

## Author

Jerry van Heerikhuize
