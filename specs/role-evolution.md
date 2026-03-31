# Role Evolution

## Summary

As the game progresses, each player's role develops a secondary perception — a partial ability to sense through another role's lens. This evolution is driven by the player's decisions and crossweave exposure, not random chance. By the convergence point, each player perceives reality through 1.5 roles instead of 1, creating richer narratives and a more satisfying sense of character growth.

## Motivation

- Players currently have a static perception throughout the game. Adding growth gives a sense of progression and reward for engaged play.
- Creates a natural narrative arc: you start seeing the world one way, then something shifts.
- The crossweave already bleeds other players' signals into your chapters — evolution makes this personal, not just environmental.
- Adds replayability: the same role can evolve differently based on decisions.
- Mirrors real human experience: intense situations sharpen unexpected senses.

## Design

### Evolution Triggers

Evolution is NOT automatic or time-based. It's triggered by a combination of:

1. **Decision pattern analysis:** E.C.H.O. tracks what kind of decisions a player gravitates toward. A Keeper who consistently makes trust-based decisions (Mirror territory) may develop Mirror as their secondary.
2. **Crossweave absorption:** If a player's chapters have received significant bleed from a specific other role (via crossweave or whispers), that role becomes a candidate.
3. **Narrative opportunity:** Evolution triggers when there's a natural story moment — a decision that would logically open a new perceptual channel.

### Evolution Timing

- **Earliest:** Round 3 (enough data to analyze patterns).
- **Latest:** Convergence point (must happen before finale).
- **Typical:** Rounds 3-5 for most players.
- **One evolution per player per game.** No stacking.

### Secondary Perception Rules

- The secondary role operates at ~30% intensity compared to the primary. It adds texture, not dominance.
- Primary role still controls decision prompts and the main narrative thread.
- Secondary perception appears as "flickers" — brief moments of unexpected awareness woven into the chapter.
- The evolution moment itself is a memorable narrative beat: a distinct sensory shift the player experiences in-story.

### Example

**Player:** Keeper (primary) → evolves Mirror (secondary)

**Before evolution (Round 2):**
> You run your fingers along the shelf's edge. Third book from the left sits wrong — pushed too far back, spine cracked at page 47. Someone opened this recently and didn't care about hiding it. You pull it free. A key falls from between the pages, brass, warm from the shelf's heat.

**Evolution moment (Round 3):**
> You reach for the next drawer and stop. Not because of what's inside — because of the woman standing at the far desk. You've never paid attention to people before. But something in the way her hands hover above the papers without touching them, the micro-pause before she turns a page — she's pretending to read. You know pretending. You've catalogued a hundred objects left to look casual. She's doing the same thing, but with her whole body.

**After evolution (Round 4):**
> The cabinet yields three folders, each sealed with different tape — institutional, hasty, careful. You sort them by intent. Across the room, two people enter and immediately separate. The tall one gravitates toward the window with practiced nonchalance. The other stands too still. You file this alongside the folders: things arranged to look natural that aren't.

### State Schema Additions

Per-player additions:

```json
{
  "role_evolution": {
    "secondary_role": null,
    "evolved_at_round": null,
    "trigger": null,
    "intensity": 0.3
  }
}
```

### Narrative Generation Integration

In step 7 (round generation), after gathering the player's role context:

```
7b. IF player.role_evolution.secondary_role is set:
    - Include secondary role's perception at reduced intensity
    - Add 1-2 "flicker" moments per chapter from the secondary sense
    - Secondary perception should feel new and slightly disorienting to the character
    - Decision prompts remain primary-role-driven but may include secondary awareness
```

### Evolution Selection Logic

```
WHEN round >= 3 AND player.role_evolution.secondary_role is null:
  1. Analyze player.decision_trail for patterns outside primary role's domain
  2. Check crossweave_history for dominant incoming role signals
  3. Score candidate roles by (decision_affinity * 0.6) + (crossweave_exposure * 0.4)
  4. Select highest-scoring role that is NOT the player's primary role
  5. Find or create a natural narrative moment in the current round
  6. Trigger evolution, store in state
```

### GM Visibility

- `/status` shows evolution state per player (evolved or pending, secondary role if assigned).
- Evolution is logged in `event_log` as `ROLE_EVOLUTION` event.
- GM is NOT asked to approve evolutions — they happen organically. But GM can see them coming in `/status` (candidate roles are shown before evolution triggers).

### Post-Game Report Addition

Each player's `/end` report includes:

```
◇ ROLE EVOLUTION
  Primary: Keeper (objects, mechanisms, traces)
  Secondary: Mirror (developed Round 3)
  Trigger: Your decisions consistently revealed attention to people's intentions, not just their possessions.
  Evolution moment: "You reached for the drawer and stopped..."
```

## Edge Cases

- **Player is very consistent with their primary role:** Evolution still happens, but later (Round 5+) and the secondary may be a "complementary" role (e.g., Observer → Weaver, since visual patterns feed into pattern analysis).
- **All players evolve the same secondary:** Possible but unlikely given different decision patterns. No restriction needed.
- **Short games (3-4 rounds total):** Evolution triggers earlier (Round 2 minimum) or may be skipped entirely if total_rounds < 4.
- **Save/load:** Evolution state is fully preserved. If evolution hasn't triggered yet, the analysis continues from the loaded state.

## Impact on Existing Features

- Crossweave is unchanged — it still operates on primary roles. Secondary perception is a per-player narrative enhancement, not a crossweave channel.
- Decision prompts remain primary-role-driven to maintain clarity.
- Image generation prompts should incorporate secondary perception elements after evolution.
- Role assignment logic is unchanged — secondary roles emerge from play, not from profiles.
