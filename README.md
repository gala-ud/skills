# skills

Small agent skills for everyday work: building software, writing, and more.

Each one is a short [Agent Skill](https://agentskills.io) that does a single
job the way a careful person would: write the spec down before building, plan
before coding, check the work before calling it done, edit a text without
changing its facts.

Works with Claude Code, Codex, Cursor, Gemini CLI and other agents that read
`SKILL.md`.

## Install

All skills:

```bash
npx skills add gala-ud/skills
```

One skill:

```bash
npx skills add gala-ud/skills --skill natural-writing
```

Or copy a folder from `skills/` into your agent's skills directory, for
example `.claude/skills/` or `.agents/skills/`.

## Skills

### Building software

| Stage | Skill | What it does |
|---|---|---|
| Idea | [`idea-to-spec`](skills/idea-to-spec/SKILL.md) | Turns a rough idea into a one-page spec with explicit scope, including what version 1 will not do. |
| Plan | [`plan-first`](skills/plan-first/SKILL.md) | Writes a 3-8 step plan before touching code. Every step has a check and leaves the project working. |
| Review | [`self-review`](skills/self-review/SKILL.md) | Reviews its own diff as a skeptical reviewer before commit. Claims need a command and its output. |
| Explore | [`architecture-sketch`](skills/architecture-sketch/SKILL.md) | Draws an architecture or sequence diagram from the code. Every box and arrow cites a file and line. |

### Writing

| Skill | What it does |
|---|---|
| [`natural-writing`](skills/natural-writing/SKILL.md) | Rewrites a draft so it reads as written by a person. Cuts stock AI phrasing and keeps every fact, number and quote. |

### Research

| Skill | What it does |
|---|---|
| [`recent-brief`](skills/recent-brief/SKILL.md) | Briefs you on what happened on a topic in the last 30 days. Every item has a date, a link and a status: confirmed, reported or chatter. |

### Reply style

| Skill | What it does |
|---|---|
| [`next-step-first`](skills/next-step-first/SKILL.md) | Puts the next action in line 1, then short numbered steps. A warning comes before the step it guards. |
| [`brief-mode`](skills/brief-mode/SKILL.md) | Short replies and compressed tool-output reports that keep every number, warning and unverified item. |

More skills are on the way, in these areas and in new ones: debugging, tests,
release, design, marketing.

## Principles

- **One skill, one job.** Each skill is under 100 lines and does a single thing.
- **Works next to other skill sets.** No global behavior rules and no generic
  names, so you can install these alongside the large collections.
- **Portable.** Only standard `SKILL.md` frontmatter and plain Markdown. No
  scripts, no network calls.
- **Evidence over confidence.** The agent shows what it ran and what happened,
  and never adds a fact you did not give it.

## Status

Early version (0.1). The skills are new and still being tested across agents.
If one does not trigger when it should, or gets in the way, please
[open an issue](https://github.com/gala-ud/skills/issues) with the prompt you
used and the agent you ran it in.

## Contributing

Issues and pull requests are welcome. For a new skill, open an issue first
describing the one job it does and when it should trigger.

## License

[MIT](LICENSE)
