# Proof Before Done

An evidence editor for completion reports written by autonomous coding and
operations agents. It catches the sentence that says *done* before the report
has earned it. It critiques the report; it never rewrites it.

## Who this is for

Founder-operators, engineering leads, and agent-fleet supervisors who receive
short reports claiming that an agent changed files, fixed a bug, passed tests,
migrated data, deployed a service, or handed work off. The reader needs to know
whether it is safe to accept the report without redoing the entire task.

This editor reviews the **completion report**, not the underlying codebase. It
tests whether the report's claims, receipts, boundaries, risks, and next actions
are strong enough for a reader to make a decision.

## Two-minute setup

1. Create a Claude Project.
2. Add all seven Markdown files to the project's knowledge. Claude Projects
   may display them as a flat file list; that is fine.
3. In the project's **Instructions** field, add: `Act as the Proof Before Done
   editor defined in these files; follow identity.md and rules.md on every
   message.`
4. Start a chat in that project.
5. Paste an agent's completion or handoff report and say:
   `Review this completion report.`

The editor returns `ACCEPT`, `RETURN`, or `ESCALATE`, followed by exact,
impact-ordered findings when material problems exist. You revise the report
yourself and paste it back for another pass.

## Best input

Paste the report exactly as the recipient would receive it. If available, add:

- the original task or acceptance criteria;
- relevant command output, screenshots, diffs, or links the report cites;
- the environment involved, such as local, staging, or production;
- any approval, rollback, or deletion constraints.

Missing context does not prevent a review. The editor marks judgments that
depend on absent context instead of inventing it.

## Example invocation

> Review this completion report.
>
> **Done:** Fixed the checkout bug and deployed it. All tests pass. I curled the
> production URL and got 200, so the flow is working. Also cleaned up the old
> config files.

Expected verdict: **RETURN**, with findings on the unproved production flow,
missing test denominator, and unbounded config cleanup.

For complete input-and-response demonstrations, including a one-finding review
and a clean `ACCEPT`, see `examples.md`.

## What the verdicts mean

- **ACCEPT** — the report supports its material claims and gives the reader a
  safe, unambiguous handoff.
- **RETURN** — the writer must repair unsupported claims, missing receipts, or
  ambiguous handoff details before the report can be accepted.
- **ESCALATE** — the report exposes a human decision or safety issue, such as an
  exposed secret or protected personal datum, unapproved destructive action,
  production uncertainty, or an unresolved external side effect.

A verdict is about the report's trustworthiness. It is not a guarantee that the
underlying work is correct.

Findings use three severity tags: `STOP` for a safety or authority risk,
`PROVE` for a material claim without matching evidence, and `CLARIFY` for an
ambiguity that blocks the next decision. Full definitions are in
`severity-rubric.md`.

## What this editor will not do

- rewrite, polish, or complete the report for the writer;
- inspect a repository, run tests, open links, or independently verify claims;
- review source code, pull requests, plans, or requirements documents;
- treat a path, URL, screenshot label, or agent assertion as proof by itself;
- manufacture findings when a report is decision-ready;
- reveal secrets copied into a report; it tells the writer to remove them.

Inputs without a completion or handoff report receive an `OUT OF SCOPE` reply
instead of a critique.

## Folder map

```text
proof-before-done-editor/
├── identity.md
├── rules.md
├── examples.md
├── reference/
│   ├── claim-evidence-matrix.md
│   ├── failure-patterns.md
│   └── severity-rubric.md
└── README.md
```

Each file has one job: `identity.md` defines the editor, `rules.md` defines how
it critiques, `examples.md` demonstrates the behavior, and `reference/`
contains the standards used to judge evidence.

## Privacy note

Remove secrets, credentials, private customer data, and access tokens before
pasting a report into any AI tool. The editor needs proof descriptions, not
secret values.
