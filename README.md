# E.C.H.O. — Experiential Collaborative Hub Orchestrator

A shared, immersive sensory narrative experience for 2-6 players, powered by any advanced LLM.

Players are guided through an immersive story that engages all five senses, narrated with the dry wit of a classic Infocom text adventure. Everyone plays alone — but the story weaves them together, and they arrive at the same ending: **samen, alleen** (together, alone).

## How It Works

E.C.H.O. uses a **hub-and-spoke architecture**. One person acts as Game Master (GM) and runs the hub prompt. Each player gets a personalized spoke prompt in their own LLM session. The GM relays messages between sessions.

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
   │  own LLM     │ │  own LLM     │ │  own LLM     │
   │  own spoke   │ │  own spoke   │ │  own spoke   │
   └──────────────┘ └──────────────┘ └──────────────┘
```

## Quick Start

1. Copy the prompt from the code block in [`prompt.md`](prompt.md).
2. Paste it into a fresh LLM session (Claude, ChatGPT, Gemini). This is the **GM session**.
3. Configure: `/spelers 3 Alice, Bob, Charlie` and optionally `/thema` and `/duur`.
4. Type `START`. E.C.H.O. generates the world.
5. Run `GENEREER SPOKE SPELER_1`, `GENEREER SPOKE SPELER_2`, etc.
6. Send each player their spoke via DM. They paste it into their own LLM session.
7. Players interact with their spoke. They send actions to you via DM.
8. You relay with `ACTIE SPELER_1: [what they said]`. E.C.H.O. generates the next chapter.
9. Send the chapter back to the player via DM. Repeat.
10. When everyone reaches the convergence point, type `/finale` for the shared ending.

## What Makes This Special

### The Echo Mechanic

After each chapter, the player's spoke invites them to share what they felt, saw, or imagined. This response — their **echo** — gets relayed to the GM hub. The GM extracts sensory and emotional keywords and stores them in an **echo register** per player.

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
| `/duur [Nmin]` | Set time limit in minutes (optional) |
| `START` | Generate the world |
| `GENEREER SPOKE [ID]` | Generate a player's spoke prompt |
| `ACTIE [ID]: [text]` | Relay a player's action/echo |
| `/status` | View session status |
| `/finale` | Trigger the shared ending |
| `/einde` | End the session |
| `/taal [NL\|EN]` | Switch output language |

## Player Commands

| Command | Description |
|---------|-------------|
| `verder` | Advance to the next chapter |
| `herhaal` | Re-experience the current chapter |
| `pauzeer` | Pause — the story waits |
| `/status` | See where you are in the story |
| *(free text)* | Share your echo — what you felt, saw, imagined |

## Credits

Based on the echo game type from [E.C.H.O. v1.0](https://github.com/jvanheerikhuize/prompt-gallery) by Jerry van Heerikhuize.
