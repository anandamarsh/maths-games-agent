# maths-games-agent

> A Claude Agent Teams framework for building interactive maths games from a teaching objective — no coding experience required.

---

## What this is

This repo is the **agent instruction set** for creating games on the [Interactive Maths](https://interactive-maths.vercel.app) platform.

You bring a teaching objective. The agents handle the rest:

- **BA agent** — turns your brief into a full game spec
- **Dev agent** — builds the game from the spec
- **Tester agent** — writes and runs Playwright tests, loops with Dev on failures
- **UAT agent** — validates the game meets the teaching objective, approves or rejects

All agents run via [Claude Code Agent Teams](https://docs.anthropic.com/en/docs/claude-code/overview). Your game code lives in your own repo — this framework is just the instruction set.

---

## How it works

```
maths-games-agent/      ← you are here (framework + agent roles)
    orchestrator.md
    roles/
        BA.md
        DEV.md
        TEST.md
        UAT.md

maths-game-[name]/      ← your game repo (forked from template)
    specs/
        brief.md        ← you write this (5 lines)
        spec.md         ← BA agent writes this
    src/
    tests/
```

1. Fork [maths-game-template](https://github.com/anandamarsh/maths-game-template)
2. Write `specs/brief.md` — teaching objective, age group, mechanic idea
3. Clone this repo and run the orchestrator, pointing it at your game repo
4. Agent Team builds, tests, and validates the game
5. Deploy to Vercel, submit to Interactive Maths

---

## Quick start

```bash
# 1. Fork the game template
gh repo fork anandamarsh/maths-game-template --clone --rename maths-game-[your-game-name]

# 2. Write your brief
cd maths-game-[your-game-name]
# edit specs/brief.md

# 3. Clone this framework
gh repo clone anandamarsh/maths-games-agent

# 4. Run the orchestrator (requires Claude Code)
cd maths-games-agent
claude  # then follow orchestrator.md instructions
```

---

## specs/brief.md format

Keep it short. The BA agent does the heavy lifting.

```markdown
# Game Brief

**Teaching objective:** [e.g. recognise multiples of 3 up to 30]
**Age group:** [e.g. 7–9]
**Mechanic idea:** [e.g. pop balloons that show multiples of 3]
**Theme:** [e.g. circus, space, underwater — or leave blank]
**Notes:** [anything else — difficulty curve, accessibility needs, etc.]
```

---

## Agent roles

| Agent | Input | Output |
|-------|-------|--------|
| BA | `specs/brief.md` | `specs/spec.md` |
| Dev | `specs/spec.md` | game code in `src/` |
| Tester | game code | Playwright tests + pass/fail report |
| UAT | spec + test results | approval or rejection with feedback |

Full role prompts are in [`roles/`](./roles/).

---

## Repo structure

```
maths-games-agent/
├── CLAUDE.md               # shared context for all agents
├── orchestrator.md         # master runbook — start here
├── roles/
│   ├── BA.md               # BA agent instructions
│   ├── DEV.md              # Dev agent instructions
│   ├── TEST.md             # Tester agent instructions
│   └── UAT.md              # UAT agent instructions
└── README.md
```

---

## Contributing

This is an open framework. PRs welcome for:
- Improving agent role prompts
- Adding orchestrator variants (e.g. fast mode, review-only mode)
- Documentation and examples

Please open an issue before submitting large changes to role prompts.

---

## Related

- [maths-game-template](https://github.com/anandamarsh/maths-game-template) — the game starter kit
- [interactive-maths](https://interactive-maths.vercel.app) — the platform where games are published

---

## License

MIT
