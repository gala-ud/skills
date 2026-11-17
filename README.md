# skills

Agent skills for solo developers: from idea to release.

Small, composable [Agent Skills](https://agentskills.io) that make a coding
agent work the way a careful one-person team does: write the spec down, plan
before coding, and check its own work before calling it done.

Works with Claude Code, Codex, Cursor, Gemini CLI and other agents that read
`SKILL.md`.

[Українською](README.uk.md)

## Install

All skills:

```bash
npx skills add gala-ud/skills
```

One skill:

```bash
npx skills add gala-ud/skills --skill plan-first
```

Or copy a folder from `skills/` into your agent's skills directory, for
example `.claude/skills/` or `.agents/skills/`.

## Skills

| Stage | Skill | What it does |
|---|---|---|
| Idea | [`idea-to-spec`](skills/idea-to-spec/SKILL.md) | Turns a rough idea into a one-page spec with explicit scope, including what version 1 will not do. |
| Plan | [`plan-first`](skills/plan-first/SKILL.md) | Writes a 3-8 step plan before touching code. Every step has a check and leaves the project working. |
| Review | [`self-review`](skills/self-review/SKILL.md) | Reviews its own diff as a skeptical reviewer before commit. Claims need a command and its output. |

More stages are on the way: schema design, debugging, tests, release, handoff.

## Principles

- **One skill, one job.** Each skill is under 100 lines and does a single thing.
- **Works next to other skill sets.** No global behavior rules and no generic
  names, so you can install these alongside the large collections.
- **Portable.** Only standard `SKILL.md` frontmatter and plain Markdown. No
  scripts, no network calls.
- **Evidence over confidence.** The agent shows what it ran and what happened.

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
