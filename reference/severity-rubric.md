# Severity and Verdict Rubric

Severity measures the effect of a report flaw on the reader's next decision.

General rule: a flaw the writer can resolve by supplying evidence or bounding
the claim produces `RETURN`; a flaw that requires a human to decide, contain,
authorize, recover, or act produces `ESCALATE`.

## STOP

The report could cause an unsafe, irreversible, externally visible, or
materially false decision.

Typical triggers:

- destructive action without authority or recovery evidence;
- exposed credentials or protected data;
- hidden production uncertainty;
- data loss or an unresolved exception dismissed as harmless;
- a material contradiction that creates an unsafe, external, or irreversible
  decision.

A `STOP` normally produces `ESCALATE`. If it is purely a reporting omission
that the writer can safely repair without a human decision, `RETURN` is allowed.
An exposed secret always produces `ESCALATE`; containment and rotation require
human ownership outside the report.

## PROVE

A material outcome may be true, but the report does not provide a receipt that
supports the same artifact, surface, environment, and time.

Typical triggers:

- “fixed” supported only by a build;
- “deployed” supported only by local checks;
- “all tests pass” without scope or denominator;
- a migration claim without reconciliation.
- a broad completion claim contradicted by a disclosed exception when the
  writer can repair it by bounding the claim and supplying the denominator.

Any unresolved `PROVE` finding produces `RETURN` unless a `STOP` requires
`ESCALATE`.

## CLARIFY

The facts may be present, but ambiguity prevents a safe or efficient handoff.

Typical triggers:

- missing owner or next action;
- relative or duplicate artifact paths;
- unstated local/staging/production boundary;
- vague verbs whose operational meaning changes the decision.

One minor `CLARIFY` can still merit `RETURN` when it blocks action. Otherwise,
use judgment and do not inflate it.

## Verdict mapping

- **ACCEPT** — no unresolved `STOP` or `PROVE`; the material claims are bounded,
  supported, and actionable.
- **RETURN** — the writer can make the report decision-ready by supplying
  missing support or resolving ambiguity.
- **ESCALATE** — a human must resolve authority, safety, production, privacy,
  destructive-action, or external-impact risk before the report can be
  accepted.

The verdict applies to the report, not the underlying implementation.
