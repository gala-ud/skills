---
name: ship-checklist
description: Release gate and release notes. Runs the release checks on the exact commit being shipped and records each as pass, fail or not run with its command, gives a go or no-go, derives the version bump from what changed for users, and writes user-facing release notes with breaking changes first and a rollback line. Stops before tagging, pushing or publishing. Use when the user asks to ship, release, cut or tag a version, prepare a release, check whether something is ready to release, or write release notes or a changelog entry. Skip for an ordinary commit or pull request during development, and for setting up deployment or CI infrastructure.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Ship checklist

Asked to release, an agent reports checks as passed from memory, sizes the
version bump by how big the diff looks, turns commit subjects into release
notes and tags before anyone has looked. This skill produces evidence for a
decision, then stops.

## Process

1. **Pin what ships.** Record the commit (`git rev-parse --short HEAD`),
   the last release tag and the commit range since it. Run `git status`:
   uncommitted changes are not part of the release, and you say so first.
2. **Read the diff of the range, not the commit subjects**
   (`git diff <tag>..HEAD`). List every change to the public surface:
   commands and flags, exported functions, HTTP routes, config keys,
   environment variables, file formats, database schema. For each change
   that looks breaking, run the old usage against the new code when it can
   be run, and record "confirmed by running" or "by reading only".
3. **Run the checks** with the project's own commands (CI file, Makefile,
   package scripts) and fill the table. Status is one of: pass, FAIL,
   not run (reason), n/a (reason).
   - Tests: the full suite. Count skipped tests and name any skip added
     in the range.
   - Build or package, if the project has such a step.
   - Version: every place the version string appears agrees.
   - Leftovers in the range diff: debug output, TODO or WIP markers,
     secrets, personal paths.
   - Migrations and data changes in the range: can each be undone?
   - Dependencies added or changed: the lockfile matches.
   - Docs: README and help text match every public-surface change. The
     changelog entry for this release is written in step 8, so its absence
     is not a failure.
4. **Give the verdict.** No-go if any check is FAIL or if tests were not
   run. Go with risks if anything else is not run. Otherwise go.
5. **Choose the bump from step 2**, with one line of reasoning: a breaking
   change to the public surface is a major bump (below 1.0.0, a minor one,
   and say so); a new backward-compatible capability is minor; anything
   else is a patch. A project with another scheme keeps it.
6. **Write the release notes** in the project's changelog format, with
   breaking changes marked and listed first; with no such format use the
   groups Breaking, Added, Changed, Fixed, Security and omit empty ones.
   Each line says what changes for a user, and each breaking line says
   what the user must do. Leave out changes users cannot observe
   (refactors, tests, CI).
7. **Write the rollback line**: the version to go back to, and anything in
   this release that going back would not undo.
8. **Stop.** Show the report. On a go, when the user asked to prepare or
   make the release, edit the changelog and version files. Tagging,
   pushing, publishing and deploying happen only when the user asked for
   that action by name. On a no-go, change no files and do none of these
   until the user has seen the report and asks again. After tagging,
   pushing or publishing, verify it (`git ls-remote --tags`, the registry
   page) before reporting it done.

Asked only for release notes: do steps 1, 2, 5, 6 and 7 and state that the
checks were not run. Show the notes in the reply; write them into the
changelog file only if the user asked for the file to be changed.

## Report

```markdown
## Release check: <name> <old version> -> <new version>
Commit `<hash>`, range `<tag>..HEAD` (<n> commits). Working tree: clean

**Verdict: NO-GO** - <the failing check, in one line>

| Check | Command | Result |
|---|---|---|
| Tests | `make test` | FAIL: 1 failed, 41 passed, 2 skipped (1 skip added in range) |
| Migrations | read `migrations/007_*.sql` | pass with note: drops a column, not reversible |

**Bump:** major - config key `timeout` renamed to `timeout_ms` (confirmed by running)
**Release notes:**
<the notes>
**Rollback:** redeploy <old version>. Not undone by rollback: <what>
**Waiting for you:** <tag, push, publish - whichever was not requested>
```

## Rules

- **Results come from this session and this commit.** A CI badge or an
  earlier run is "not run here", with what it claimed.
- **Read the output, not the exit code.** A command that exits 0 while
  printing failures, or after running zero tests, is a FAIL.
- **Never drop** a breaking change, a security fix, a failed check or an
  irreversible migration from the report or the notes, and never invent a
  note: every line traces to a hunk in the range diff.
- **Report failures, do not fix them here.** If asked to fix, rerun every
  check afterwards: the commit changed.
- Never force-push, move or delete an existing tag, or amend a pushed commit.
