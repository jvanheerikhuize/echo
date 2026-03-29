# E.C.H.O. — Experiential Collaborative Hub Orchestrator

An immersive multiplayer narrative experience for 2-6 players, powered by any advanced LLM. Built around mystery, roles, and decisions.

Players are assigned roles — Observer, Listener, Keeper, or Anchor — each perceiving a different slice of the same reality. A mystery unfolds through their choices. No one has the full picture alone. The answer only assembles when all perspectives combine.

## How It Works

E.C.H.O. uses a **single-LLM architecture**. One person acts as Game Master (GM) and runs the prompt. Players don't need AI — they read DMs from the GM, make decisions, and respond. The GM relays their choices to the LLM, which generates the next chapter with consequences.

```
                 ┌──────────────────────┐
                 │   GM's LLM Session   │
                 │   loads: prompt.md    │
                 │   sees: everything    │
                 └──────────┬───────────┘
                            │
           ┌────────────────┼────────────────┐
           │ DM             │ DM             │ DM
           ▼                ▼                ▼
   ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
   │  Observer     │ │  Listener    │ │  Keeper      │
   │  sees layout  │ │  hears clues │ │  finds objects│
   │  decides where│ │  decides who │ │  decides what │
   └──────────────┘ └──────────────┘ └──────────────┘
```

## Quick Start

1. Copy the prompt from the code block in [`prompt.md`](prompt.md).
2. Paste it into a fresh LLM session (Claude, ChatGPT, Gemini). This is the **GM session**.
3. Configure: `/players 3 Alex, Sam, Jordan` and optionally `/theme` and `/turns`.
4. Type `START`. E.C.H.O. generates a titled world with a mystery.
5. DM the intake questions to each player. They respond with their answers.
6. Register each player: `PROFILE PLAYER_1: English, she/her, 28, I notice the exits, sight, ...`
7. E.C.H.O. assigns a role. Generate welcome: `WELCOME PLAYER_1`. Send via DM.
8. Players read their chapter, face a decision, and respond with their choice.
9. Relay each response: `ACTION PLAYER_1: I took the notebook`.
10. When ALL players have responded, E.C.H.O. generates the next chapter for everyone.
11. Send each player their personal chapter via DM. Repeat from step 8.
12. At the convergence point, type `/finale` for the shared ending.

## Core Mechanics

### Roles

Each player is assigned a role based on their intake answers. Roles determine what you perceive and what decisions you face:

| Role | Perceives | Decides on |
|------|-----------|------------|
| **Observer** | Visual details, spatial layout, patterns, light | Where to go, what to examine |
| **Listener** | Sounds, voices, rhythms, silences, recordings | Who to trust, what signals mean |
| **Keeper** | Objects, textures, mechanisms, traces, tools | What to take, use, or leave behind |
| **Anchor** | Atmosphere, temperature, instinct, timing | When to act, wait, or warn |

### Decisions, Not Feelings

Each chapter ends with a concrete, role-appropriate choice. Your decisions have consequences that shape the next chapter. The Observer chooses which corridor to investigate. The Listener decides whether to trust the recording. The Keeper picks which object to take. Every choice matters.

### Signal Register & Crossweave

After each decision, E.C.H.O. extracts signals — sensory details and decision outcomes — and stores them in a **signal register** per player. These signals progressively bleed into other players' realities:

- **Early (HINT):** "Someone else has been here. The dust is disturbed."
- **Middle (BLEED):** Unexplained clues from other players' decisions appear in your scene.
- **Late (MERGE):** Other players' choices directly affect your reality.
- **Finale (REVEAL):** All signals converge. The mystery resolves. Names appear for the first time.

### Mystery Plot

Every session is built around a central mystery with real stakes. The plot follows a narrative arc — discovery, complication, revelation, resolution — not an emotional mood trajectory. Each session gets a unique title tied to its specific story.

### Multilingual

All internal systems are English. Player-facing narrative renders in each player's chosen language. Different players in the same session can play in different languages.

## GM Commands

| Command | Description |
|---------|-------------|
| `/players [2-6] [names]` | Register players |
| `/theme [text]` | Set a theme (optional — auto-generated if omitted) |
| `/turns [N]` | Set max turns per player (optional) |
| `START` | Generate the world and title |
| `PROFILE [ID]: [answers]` | Register a player's profile and assign role |
| `WELCOME [ID]` | Generate a player's welcome message |
| `ACTION [ID]: [text]` | Relay a player's decision |
| `/status` | View session status, player insights, timing |
| `/state` | Dump full raw state as JSON |
| `/state [ID]` | Dump a single player's state |
| `/pulse` | In-story progress update for the group |
| `/rest` | Day-closing story beat for the group |
| `/hint [ID]` | Send a nudge to a stuck player |
| `/save` | Export complete state for session transfer |
| `/load` | Import a saved state into a new session |
| `/finale` | Trigger the shared ending |
| `/end` | End session with summary |

## Player Experience

Players don't need commands or AI. They:
1. Answer intake questions (language, pronouns, perception style, instinct, etc.)
2. Receive a role assignment and personalized welcome
3. Read each chapter — a scene filtered through their role
4. Make a decision at the end of each chapter
5. Respond with their choice (a sentence, a word, whatever feels right)

Every decision shapes what happens next. There are consequences.

## Guides

- [`gm-guide.md`](gm-guide.md) — Detailed guide for Game Masters
- [`player-guide.md`](player-guide.md) — Quick guide for players

## Credits

Based on E.C.H.O. v1.0 by Jerry van Heerikhuize.
