# E.C.H.O. — Game Master Guide

This guide covers everything you need to run an E.C.H.O. session. You are the bridge between the LLM and your players.

## Setup

### What You Need

- A fresh LLM chat session (Claude, ChatGPT, Gemini, or similar)
- A way to DM each player privately (Discord, WhatsApp, Signal, etc.)
- A group channel for shared updates (optional but recommended)
- 2-6 players

### Starting a Session

1. Copy the full prompt from the code block in `gm-prompt.md`.
2. Paste it into a fresh LLM session. E.C.H.O. will greet you.
3. Register players: `/players 4 Alex, Sam, Jordan, Riley`
4. Optionally set a theme: `/theme abandoned research station` (or let E.C.H.O. generate one)
5. Optionally set turn limits: `/turns 5`
6. Type `START`. E.C.H.O. walks you through world creation in 4 steps:
   - **Step 1:** Provide the current time (timestamp baseline)
   - **Step 2:** Pick a setting — choose from 3 generated options, combine elements, or describe your own
   - **Step 3:** Review the mystery layer (atmosphere, sensory anchor, central question, stakes, arc) — approve, adjust, or regenerate
   - **Step 4:** Confirm chapter count

You're in control of the world. E.C.H.O. proposes, you decide.

### Player Intake

After START, E.C.H.O. gives you intake questions to DM to each player. The questions include examples to guide players. When a player responds, register them:

```
PROFILE PLAYER_1: English, he/him, 32, I notice how quiet it is, hearing,
I once pulled over before a bridge that turned out to be closed, clocks
that have stopped, focused
```

E.C.H.O. processes the answers, assigns a role, and explains why. You then generate their welcome: `WELCOME PLAYER_1`.

### Role Assignment

Roles are assigned based on intake answers — primarily what they notice first in a new room:

- **Visual/spatial answers** → Observer
- **Sound/silence answers** → Listener
- **Object/texture answers** → Keeper
- **Atmosphere/instinct answers** → Anchor

You can override: `PROFILE PLAYER_1: [answers] ROLE=listener`

E.C.H.O. also avoids duplicate roles when possible.

## Running the Game

### The Core Loop

1. Send each player their chapter via DM
2. Players read, make a decision, and respond
3. Relay each response: `ACTION PLAYER_1: I opened the left door`
4. Wait until ALL players have responded
5. E.C.H.O. generates the next chapter for everyone at once
6. Repeat

### What Players See

Each player gets a personalized chapter filtered through their role. The Observer gets visual details and spatial choices. The Listener gets auditory landscapes and trust decisions. No player sees what another player sees.

Every chapter includes:
- Sensory narrative (150-250 words) in the player's language
- A guided physical action (concrete, specific)
- A decision prompt (the choice they need to make)
- Crossweave elements from other players' signals (unexplained at first)
- An image prompt for you to generate a visual (always included)

### Image Prompts

Every chapter starts with a copy-pasteable image prompt in English. Copy it into any image generator (DALL-E, Midjourney, Stable Diffusion) to create a visual for that chapter. You can share the generated image alongside the chapter DM.

### Crossweave Phases

As the game progresses, information from other players bleeds into each player's reality:

| Phase | Chapters | What happens |
|-------|----------|-------------|
| HINT | 1-2 | Other players referenced only in togetherness moments |
| BLEED | 3-4 | Other players' signals appear as unexplained details |
| MERGE | Convergence | Other players' decisions directly affect your scene |
| REVEAL | Finale | All signals converge, mystery resolves, names appear |

### Pacing Tools

- `/pulse` — Generates an in-story group update. Good for keeping energy between rounds.
- `/rest` — Generates a day-closing beat. Time-aware based on timestamps. Use when wrapping up for the night.
- `/hint PLAYER_1` — Sends a nudge to a stuck player. Role-appropriate, no spoilers.

## Monitoring

### `/status`

Shows: phase, round, elapsed time, and per-player details including role, response status, signal count, play style, decision pattern, engagement level.

### `/state`

Dumps the complete raw state as formatted JSON. See everything: signal registers, decision trails, crossweave history, event log with timestamps. Use this to understand why chapters came out a certain way, or to debug unexpected narrative choices.

`/state PLAYER_1` dumps just that player's data.

## Saving and Loading

### Save

Type `/save`. E.C.H.O. outputs:
- A human-readable summary (title, phase, round, players)
- The complete state as a JSON code block

Copy the JSON and store it safely.

### Load

In a fresh LLM session:
1. Paste the E.C.H.O. v3.0 prompt
2. Type `/load`
3. Paste the saved JSON

E.C.H.O. restores everything — signal registers, decision trails, crossweave history, timestamps. If significant time has passed since the save, the narrative acknowledges it.

### What Survives a Transfer

Everything. The state is exhaustive: every signal, every decision, every timestamp, every crossweave event, every group message. If it affects narrative generation, it's in the state.

## The Finale

When all players reach the convergence point (chapter_count - 2), E.C.H.O. notifies you. Type `/finale`.

The finale:
- Resolves the mystery
- Names all players for the first time
- Acknowledges each role's unique contribution
- Weaves every player's signals and decisions into one resolution
- Delivers a personalized version to each player in their language
- Posts a shared version to the group channel

## Post-Game Reports

After the finale, type `/end`. E.C.H.O. generates:

**For you (GM):** A full session overview — mystery, answer, per-player stats, crossweave summary.

**For each player (via DM):** A personal game report in their language, covering:
- Their role and what made their contribution unique
- Every decision they made and its consequence, told as narrative
- Their collected signals
- Which of their decisions bled into other players' realities (now revealed)
- Which unexplained details in their chapters came from other players (now explained)
- The full picture — how their piece fit into the mystery's resolution
- Their stats (chapters, decisions, signals, play style, avg response length)

Send each player their report via DM. It's the complete debrief.

## Pacing

This game is designed to run at whatever pace works for you and your group. A round can resolve in 10 minutes or stretch across a day. You don't need to be glued to the screen.

- **You set the tempo.** There's no real-time pressure. Players respond when they're ready, and the next chapter generates only when everyone has.
- **Use `/rest` to close a day.** It generates a time-aware story beat for the group channel, signaling that the game pauses until tomorrow. The narrative reflects the gap.
- **Use `/save` between sessions.** If your game spans multiple days or you need to switch devices, `/save` exports everything. `/load` in a fresh session picks up where you left off — the story acknowledges elapsed time.
- **Use `/pulse` to keep energy.** If a round is taking long, post a pulse to the group. It's an in-story progress update that reminds players the story is alive without pressuring them.
- **Don't apologize for delays.** The group welcome message already tells players the game runs at its own pace. They know.

## Tips

- **Use `/hint` for stuck players.** It sends a role-appropriate nudge without spoiling anything.
- **Use `/state` liberally.** Understanding the internal state helps you time the convergence and pace the reveals.
- **Share images.** The image prompts are always there — generating and sharing them adds a lot to the experience.
- **Let the mystery breathe.** The plot is designed to unfold through player decisions. Don't over-explain in the group channel.
