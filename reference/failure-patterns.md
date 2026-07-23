# Completion-Report Failure Patterns

Use these names to diagnose recurring editorial failures precisely. They are
cross-cutting patterns, not a second inventory of claim types; the canonical
claim inventory is `claim-evidence-matrix.md`, and any pattern can affect
multiple rows in that matrix.

## 1. Done Inflation

A partial result becomes “complete,” “fully fixed,” “end to end,” or “all”
without a denominator or boundary. Look for a broad headline supported by
narrow checks.

## 2. URL Alive Fallacy

Reachability is used to prove behavior. HTTP 200, DNS resolution, or a running
process cannot by itself prove a rendered page, authenticated workflow,
transaction, integration, or mobile interaction.

## 3. Green Check Fog

“Tests pass” appears without the command, suite, timing, denominator, exit
result, or relevance to the requested behavior.

## 4. Path-as-Proof

A filename, URL, PR number, commit, or screenshot label is presented as if its
mere existence proves content, correctness, currency, or deployment.

## 5. Receipt Mismatch

The evidence is real but tests the wrong artifact, surface, environment, or
time. Examples: local build for a production claim, API health for a UI flow,
or a pre-change test for a post-change result.

## 6. Scope Smuggling

Adjacent work appears inside the closeout without being requested, bounded, or
risk-assessed: “also cleaned up,” “while there, upgraded,” or “removed unused.”

## 7. Artifact Ambiguity

The report names “the app,” “config,” “database,” “final file,” or a relative
path where multiple targets or environments could exist.

## 8. Denominator Drop

Counts lack their comparison set. “12,000 migrated” says little without source,
destination, rejected, duplicate, or total counts. “All tests” has the same
failure.

## 9. Human Gate Erasure

A required approval, classification, physical check, credential step, review,
or business decision is concealed beneath a completion claim or dismissed as
obvious.

## 10. Risk Burial

Failures, skips, unknowns, or destructive side effects appear after “done,” in
parentheses, or under “notes” where the reader may miss their effect on the
verdict.

## 11. Verb Laundering

Vague verbs hide the actual operation: “handled,” “addressed,” “cleaned up,”
“updated,” “optimized,” or “verified.” Ask what object changed, what action
occurred, and what outcome was observed.

## 12. Secret-as-Receipt

A credential, token, private customer datum, or protected value is copied into
the report to prove access. The proof creates a new incident. Require redaction
without echoing the value, plus rotation when the exposed value is a
credential.

## 13. Self-Contradiction

The headline, receipts, boundary, or remaining-work section disagree. Examples:
“moved all records” beside “three rows skipped,” or “no further action” beside
an unresolved human approval.
