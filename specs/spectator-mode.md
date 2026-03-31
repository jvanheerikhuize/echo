# Spectator Mode

## Summary

Allow non-players to follow a live E.C.H.O. session as read-only spectators via a dedicated group channel. Spectators see a curated "omniscient narrator" feed that weaves together all players' perspectives without revealing the mystery's resolution — preserving tension while enabling an audience experience.

## Motivation

- Players often tell friends about sessions after the fact, but the magic is in the unfolding. Spectators let others experience that live.
- GMs sometimes want to showcase E.C.H.O. to potential players before they commit.
- Session recordings lose the real-time pacing that makes the crossweave compelling.
- Grows the community: spectators become future players.

## Design

### New Commands

| Command | Description |
|---------|-------------|
| `/spectate [channel]` | Register a spectator channel (group chat link/name). Can be set during SETUP or ACTIVE phase. |
| `/spectate off` | Disable spectator feed. |

### Spectator Feed Behavior

- **What spectators see:** After each round completes, a single "omniscient beat" is generated — a 100-200 word narrative paragraph that blends sensory threads from all players' chapters without attributing them to specific roles.
- **What spectators don't see:** Role assignments, individual player decisions, signal registers, decision prompts, or the mystery's resolution mechanism. Player names ARE visible (they're public participants), but their roles remain hidden.
- **Timing:** The spectator beat is generated and output AFTER all player chapters for that round, as part of the round completion flow.
- **Finale:** During `/finale`, spectators receive a version of the resolution that reveals the mystery but omits per-player signal details. During `/end`, spectators get a summary of the session (theme, round count, player count) but NOT individual player reports.

### State Schema Additions

```json
{
  "spectator": {
    "enabled": false,
    "channel": null,
    "feed_log": []
  }
}
```

### Output Template: SPECTATOR_BEAT

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ROUND {N} — OMNISCIENT FEED

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

{Blended narrative paragraph — all senses, no role attribution, present tense, atmospheric}

  ◇ {number} players acted this round
  ◇ Crossweave intensity: {HINT|BLEED|MERGE|REVEAL}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Narrative Generation Rules

- The spectator beat must NOT simply concatenate player chapters. It is a new, synthesized paragraph that captures the round's atmosphere from an omniscient vantage point.
- Sensory details from all active roles should appear, but without flagging which role perceived them (e.g., "A door creaks somewhere below" rather than "The Listener hears a door creak").
- Tension and arc position should match the players' experience.
- Language: Always English (spectator channel is public/shared).

### Session Loop Integration

Insert after step 9 in the current SESSION_LOOP (after round output, before GM copies DMs):

```
9a. IF spectator.enabled:
    - Generate SPECTATOR_BEAT from all players' round narratives
    - Append to spectator.feed_log
    - Output SPECTATOR_BEAT template (GM copies to spectator channel)
```

## Edge Cases

- **Mid-session join:** `/spectate` can be enabled mid-game. No backfill — feed starts from the current round.
- **Single player remaining:** Spectator beat still generates from the solo player's chapter (reduced blending).
- **Save/load:** `spectator` state is included in save. On load, GM must re-confirm the spectator channel is still active.

## Impact on Existing Features

- No changes to player-facing narrative or mechanics.
- Adds one optional output per round for the GM to relay.
- State schema grows by one top-level key.
- `/status` should include spectator status (enabled/disabled, channel).
