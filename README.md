<div align="center">

# E.C.H.O.

### Experiential Collaborative Hub Orchestrator

An immersive multiplayer narrative experience for 2-6 players, powered by any advanced LLM.

[![License: MIT](https://img.shields.io/badge/License-MIT-black.svg)](LICENSE)
[![Players](https://img.shields.io/badge/Players-2--6-blue.svg)](#)
[![AI Required](https://img.shields.io/badge/AI-Any%20LLM-purple.svg)](#)
[![Languages](https://img.shields.io/badge/Languages-Any-green.svg)](#)

---

*Players are assigned roles — each perceiving a different slice of the same reality.*
*A mystery unfolds through their choices. No one has the full picture.*
*The answer only assembles when all perspectives combine.*

</div>

<br>

```
                  ┌────────────────────────┐
                  │    GM's LLM Session    │
                  │   loads: gm-prompt.md  │
                  │    sees: everything    │
                  └───────────┬────────────┘
                              │
         ┌──────────┬─────────┴────────┬──────────┐
         │ DM       │ DM               │ DM       │ DM
         ▼          ▼                  ▼          ▼
  ┌────────────┐┌────────────┐┌────────────┐┌────────────┐
  │  Observer   ││  Listener  ││   Keeper   ││   Anchor   │
  │ sees layout ││ hears clues││finds objects││ senses mood│
  │decides where││ decides who││decides what││decides when│
  └────────────┘└────────────┘└────────────┘└────────────┘
```

One person runs the prompt as **Game Master**. Players don't need AI — they read DMs, make decisions, and respond. The GM relays their choices. The LLM generates the next chapter with consequences.

<br>

## Quick Start

> **Requirements:** Any advanced LLM chat (Claude, ChatGPT, Gemini) + a messaging platform (WhatsApp, Signal, Telegram, Discord) + 2-6 players

```
1.  Copy the prompt from the code block in gm-prompt.md
2.  Paste into a fresh LLM session
3.  /players 3 Priya, Sam, Lucia
4.  START → guided world creation
5.  DM intake questions to each player
6.  PROFILE PLAYER_1: [answers] → roles assigned
7.  WELCOME PLAYER_1 → send personalized welcome
8.  Players decide → relay with ACTION PLAYER_1: [choice]
9.  All responded → next chapter generates
10. /finale → the mystery resolves
11. /end → personal game reports for everyone
```

<br>

## Roles

Each role perceives a **different slice** of the same reality. The mystery can only be solved by combining all perspectives.

| | Role | Perceives | Decides on |
|---|------|-----------|------------|
| **👁** | **Observer** | Visual details, spatial layout, patterns, light, written text, marks | Where to go, what to examine, what to read |
| **👂** | **Listener** | Sounds, voices, rhythms, silences, recordings | Who or what to trust, what signals mean, whether to respond |
| **🤲** | **Keeper** | Objects, textures, mechanisms, traces, tools | What to take, use, leave behind, or combine |
| **🌡** | **Anchor** | Atmosphere, temperature shifts, instinct, timing, wrongness | When to act, wait, or warn, what feels off |

> Roles are assigned automatically based on intake answers. The GM can override.

<br>

## How Decisions Work

Each chapter ends with a concrete, role-appropriate choice. The Observer picks which corridor to investigate. The Listener decides whether to trust the recording. The Keeper chooses which object to take. Every choice has consequences that shape the next chapter.

After each decision, E.C.H.O. extracts **signals** — sensory details and decision outcomes — and stores them per player. These signals progressively bleed into other players' realities through **crossweave**:

```
  Chapter 1-2        Chapter 3-4        Convergence          Finale
 ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
 │    HINT     │    │    BLEED    │    │    MERGE    │    │   REVEAL    │
 │             │    │             │    │             │    │             │
 │   Distant   │───►│ Unexplained │───►│   Others'   │───►│     All     │
 │  presences  │    │    clues    │    │  decisions  │    │   signals   │
 │  referenced │    │   appear    │    │ affect your │    │  converge   │
 │             │    │             │    │   reality   │    │             │
 └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
```

<br>

## Features

<table>
<tr>
<td width="50%">

**Narrative Engine**
- Mystery-driven plot with real stakes
- Unique session title per game
- Guided world creation
- Image prompts on every chapter
- Post-game reports for every player

</td>
<td width="50%">

**Technical**
- Multilingual — each player picks their language
- Timestamps on every action
- Persistent state via `/save` and `/load`
- Raw state access via `/state`
- Synchronized rounds

</td>
</tr>
<tr>
<td width="50%">

**Social**
- Public recruitment via QR code flyers
- Any messaging platform
- 2-6 players, any language mix

</td>
<td width="50%">

**Pacing**
- Rounds take minutes, hours, or days
- `/pulse` for in-story group updates
- `/rest` for day-closing story beats
- No real-time pressure

</td>
</tr>
</table>

<br>

## GM Commands

<details>
<summary><b>Setup</b></summary>

| Command | Description |
|---------|-------------|
| `/players [2-6] [names]` | Register players |
| `/theme [text]` | Set a theme (optional) |
| `/turns [N]` | Set max turns per player |
| `/recruit [link]` | Generate printable flyer with QR code to recruit players |
| `START` | Begin guided world creation |

</details>

<details>
<summary><b>Gameplay</b></summary>

| Command | Description |
|---------|-------------|
| `PROFILE [ID]: [answers]` | Register profile, assign role |
| `WELCOME [ID]` | Generate personalized welcome |
| `ACTION [ID]: [text]` | Relay a player's decision |
| `/hint [ID]` | Nudge a stuck player |
| `/pulse` | In-story group progress update |
| `/rest` | Day-closing story beat |

</details>

<details>
<summary><b>Session Management</b></summary>

| Command | Description |
|---------|-------------|
| `/status` | Session status and player insights |
| `/state` | Full raw state dump (JSON) |
| `/state [ID]` | Single player state dump |
| `/save` | Export state for session transfer |
| `/load` | Import saved state |
| `/finale` | Trigger the shared ending |
| `/end` | End session with personal reports |

</details>

<br>

## Documentation

| | File | Description |
|---|------|-------------|
| **Prompt** | [`gm-prompt.md`](gm-prompt.md) | The complete game engine — copy and paste into any LLM |
| **GM Guide** | [`gm-guide.md`](gm-guide.md) | Everything you need to run a session |
| **Player Guide** | [`player-guide.md`](player-guide.md) | Quick reference to share with players |
| **Contributing** | [`CONTRIBUTING.md`](CONTRIBUTING.md) | How to contribute to the project |

<br>

---

<div align="center">

**[MIT License](LICENSE)** — Created by Jerry van Heerikhuize

</div>
