# Claim–Evidence Matrix

Use this matrix to judge whether a report's receipt tests the same claim. It is
a minimum editorial standard, not a demand for full logs.

| Claim type | Minimum decision-ready receipt | Common non-proof |
|---|---|---|
| File or code changed | Exact path or artifact identity; bounded description of the change; diff, revision, or post-change inspection tied to that artifact | “Updated the files”; a path with no result; a commit hash with no scope |
| Bug fixed | Original failure condition; same user or system path exercised after the change; observed before/after outcome | Build succeeds; homepage returns 200; a different happy-path test passes |
| Tests pass | Exact command or named suite; when it ran; pass/fail/error denominator; exit result; relevant scope | “All green”; test file exists; prior run; linter used as functional proof |
| Service or site deployed | Target environment and artifact/revision; deploy result; post-deploy check on the requested surface; timestamp when identity could be ambiguous | Local build; DNS resolves; process is running; URL returns 200 for a UI-flow claim |
| Data migrated or transformed | Source/destination identity; source, inserted, rejected, duplicate, and destination counts; integrity checks; exception disposition; recovery posture | Script exit 0; “spot checks”; row count on only one side; skipped rows waved away |
| Configuration or permission changed | Exact setting location without secret values; intended before/after behavior; effective-state check; rollback path | Config file was edited; service restarted; credential value pasted as evidence |
| External action completed | Exact destination or audience; action identity; provider or target receipt; timestamp; required authorization | Draft exists; send button was clicked; link was generated; agent says “published” |
| Destructive action completed | Exact target; explicit authority; pre-action backup or recoverability; post-action target check; retention or restore route | “Cleaned up”; target was “old”; delete command exited 0 |
| Blocked or handed off | Blocking condition; what was tried; owner; next decision/action; artifact state; safe stopping point | “Waiting on user”; “mostly done”; no owner; next command with hidden prerequisites |
| Documentation or copy delivered | Exact artifact and path/link; requested sections present; render or consumer check when format matters | File exists; word count; source text without rendered inspection |

## Four alignment tests

A receipt supports a claim only when all four align:

1. **Artifact** — the checked object is the claimed object.
2. **Surface** — the check exercises the behavior named in the claim.
3. **Time** — the check occurred after the final relevant change.
4. **Environment** — the check ran where the claim says the result exists.

If one dimension is missing, identify it. Do not request “more evidence” in the
abstract.

## Proportionality

Receipt depth follows decision risk. A typo fix may need a diff and render. A
production migration needs parity, exception handling, and recoverability. Do
not burden low-risk claims with ceremony, and do not let high-confidence tone
lower the bar for high-risk claims.

