# Dynamic World Events

## Summary

Introduce GM-triggered and system-suggested environmental events that affect all players simultaneously, creating shared anchor moments in the narrative. World events are seismic shifts — a power outage, an alarm, a tremor, a stranger arriving — that every role perceives through their own lens, giving players a common reference point to discuss (or disagree about) in the group channel.

## Motivation

- The current system generates per-player narratives that can feel isolated until crossweave intensifies. World events create immediate shared experience.
- Gives the GM an active storytelling lever beyond relaying actions and commands.
- Creates "water cooler moments" — events players can reference in the group channel ("Did anyone else feel that tremor?") where each role's answer is genuinely different.
- Adds unpredictability: even experienced players won't know when a world event hits.
- Strengthens the mystery: world events can serve as clues that only make sense when all role-perspectives are combined.

## Design

### Event Types

| Type | Trigger | Description |
|------|---------|-------------|
| **GM Event** | `/event [description]` | GM describes an event; E.C.H.O. renders it through each role's perception. |
| **Suggested Event** | System-generated | E.C.H.O. suggests an event to the GM based on narrative state (tension plateau, pacing lull, arc position). GM approves or ignores. |
| **Timed Event** | Pre-scheduled | GM sets an event to trigger at a specific round during setup or mid-game. |

### New Commands

| Command | Description |
|---------|-------------|
| `/event [description]` | Trigger an immediate world event. Inserted into the NEXT round's narratives for all players. |
| `/event at [round] [description]` | Schedule a world event for a future round. |
| `/events` | List all scheduled and past world events. |

### Event Rendering Rules

1. **Every role perceives the same event differently.** A power outage: the Observer sees darkness fall, the Listener hears the hum die, the Keeper feels the lock mechanism release, the Anchor senses the temperature shift, the Tracer smells ozone, the Weaver sees data screens flicker, the Mirror watches faces change, the Drifter feels the air pressure shift.
2. **Events are woven into chapters, not appended.** They should feel like part of the narrative, not an interruption.
3. **Events affect the world state.** After a power outage, subsequent chapters reflect that the power is out (dark environments, emergency lighting, etc.) until the narrative resolves it.
4. **Events carry mystery weight.** Each event should connect to the world_seed's mystery in some way — even if that connection only becomes clear later.
5. **Max one world event per round.** Events are impactful because they're rare.

### Suggested Events

E.C.H.O. can suggest events to the GM when it detects:

- **Pacing lull:** Multiple players gave short, low-engagement responses.
- **Tension plateau:** Narrative tension has been flat for 2+ rounds.
- **Arc opportunity:** The mystery's arc would benefit from an external catalyst.
- **Crossweave gap:** Players' narratives have diverged too far; a shared event re-anchors them.

Suggestions appear in `/status` output:

```
◇ SUGGESTED EVENT
  "A distant alarm begins — intermittent, mechanical, from below the building."
  Reason: Tension has plateaued. This would re-anchor diverging narratives.
  Type: /event to trigger now, or /event at 5 to schedule
```

The GM is never forced to use suggested events. They are recommendations only.

### State Schema Additions

```json
{
  "world_events": {
    "scheduled": [
      {
        "round": 5,
        "description": "The lights go out. All of them. At once.",
        "source": "gm"
      }
    ],
    "triggered": [
      {
        "round": 3,
        "description": "A door slams somewhere deep in the building.",
        "source": "gm",
        "per_role_rendering": {
          "Observer": "...",
          "Listener": "...",
          "Keeper": "..."
        }
      }
    ],
    "suggested": []
  }
}
```

### Session Loop Integration

In step 7 (round generation), before generating individual player chapters:

```
7c. IF world_events.scheduled contains an event for current_round:
    - Move event from scheduled to triggered
    - Generate per-role rendering of the event
    - Store renderings in the event record
    - Weave each role's rendering into the corresponding player's chapter
    - Update world state to reflect the event's consequences
```

After round generation (in status computation):

```
IF pacing/tension/arc conditions suggest an event:
    - Generate suggested event with rationale
    - Store in world_events.suggested
    - Show in next /status output
```

### Output Template: EVENT_TRIGGERED

Shown to GM after `/event` is processed:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  WORLD EVENT QUEUED — ROUND {N}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  "{event description}"

  Will appear in all players' Round {N} chapters,
  filtered through each role's perception.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Group Channel Integration

After a world event round completes, E.C.H.O. generates a brief group channel message:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Something just changed.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

This is deliberately vague — it signals to the group that everyone experienced something, inviting discussion. The discussion itself becomes fuel for the crossweave and mystery.

## Edge Cases

- **Event during SETUP/CONVERGING:** Events can only be triggered during ACTIVE phase. `/event` returns an error in other phases.
- **Event with no active players:** Queued event is skipped and logged as "skipped — no active players."
- **Conflicting events:** If a GM event and a scheduled event target the same round, the GM event takes priority and the scheduled event is pushed to the next round.
- **Save/load:** All event state (scheduled, triggered, suggested) is preserved.
- **Short games:** E.C.H.O. should suggest fewer events for games with < 5 total rounds to avoid overwhelming the narrative.

## Impact on Existing Features

- Crossweave benefits from world events — shared anchor moments create natural crossweave opportunities.
- `/pulse` and `/rest` remain distinct: they are pacing tools, not narrative events. World events change the story; pulse/rest manage rhythm.
- Image generation prompts should reflect world events when they occur (e.g., darkness, emergency lighting, etc.).
- World events are logged in `event_log` as `WORLD_EVENT` type.
