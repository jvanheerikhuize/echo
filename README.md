# E.C.H.O. — Experiential Collaborative Hub Orchestrator

A shared, immersive sensory narrative experience for 2-6 players, powered by any advanced LLM.

Players are guided through an immersive story that engages all five senses, narrated with the dry wit of a classic Infocom text adventure. Everyone plays alone — but the story weaves them together, and they arrive at the same ending: **samen, alleen** (together, alone).

## How It Works

E.C.H.O. uses a **single-LLM architecture**. One person acts as Game Master (GM) and runs the prompt. Players don't need AI — they just read DMs from the GM and respond naturally with what they felt. The GM relays their responses to the LLM, which generates the next chapter.

```
                 ┌──────────────────────┐
                 │   GM's LLM Session   │
                 │   loads: prompt.md   │
                 │   sees: everything   │
                 └──────────┬───────────┘
                            │
           ┌────────────────┼────────────────┐
           │ DM             │ DM             │ DM
           ▼                ▼                ▼
   ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
   │  Player 1    │ │  Player 2    │ │  Player N    │
   │  reads DMs   │ │  reads DMs   │ │  reads DMs   │
   │  responds    │ │  responds    │ │  responds    │
   └──────────────┘ └──────────────┘ └──────────────┘
```

## Quick Start

1. Copy the prompt from the code block in [`prompt.md`](prompt.md).
2. Paste it into a fresh LLM session (Claude, ChatGPT, Gemini). This is the **GM session**.
3. Configure: `/spelers 3 Alice, Bob, Charlie` and optionally `/thema`, `/beurten`, and `/beeld`.
4. Type `START`. E.C.H.O. generates the world and an intro message for players.
5. DM the intro message to each player. They respond with their name, pronouns, and age.
6. Register each player: `PROFIEL SPELER_1: Alice, zij, 28`.
7. Generate welcome messages: `WELKOM SPELER_1`, `WELKOM SPELER_2`, etc. Send via DM.
8. Players read the welcome and respond with `verder` or what they felt.
9. You relay each response with `ACTIE SPELER_1: [what they said]`.
10. When ALL players have responded, E.C.H.O. generates the next chapter for everyone at once.
11. Send each player their personal chapter via DM. Repeat from step 8.
12. When the convergence point is reached, type `/finale` for the shared ending.

## What Makes This Special

### The Echo Mechanic

After each chapter, the player is invited to share what they felt, saw, or imagined. This response — their **echo** — gets relayed by the GM to the LLM. The GM extracts sensory and emotional keywords and stores them in an **echo register** per player.

The next chapter is generated dynamically, incorporating the player's echoes. If someone mentioned "warmth", the next chapter breathes warmth. If someone felt "loneliness", the story gently acknowledges it. Every playthrough is unique because the story listens.

### Echo Crossweave

Echoes don't stay isolated. When generating togetherness moments (the subtle signals that other players share the journey), the GM uses echoes from *other* players — without attribution. If Player A echoed "rain", Player B might encounter: *"Ergens ruikt iemand anders dezelfde regen."*

This creates genuine sensory bridges between players who never directly communicate.

### Personal Finale

The shared ending weaves each player's accumulated echoes into a single closing scene. The player who felt warmth finds warmth waiting. The player who heard silence discovers silence at the center. Everyone is named. Everyone is present. The ending is shared — but deeply personal.

### No Failure State

There is no way to lose. No wrong answers. No puzzles to solve. The only objective: *"Volg het verhaal. Laat het toe. Kom aan bij het einde."* (Follow the story. Allow it. Arrive at the ending.)

## Language

All narrative output is in **Dutch**. The game is designed for Dutch-speaking players. The prompts, documentation, and structural labels are in English.

## GM Commands

| Command | Description |
|---------|-------------|
| `/spelers [2-6] [names]` | Register players with names |
| `/thema [text]` | Set a theme (optional — auto-generated if omitted) |
| `/beurten [N]` | Set max turns per player (optional) |
| `/beeld` | Toggle image prompt generation per chapter (optional) |
| `START` | Generate the world |
| `PROFIEL [ID]: [name, pronouns, age]` | Register a player's profile |
| `WELKOM [ID]` | Generate a player's welcome message |
| `ACTIE [ID]: [text]` | Relay a player's response/echo |
| `/status` | View session status |
| `/finale` | Trigger the shared ending |
| `/einde` | End the session |
| `/taal [NL\|EN]` | Switch output language |

## Player Responses

Players don't need commands or an AI. They simply:
- Read the DM from the GM
- Respond with what they felt, saw, or imagined
- Or send `verder` if they want to move on without sharing

There is no wrong response. The story adapts.

## Credits

Based on the echo game type from [E.C.H.O. v1.0](https://github.com/jvanheerikhuize/prompt-gallery) by Jerry van Heerikhuize.
