# Thermo-Nuclear Game Design Review

A Claude Code skill that runs an extremely strict fun review of a game design doc for a new system.

The review has one goal: make the system as fun as possible for the game's players. It looks for "design judo": a reframe that keeps the doc's intent and makes the system much more fun, simpler, or free of chores.

## How it works

1. It reads the doc (a local path or a link) and saves a snapshot, so every reviewer sees the same text.
2. It collects the game's anchors: the core fantasy, the target players and modes, your stated tastes, the settled decisions, the linked systems, and your playtest tools. Findings are judged against these anchors, not against generic taste.
3. It starts 8 fresh agents in parallel, one per lens:
   - fantasy and feel
   - decisions and dominant strategies
   - mastery, pacing, and staleness
   - motivation and respect for the player's time
   - UI/UX and onboarding
   - modes and other players
   - precedents from shipped games
   - walkthroughs as four players: the optimizer, the newcomer, the returner, and the other player
4. It checks each finding against the doc, the anchors, and the sources. Then it merges the findings and ranks them.
5. It reports in chat: a verdict, up to 8 findings, the riskiest bets with the cheapest test for each, the design-judo moves, and the lenses that came back clean.

The skill does not edit the doc.

## Evidence

`references/evidence.md` holds 97 entries: designer principles, data from live games, research on player psychology and UX, and precedents from shipped games. Research agents opened each source, and they dropped every claim that they could not confirm. Each entry names its source, says how it was checked, and says how far it transfers.

The file also lists famous stories that are wrong or overstated, and claims that the research could not confirm. Reviewers must not cite those claims.

Retention, play time, and spending data do not prove fun. The review uses that data only to find chores and compulsion.

## Install

With the [skills CLI](https://github.com/vercel-labs/skills):

```
npx skills add wescopeland/thermo-nuclear-game-design-review
```

Or copy this repo into `~/.claude/skills/thermo-nuclear-game-design-review/`.

## Usage

```
/thermo-nuclear-game-design-review <design doc path or link> [focus notes]
```

Only you can start the skill (`disable-model-invocation: true`). Claude does not start it by itself.

Each run starts 8 agents, and each agent reads about 40k tokens of evidence. Expect a few hundred thousand tokens per review.

## Credit

The structure is adapted from the `thermo-nuclear-code-quality-review` skill in [cursor/plugins](https://github.com/cursor/plugins/tree/main/cursor-team-kit/skills/thermo-nuclear-code-quality-review) (MIT License, Copyright (c) 2026 Cursor).

## License

MIT. See [LICENSE](LICENSE).
