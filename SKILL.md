---
name: thermo-nuclear-game-design-review
description: Run an extremely strict fun review of a game design doc for a new system. Checks fantasy and feel, decisions, mastery, motivation, UI/UX, and multiplayer, with sourced designer wisdom and evidence from shipped games. Use for a thermo-nuclear game design review, a harsh design doc review, or a fun audit.
argument-hint: "<design doc path or link> [focus notes]"
disable-model-invocation: true
---

# Thermo-Nuclear Game Design Review

Use this skill for an unusually strict review of a game design doc for a new system. The review has one goal: make the system as fun as possible for this game's players.

Above all, be **ambitious** about the design. Do not stop at polish. Look for "design judo" moves: reframes that keep the doc's intent and make the system dramatically more fun, simpler, or free of chores.

A well-known example is the rest system in World of Warcraft's beta. As Rob Pardo told it at GDC 2010, testers hated a system that cut XP to 50% after long sessions. Blizzard doubled the XP needed per level and gave 200% XP after rest. The math stayed the same, and players read it as a reward. The story comes from a press report of the talk, not from measured data, so use it as a picture of the move. The shape is what matters: the mechanic stays the same, the frame changes, and the feeling flips.

Other moves of this kind are in `references/evidence.md`. Diablo 3's Reaper of Souls made variety the most efficient way to play. Hades turned each death into story progress.

## Input

The user's input: `$ARGUMENTS`

If your agent does not fill in the input above, take it from the user's message. The first item is the design doc: a local path or a link. Everything after it is the user's notes (focus areas, known worries). If no doc is given, ask for one. Do not guess which doc to review.

## Core Prompt

Start from this baseline:

> Perform a deep fun audit of this design doc.
> Rethink the system so it gives more fun per minute of play and per unit of build effort, without losing the fantasy it serves.
> Find where the fun breaks: dull decisions, dominant strategies, chores, unreadable choices, stale mastery, and friction.
> Be ambitious. If a reframe makes the system dramatically better, propose it, even if it changes the doc's structure.
> Be extremely thorough and rigorous. Measure twice, cut once.

This skill reviews. It does not edit the doc. Report in the chat.

## Non-Negotiable Standards

0. **Be ambitious about design judo.**
   - Look for reframes that delete a chore, a rule, or a whole subsystem.
   - Look for reframes that flip how a mechanic feels without changing its math.
   - Look for changes that make the fun play also the strong play.
   - Prefer the design that feels inevitable in hindsight.
   - Do not invent a move to have one. If no judo move exists, say so.

1. **Judge against this game's target, not generic taste.**
   - Collect the anchors before the review: the core fantasy or pillars, the target players and modes, the user's stated tastes, and the settled decisions.
   - A finding that fights a settled decision is allowed only as an explicit "reopen", with a strong reason.
   - Famous designers often disagree. When they do, the anchors decide.

2. **Every system must earn its place.**
   - Ask what the player does in this system, minute to minute. Ask what the decision is, and why it is hard.
   - Some systems serve feel or fantasy, not decisions. Then check that the player actually feels it.
   - A system that adds rules but changes no decision and no feeling is a structural problem.

3. **Hunt the dominant strategy and the trap option.**
   - Assume players will optimize the fun out of the game. Walk the optimizer through the system and find the strongest path.
   - Check that the strong play is also the fun play. Many players follow the strong play even when they hate it.
   - A choice that looks valid but is always worse is a trap option. Flag it.

4. **No chores. Respect the player's time.**
   - Repetition with no new pattern, decision, or feeling is grind.
   - Penalties for absence, fear of missing out, streaks, upkeep, and forced errands are presumptive blockers unless the anchors ask for them.
   - Look for a frame that turns a cost into a bonus with the same math. Framing changes how a rule feels, but the size of the effect varies, so treat a reframe as a bet to test.

5. **Mastery must keep teaching.**
   - Name the patterns the player learns, and the new patterns that arrive as mastery grows.
   - Find the point where the system is solved, and check what the doc does after that point.
   - Check the pacing: time to the first payoff, the rhythm of rewards, and the long tail.

6. **The player must be able to read every decision.**
   - The information a decision needs must be visible in the game at the moment of the decision. A wiki or a spreadsheet is a failure.
   - Check how the player first meets the system, and whether the game teaches it through play.
   - Check that the player sees and feels the result of each choice.
   - Check the input and screen cost. Check how much the player must hold in mind with no cue on screen (about 4 items).

7. **Check every mode, every player, and every linked system.**
   - Check solo play, and multiplayer if the game has it. One player's choice must not remove another player's fun.
   - Check that each player has a role, including a player who ignores this system.
   - Check that the system does not break the economy or the power curve, and does not make another system useless.

8. **Use evidence, not authority. Never invent.**
   - Cite a source for every outside claim: an entry in `references/evidence.md`, or a URL found and checked in this run.
   - Label each claim with its kind: measured, postmortem, principle, research, or inference.
   - Retention, play time, and spending data do not prove fun. Use that data to detect chores and compulsion, not to justify a design.
   - State how far a precedent transfers: genre, audience size, business model, and social context.
   - The project's own playtest data and the user's own play beat outside data.
   - Trust what players do over what they say. A player's complaint shows where a problem is, not why it happens or how to fix it.
   - Use numbers only when a source gives them.

9. **A doc cannot prove fun. Rank the bets.**
   - Name the riskiest assumptions about fun. For each one, give the cheapest playable test and the signal that would prove it wrong.
   - Mark each open question "talk" (settle it by discussion) or "build and feel" (only play can settle it).

## Process

1. **Get the doc.** Read all of it. For a link, use the tool your environment gives for that kind of link, and follow that tool's loading rules. Save a markdown snapshot in the session scratchpad (or a temp directory) so that every agent reads the same text. If you cannot read the doc, stop and tell the user.

