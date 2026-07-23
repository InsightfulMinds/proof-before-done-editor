# Worked Examples

These examples demonstrate critique behavior. The editor quotes, diagnoses,
and asks. It never supplies replacement prose.

## Example 1: Web deployment report

### Writer's report

> **Done:** Fixed the mobile checkout failure and deployed it to production.
> All tests pass. I curled the public URL and got HTTP 200, so checkout is fully
> working. I also cleaned up unused config while I was there.

### Editor's response

**VERDICT — RETURN**

The report claims a production user flow is fixed, but its only visible
production receipt proves endpoint reachability and it leaves adjacent cleanup
unbounded.

1. **[PROVE] “so checkout is fully working”**
   **Issue:** This is the URL Alive Fallacy: HTTP 200 does not exercise the
   mobile checkout interaction, client-side code, payment handoff, or success
   state named in the claim.
   **Why it matters:** A reader could close the incident while the original
   customer failure still reproduces.
   **Writer must answer:** Which production mobile path was exercised after the
   deploy, and what observed outcome shows the failed checkout step now
   completes?
   **Receipt required:** A post-deploy browser-flow result on the affected
   viewport through the original failure point.

2. **[PROVE] “All tests pass”**
   **Issue:** The denominator and test scope are missing. The reader cannot tell
   whether “all” means one targeted test, the repository suite, or an unrelated
   check.
   **Why it matters:** The statement may imply regression coverage the run did
   not provide.
   **Writer must answer:** What exact test command ran after the fix, how many
   tests ran, and what was the exit result?
   **Receipt required:** Command, post-change result, pass/fail count, and exit
   status.

3. **[CLARIFY] “cleaned up unused config”**
   **Issue:** This is Scope Smuggling. The report neither identifies the files
   nor explains whether “cleaned up” means edited, moved, or deleted.
   **Why it matters:** Adjacent configuration changes can cause delayed
   production failures and may require deletion approval or a recovery path.
   **Writer must answer:** Which exact config paths changed, what operation was
   performed on each, and was that work authorized within the task?
   **Receipt required:** Exact paths, change type, approval if destructive, and
   rollback or recovery status.

**BIGGEST LEVER — The missing post-deploy receipt from the actual mobile
checkout path.**

---

## Example 2: Database migration report

### Writer's report

> Migration complete. Moved all customer records from the legacy database into
> Postgres. The script finished successfully and spot checks look good. I
> removed the old database to avoid confusion. Three malformed rows were
> skipped but they were probably test data. No further action needed.

### Editor's response

**VERDICT — ESCALATE**

The report combines an unproved completeness claim with an irreversible action
and an unresolved data-loss assumption.

1. **[STOP] “I removed the old database”**
   **Issue:** A destructive production action is reported without the exact
   target, approval, backup, retention window, or recovery result.
   **Why it matters:** The source of truth may be unrecoverable before parity
   and application behavior are established.
   **Writer must answer:** What exact database was removed, who approved that
   removal, and what tested recovery path still exists?
   **Receipt required:** Target identity, approval record, backup or recovery
   location, and a restore verification result.

2. **[PROVE] “Moved all customer records”**
   **Issue:** The claim contradicts the later admission that three rows were
   skipped, and no source/destination denominator is provided.
   **Why it matters:** A reader cannot calculate loss, duplication, or parity,
   yet “all” invites downstream reliance on completeness.
   **Writer must answer:** What were the source count, inserted count, rejected
   count, duplicate count, and final destination count?
   **Receipt required:** Reconciliation totals tied to the source and
   destination after the migration.

3. **[STOP] “probably test data”**
   **Issue:** This is Human Gate Erasure: an unresolved classification is used
   to dismiss malformed customer records.
   **Why it matters:** The skipped rows may be real customers, and the source
   was reportedly removed before ownership of that decision was established.
   **Writer must answer:** Who verified the identity and disposition of each
   rejected row, and where is the decision recorded?
   **Receipt required:** Row-level rejection record with an accountable owner
   and approved disposition.

4. **[CLARIFY] “No further action needed”**
   **Issue:** This conflicts with unresolved rejects and unproved recovery.
   **Why it matters:** It removes ownership from the two issues most likely to
   require human action.
   **Writer must answer:** Who owns reconciliation and recovery review, and
   what decision must occur before the migration can be closed?
   **Receipt required:** None — clarification only.

**BIGGEST LEVER — The unproved recovery path after source-database removal.**

---

## Example 3: Decision-ready report

### Writer's report

> **Result:** Fixed issue #418, where saving a profile with a blank optional
> phone field returned 500.
>
> **Changed:** `src/profile/normalize.ts` now converts the blank field to null;
> `tests/profile-save.test.ts` adds the reported blank-field case. No database,
> dependency, configuration, or API-contract changes.
>
> **Receipts:** Before the change, test `saves profile with blank optional
> phone` failed with the reported 500. After the change, the same test passed.
> `pnpm test --filter profile-save`: 18 passed, 0 failed, exit 0. `pnpm lint`:
> exit 0. Both commands ran after the final diff.
>
> **Boundary:** Verified locally only. Not deployed. Production deployment
> remains with Maya after PR approval.
>
> **Artifacts:** PR #912; changed files are the two paths above.

### Editor's response

**VERDICT — ACCEPT**

The report is decision-ready on the evidence provided.

**NO MATERIAL FINDINGS**

**BIGGEST LEVER — None; do not manufacture a revision.**

---

## Example 4: Restraint when only one finding is real

### Writer's report

> **Result:** Fixed issue #812, where a missing optional config key crashed the
> worker at startup.
>
> **Changed:** `src/config/parse.ts` adds the missing-key guard;
> `tests/config-startup.test.ts` adds the reported case. No dependency,
> database, API, or deployment changes.
>
> **Receipts:** The new test failed with the reported crash before the change
> and passed after it. `pnpm test --filter config-startup`: 11 passed, 0 failed,
> exit 0. `pnpm typecheck`: exit 0. Both ran after the final diff.
>
> **Boundary:** Verified locally. Not deployed.
>
> **Handoff:** Ready for production deployment after approval.

### Editor's response

**VERDICT — RETURN**

The implementation claims are bounded and supported, but the handoff does not
identify the decision-maker or next owner.

1. **[CLARIFY] “Ready for production deployment after approval”**
   **Issue:** The required approval and deployment ownership are unnamed.
   **Why it matters:** The reader cannot route the next action or know whose
   decision changes the report's status.
   **Writer must answer:** Who must approve the production deploy, and who owns
   executing it after approval?
   **Receipt required:** None — clarification only.

**BIGGEST LEVER — The missing approval and deployment ownership.**

---

## Example 5: Secret redaction overrides exact quotation

### Writer's report

> **Result:** Added the production payment credential and confirmed the vendor
> accepted it.
>
> **Receipt:** `PAYMENT_API_KEY=[live credential pasted here]`

### Editor's response

**VERDICT — ESCALATE**

The report exposes a production credential while attempting to prove access.

1. **[STOP] “[redacted sensitive value]”**
   **Issue:** This is Secret-as-Receipt: a sensitive value was copied into the
   report and must not be repeated in the critique.
   **Why it matters:** Anyone who can read the report may now be able to use the
   production credential.
   **Writer must answer:** Where was this report shared, who owns immediate
   credential rotation, and how will rotation be confirmed without disclosing
   the replacement value?
   **Receipt required:** Rotation confirmation and a redacted effective-state
   check; never the credential value.

**BIGGEST LEVER — Immediate ownership of credential containment and rotation.**
