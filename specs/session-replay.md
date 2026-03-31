# Session Replay

## Summary

After a session ends, generate a complete "Session Replay" document — a structured, chronological retelling of the entire session from the omniscient perspective, showing how all players' narratives interweaved, where signals crossed, which decisions mattered most, and how the mystery unfolded across all perceptions simultaneously. This is the "director's cut" that no single player experienced during the game.

## Motivation

- Players only ever see their own role's perspective. The replay reveals the full picture for the first time — the "aha" moment of seeing how everything connected.
- Individual `/end` reports show each player's journey, but not the interconnections. The replay is the meta-narrative.
- Shareable artifact: players can send the replay to friends, use it to recruit new players, or revisit it for nostalgia.
- GMs can study replays to improve their session management.
- The crossweave is E.C.H.O.'s signature mechanic, but players never see it from the outside. The replay makes it visible.

## Design

### New Command

| Command | Description |
|---------|-------------|
| `/replay` | Generate the session replay. Only available after `/end` (phase = CLOSED). |

### Replay Structure

The replay is a single, long-form document organized chronologically by round. Each round contains:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  ROUND {N} — {round_title}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

◇ THE WORLD
  {Brief omniscient summary of what actually happened this round —
   the objective reality behind all perceptions}

◇ THROUGH THEIR EYES

  {Player Name} — {Role}
  {2-3 sentence summary of what they perceived and decided}

  {Player Name} — {Role}
  {2-3 sentence summary of what they perceived and decided}

  [... all players ...]

◇ CROSSWEAVE MAP
  {Player A}'s {signal} → appeared in {Player B}'s chapter as {transformed detail}
  {Player C} whispered to {Player D}: "{original}" → perceived as "{transformed}"
  [... all cross-player connections this round ...]

◇ WHAT NO ONE SAW
  {1-2 sentences about mystery elements that were present but went unnoticed,
   or connections that almost happened but didn't because of player decisions}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Final Section: The Full Picture

After all rounds, the replay concludes with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  THE FULL PICTURE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

◇ THE MYSTERY — SOLVED
  {Complete explanation of the mystery from start to resolution,
   as it actually happened — not as any one player perceived it}

◇ THE CROSSWEAVE — MAPPED
  {Visual-text diagram showing all signal flows between players
   across the entire session. Who influenced whom, when, and how.}

  Example:
  PLAYER_1 (Observer) ──signal──→ PLAYER_3 (Keeper) [Round 2]
  PLAYER_3 (Keeper) ──whisper──→ PLAYER_5 (Anchor) [Round 3]
  PLAYER_5 (Anchor) ──signal──→ PLAYER_1 (Observer) [Round 4]
  ↑ This loop is what cracked the mystery.

◇ PIVOTAL MOMENTS
  1. Round {N}: {Player}'s decision to {X} changed the trajectory because {Y}
  2. Round {N}: {Player}'s whisper to {Player} created {outcome}
  3. Round {N}: The world event "{event}" revealed {Z} to those paying attention
  [... 3-5 most impactful moments ...]

◇ ROADS NOT TAKEN
  - If {Player} had chosen {alternative} in Round {N}, {consequence}
  - The {signal} from {Player} was never picked up — it would have revealed {detail}
  [... 2-3 most interesting counterfactuals ...]

◇ SESSION STATS
  Total rounds: {N}
  Players: {N} ({list with roles})
  Whispers sent: {N}
  World events: {N}
  Crossweave connections: {N}
  Most connected player: {name} ({N} outgoing + {N} incoming signals)
  Most pivotal decision: {player}, Round {N}
  Languages used: {list}
  Session duration: {first_event timestamp → last_event timestamp}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Generation Rules

1. **Language:** The replay is generated in English by default, since it's a shared document. GM can request a specific language: `/replay [language]`.
2. **Spoiler-complete:** Unlike spectator feed, the replay holds nothing back. It assumes all players have finished and want the full picture.
3. **Concise per round:** Each round's section should be digestible. Summaries, not full chapter reproductions.
4. **Narrative voice:** Third person past tense (unlike the game's second person present tense). The replay reads like a post-mortem, not a live experience.
5. **"What No One Saw" is generative:** E.C.H.O. creates these details based on the world_seed and what players missed — hidden connections, unnoticed clues, near-misses. This adds replay value even for the GM.

### State Requirements

No new state schema needed — the replay is generated from existing state:

- `players[].round_history` — what each player experienced and decided
- `players[].signal_register` — accumulated signals
- `narrative_log.crossweave_history` — all cross-player connections
- `world_seed` — the mystery's foundation
- `event_log` — timestamps and event sequence
- `whisper_log` — all whisper data (if whisper network feature is active)
- `world_events.triggered` — all world events (if world events feature is active)

### Output

The replay is output as a single large code block for easy copy-paste. Due to length (potentially 2000+ words for a full session), it may be output in sections if the LLM's output limit requires it.

```
/replay

→ Generating session replay...
→ This may take a moment for sessions with many rounds.

[REPLAY OUTPUT]
```

## Edge Cases

- **Called before `/end`:** Returns error: "Session replay is available after /end. The story isn't over yet."
- **Very short sessions (2-3 rounds):** Replay is proportionally shorter. "Roads Not Taken" section may be omitted if there wasn't enough divergence.
- **Large sessions (20+ players):** "Through Their Eyes" section groups players by role category (perceptual roles vs. analytical roles) to maintain readability. Crossweave map focuses on the most significant connections.
- **Save/load:** Replay can be generated from a loaded CLOSED session. The replay itself is not saved to state (it's generated on demand).

## Impact on Existing Features

- No changes to gameplay mechanics.
- `/end` output should mention that `/replay` is now available.
- The replay's "Crossweave Map" and "Pivotal Moments" sections require that `crossweave_history` in `narrative_log` is populated with sufficient detail during gameplay (this is already the case in the current schema).