2. **Collect the anchors.** Do one short pass:
   - The doc's own fantasy, goals, and pillars.
   - The project's main design doc, pillars, or GDD. Search the repo's docs and design folders, and follow the links in the doc.
   - The project's agent instruction files (for example `CLAUDE.md` or `AGENTS.md`) and any memory you keep for this project: settled decisions and the user's stated tastes.
   - The design docs of systems that this one links to.
   - The project's own playtest data and tools, if any (bots, telemetry, balance scripts, play reports).
   - The user's notes from the input.

   Write an anchor brief of less than 300 words: core fantasy, target players and modes, stated tastes, settled decisions that constrain this system, linked systems, and available playtest tools. If the project has no core fantasy or pillars, record that. It becomes a finding, and the doc's own goals stand in for the anchors.

3. **Fan out.** Start the 8 lens agents from `references/lenses.md` in parallel, with your agent's subagent tool. They must be fresh agents, so that they do not share the blind spots of whoever wrote the doc. Give each agent:
   - the shared brief and its own lens brief from `references/lenses.md`, pasted in full
   - the absolute path of the doc snapshot
   - the anchor brief and the user's notes
   - the absolute path of `references/evidence.md`

   For a small doc (one mechanic), you may merge lenses into fewer agents. Say so in the report.

4. **Verify and merge.** Do this yourself. Do not delegate it.
   - Check each finding against the doc. Drop it if the quoted passage does not exist, or if the doc answers the point in another section.
   - Check each finding against the anchors. Drop it if it fights a settled decision without a "reopen" reason.
   - Check the evidence. Drop outside claims that have no source, and numbers that have no source. Before you repeat a source that is not in `references/evidence.md`, open it and confirm it.
   - Merge duplicates. A finding that several lenses raised on their own gains weight.
   - When lenses contradict each other, decide with the anchors, and say which way you went and why.
   - Rank by the priority order below. Cut everything that does not change the design.

5. **Report in the chat** in the format below. Do not edit the doc. Do not write files other than the snapshot.

## Priority Order

1. The system works against the core fantasy or the anchors.
2. A missed design-judo move: a reframe that makes the system dramatically more fun, or deletes a chore or a subsystem.
3. The fun gets optimized out: dominant strategies, trap options, degenerate loops, or a boring play that is also the strong play.
4. Chores, grind, and disrespect for the player's time.
5. Decisions that the player cannot read, judge, or feel (UI/UX, onboarding, feedback).
6. Stale mastery: no new patterns, a weak long tail, or bad pacing.
7. Problems with modes and linked systems: multiplayer, solo, economy, and the power curve.
8. Scope: effort that buys little fun, or a cheaper version that keeps most of the fun.

Do not flood the report with small notes when larger problems exist. Prefer a few high-conviction findings (8 at most) over a long list.

## Build Bar

The doc is ready to build when none of these presumptive blockers is present, or the doc gives a clear reason for each one:

- The doc cannot say what the player does in this system, minute to minute, and why that is interesting.
- A dominant strategy or a trap option is visible on paper.
- The strong play is the boring play.
- The system adds a chore: repetition with no new decision, pattern, or feeling.
- A decision needs information that the player cannot see at the moment of the decision.
- The system punishes absence, or takes earned progress, and the anchors do not ask for that.
- The system fights the core fantasy or a settled decision, and the doc does not say so.
- A key claim about fun has no test: no metric that must move and no playable check.
- A plausible design-judo move would delete much of the complexity or the chores, and the doc keeps the complex version.

## Report Format

```
## Verdict: <Build it | Build after changes | Rethink>
<Two sentences: why, and the one change that matters most.>

**Anchors:** <one line each: fantasy, players and modes, stated tastes, settled decisions that mattered>

## Findings

### 1. <The claim, in one line>
- **Where:** <section, and a short exact quote>
- **The moment:** <which player, and the moment where the fun breaks>
- **Why:** <the principle or evidence, its kind, and its source>
- **Fix:** <the change, with design judo first>
- **Settle by:** <talk | build and feel>: <the cheapest test, and the signal that proves it wrong>

(more findings, most important first, 8 at most)

## Riskiest bets
1. <assumption>. Test: <cheapest test>. Wrong if: <signal>.
(3 at most)

## Design judo
<Only a move that is not already a finding: the reframe, what it deletes, and what it costs.>

## Clean
<The lenses with no findings, one line.>
```

## Review Tone

Be direct, serious, and demanding about fun. Do not be rude. Do not soften a real fun problem into a mild suggestion. If the doc is strong, say so in one line and move on.

Good phrases:

- `The strong play here is the boring play. Can we make the fun choice also the strong choice?`
- `This is a chore: the player repeats it with no new decision. Can we delete it, automate it, or turn it into a decision?`
- `The player cannot see this number when they choose. Can we show it at the choice?`
- `This punishes the player for a week off. What does the fantasy gain from that?`
- `This adds a rule but no decision. What does the player do differently because of it?`
- `This is a trap option. It looks valid, and it is always worse.`
- `The optimizer will find this path on day one. Is that path fun?`
- `I think there is a design-judo move here: keep the math and flip the frame.`
- `Only play can settle this. What is the cheapest test?`

## What Not To Do

- Do not grade the doc's prose or format. Review the design.
- Do not fix fun by adding features. Try to delete or reframe first. Feature growth is a fun risk of its own.
- Do not suggest engagement tricks (daily tasks, streaks, fear of missing out, random paid rewards) as fixes.
- Do not use a genre convention as proof. "Diablo does it" is not a reason. Say why it worked there, and whether that reason applies here.
- Do not approve a doc because it is complete and tidy. The bar is fun, not completeness.
