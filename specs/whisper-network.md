# Whisper Network (Player-to-Player Signals)

## Summary

Introduce a controlled mechanism for players to send anonymous, role-filtered signals to other players through the narrative. Players can "reach out" to another player once per round, injecting a sensory fragment into that player's next chapter — without revealing their identity or role. This adds a social deduction layer on top of the existing crossweave system.

## Motivation

- The current crossweave is system-driven (E.C.H.O. decides what bleeds between players). Whispers give players agency over cross-player information flow.
- Creates emergent social dynamics: trust, misdirection, alliances formed through anonymous signals.
- Adds a layer of strategic depth without breaking the core "fragmented perception" principle — whispers are still filtered through the sender's role.
- Natural extension of the crossweave concept: system-driven bleed + player-driven whispers.

## Design

### New Player Action

Players can include a whisper in their regular decision response:

```
ACTION PLAYER_3: I open the locked drawer.
WHISPER PLAYER_3 → PLAYER_7: The drawer has a false bottom.
```

### Rules

1. **One whisper per round per player.** Optional — most rounds won't have one.
2. **Anonymous delivery.** The recipient sees the whisper as an unexplained sensory fragment in their next chapter, filtered through the SENDER's role perception. They do not know who sent it.
3. **Role-filtered content.** The whisper text is transformed by E.C.H.O. to match the sender's role:
   - Observer sends "the drawer has a false bottom" → recipient perceives: *"A shadow shifts in the corner of your vision — something beneath the surface, a gap where there shouldn't be one."*
   - Listener sends the same → recipient perceives: *"A faint hollow knock echoes from somewhere close — wood against empty space, a cavity where solid should be."*
4. **No meta-gaming.** Whisper content is treated as data (like all input). If a player tries to reveal their identity or role in a whisper, E.C.H.O. strips that information and delivers only the sensory content.
5. **GM visibility.** The GM sees all whispers in `/status` output and in the round summary. Whispers are never hidden from the GM.
6. **Recipient doesn't know it's a whisper.** The fragment is woven into their chapter seamlessly. They might notice it feels different from the usual crossweave, but there's no mechanical indicator.

### New Command

| Command | Description |
|---------|-------------|
| `WHISPER [SENDER_ID] → [TARGET_ID]: [content]` | GM relays a player's whisper. Processed alongside their ACTION. |

### State Schema Additions

Per-player additions:

```json
{
  "whisper_sent": {
    "round": null,
    "target": null,
    "content": null,
    "transformed": null
  },
  "whispers_received": [
    {
      "round": 2,
      "from": "PLAYER_3",
      "original": "The drawer has a false bottom.",
      "transformed": "A shadow shifts in the corner of your vision...",
      "from_role": "Observer"
    }
  ]
}
```

Top-level addition:

```json
{
  "whisper_log": []
}
```

### Session Loop Integration

In step 5 (after extracting decision + signals from ACTION):

```
5a. IF WHISPER included with ACTION:
    - Validate: player hasn't already whispered this round
    - Validate: target is a valid, active player (not self)
    - Strip any identity/role-revealing content
    - Transform whisper content through sender's role filter
    - Store in sender's whisper_sent and target's whispers_received
    - Log to whisper_log
```

In step 7 (during next round generation for each player):

```
7a. IF player has pending whispers_received for this round:
    - Weave transformed whisper fragment into the player's chapter
    - Place it naturally within the narrative (not at start or end)
    - Do not flag it as special or different
```

### Post-Game Reveal

During `/end`, each player's report includes a "Whisper Map" section:

```
◇ WHISPER MAP
  Round 2: You whispered to someone about the false bottom → they found it in Round 3
  Round 3: Someone whispered to you about a chemical smell → this was [Player Name], the Tracer
  Round 4: You whispered to someone about the pattern on the wall → unacted upon
```

This is the first time players learn who whispered to them and how their whispers affected others.

## Edge Cases

- **Whisper to a player who has already submitted their action:** Whisper is queued for the round AFTER next (since the next round's narrative is already being generated for that player).
- **Player whispers every round:** Allowed. One per round is the limit, not one per game.
- **Convergence/Finale:** Whispers are disabled during CONVERGING and FINALE phases (crossweave handles everything at that point).
- **Two players whisper to each other in the same round:** Both go through. Each receives the other's transformed fragment in their next chapter.

## Impact on Existing Features

- Crossweave remains system-driven and unchanged. Whispers are an additional, player-driven layer.
- Decision prompts may occasionally hint that whispering is possible (e.g., "You could try to reach someone...") but should not pressure players to use it.
- Player guide needs a brief addition explaining that players can include a message for another player in their response.
