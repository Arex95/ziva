# Contributing to ZIVA

ZIVA is in design. The most valuable contribution right now is argument, not
code: the architecture is being settled, and a decision questioned today costs
nothing to change.

## Before anything else

**Never put real health data in this repository.** Not in an issue, not in a
test fixture, not in a screenshot, not "anonymised". Use synthetic data. This is
the one rule with no exception and no escape hatch.

The same goes for credentials and API keys, including your own. If one lands in
a commit, say so immediately — rotating it is the fix, deleting the commit is
not.

## The Contributor Licence Agreement

Every code contribution requires signing the [CLA](./CLA.md). A bot asks you on
your first pull request; it takes one comment, and it applies to everything you
contribute afterwards.

You keep the copyright to your work. What the CLA grants is the right to
relicense the project as a whole — which keeps ZIVA from being frozen forever by
a contributor nobody can reach, and keeps the door open to funding it without
ever charging a family.

Issues, reviews and design discussion need no CLA.

## Scope: what ZIVA will not do

ZIVA's intended purpose is not medical, and that is a design constraint rather
than a legal footnote. A contribution that moves the product toward diagnosis,
treatment recommendation, dosing or triage will be declined regardless of how
well it is written.

| Belongs in ZIVA | Does not |
|---|---|
| Showing the user their own records | Telling them what condition they have |
| Explaining a term that appears in their own report | Interpreting an image, an ECG or a scan |
| Flagging a value against the reference range printed on that same report | Deciding that a value is dangerous |
| "You did not record the 8:00 dose" | "Skip today's dose" |
| Suggesting questions to ask a clinician | Deciding whether something is urgent |

If you think a feature sits on the line, open an issue before writing it. That
conversation is cheap and the rewrite is not.

## Working on a change

**Every change starts from an issue with acceptance criteria**, written before
the work and checkable by somebody who did not write the code. "Improve the
timeline" is not a criterion; "a medication whose schedule crosses midnight
produces two reminders, not one" is.

Check the state of the remote before you branch, and again before you push:

```bash
git fetch origin
git log --oneline main..origin/main   # commits you do not have
git log --oneline origin/main..main   # commits you have not pushed
```

Branch as `<type>/<issue>-<short-description>`:

```
feat/12-household-group-model
fix/31-reminder-duplicated-across-midnight
```

Types: `feat`, `fix`, `refactor`, `perf`, `test`, `docs`, `chore`, `ci`, `build`.

One branch carries one coherent group of changes. If the work reveals a second,
unrelated problem, note it and branch again.

**Stage by name.** `git add -A` and `git add .` sweep in whatever else is in the
working tree. Run `git status -s`, then add the paths you meant.

## Commits

```
<type>(<scope>): <subject, imperative, lowercase, no full stop>

<body: what changed and why, wrapped at 72 columns>

Closes #12
```

The subject states the change, not the file. The body explains **why** — the
diff already shows what, and the reason is the only thing nobody can reconstruct
a year later.

Documentation derived from a change goes in the **same commit** as the change.
Split apart, the two drift the first time a branch is reordered or abandoned.

If a change removes behaviour or changes what a value means, mark it: `!` after
the type and a `BREAKING CHANGE:` footer saying what stopped being true.

## Pull requests

```markdown
## What
One paragraph. The problem, not the diff.

## Approach
Why this way, and what was deliberately not done.

## Acceptance criteria
- [ ] Copied from the issue, each one checked

## Verification
What was run, and what was observed. Screenshots for interface changes.

Closes #12
```

A description that lists the files is not a description. An unticked criterion
blocks the merge — that is what it is for. And verification is evidence, not a
claim: "tested locally" is worth nothing, the command and its output are worth
something.

## Reporting a security problem

Do not open a public issue. See [SECURITY.md](./SECURITY.md) if present, or
contact the maintainer privately. A health record's defects are worth reporting
carefully.
