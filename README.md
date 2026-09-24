# Thermo-Nuclear Game Design Review

A Claude Code skill that reviews a game design doc with one goal: make the system as fun as possible. It runs 8 lens agents in parallel and cites a checked file of designer principles, live-game data, and research. One review uses a few hundred thousand tokens.

```
npx skills add wescopeland/thermo-nuclear-game-design-review
```

```
/thermo-nuclear-game-design-review <design doc path or link> [focus notes]
```

Adapted from Cursor's [thermo-nuclear-code-quality-review](https://github.com/cursor/plugins/tree/main/cursor-team-kit/skills/thermo-nuclear-code-quality-review) (MIT). [MIT licensed](LICENSE).
