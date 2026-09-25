# Verification Report

> The `openspec-verify-change` skill produces this file after apply, to confirm the
> implementation is consistent with specs / design / tasks. A failed check goes back
> to the corresponding artifact for a fix, then verify runs again.

**Change**: `<change-name>`
**Verified at**: `YYYY-MM-DD HH:mm`
**Verifier**: `<who / which agent>`

---

## 1. Structural Validation (`openspec validate --all --json`)

- [ ] Every item is `"valid": true`

**Result**:

```text
<paste a summary of the openspec validate --all output>
```

If any item fails, list its id + issues:

| Item | Type | Issues |
|---|---|---|
| — | — | — |

---

## 2. Task Completion (`tasks.md`)

- [ ] Every `- [ ]` has become `- [x]`

**Incomplete tasks** (if any):

| Task | Why incomplete | Blocks archive? |
|---|---|---|
| — | — | — |

---

## 3. Delta Spec Sync State

Compare each capability directory under `openspec/changes/<name>/specs/` with
`openspec/specs/<capability>/spec.md`:

| Capability | Sync state | Notes |
|---|---|---|
| — | ✓ synced / ✗ pending sync / N/A | — |

---

## 4. Design / Specs Coherence Spot Check

Sample whether the decisions in `design.md` are reflected in the Requirements and
Scenarios of `specs/*.md`:

| Sample | Design says | Specs counterpart | Gap |
|---|---|---|---|
| — | — | — | — |

**Drift warnings** (non-blocking):

- <list them if any; otherwise write "none">

---

## 5. Implementation Signal

- [ ] No unstaged files in the worktree
- [ ] All related work is committed on the task branch (pushing is a separate, human-requested step)

**Commit range** (if known): `<from-sha>..<to-sha>`

---

## 6. Front-Door Routing Leak Detector (warning, non-blocking)

Design output must not land in `docs/superpowers/specs/` (the brainstorm artifact's
output redirection sends it to `openspec/changes/<name>/brainstorm.md`).

Detect:

```bash
ls docs/superpowers/specs/*.md 2>/dev/null
```

- [ ] No files, or the existing files are legitimate leftovers from before the schema was installed

**Leak list** (if any):

| File | Content already captured in the change? | Suggested action |
|---|---|---|
| — | — | — |

> Does not block archive. A leak produced by a new schema-installed cycle should be
> moved into `openspec/changes/<name>/brainstorm.md` or `design.md`, then the original deleted.

---

## 7. Deferred Manual Dogfood vs Automated Test Equivalence

For each manual dogfood / smoke task marked `[~]` deferred in plan.md, list the
equivalent automated test coverage. Without an equivalent automated test the item
is a **real gap**, not a reasonable deferral; record it under Misses in the retrospective.

| Deferred dogfood (plan §) | Equivalent automated test | Coverage assessment | Real gap? |
|---|---|---|---|
| e.g. §11.3 `compose up + curl /actuator/health` | `LinebcIntegrationApplicationTests` (Testcontainers, 24s) | Spring context boot + Flyway completes + main bean injection | ❌ covered equivalently |
| — | — | — | — |

> **Reading rules**:
> - "Equivalent" = the automated test's assertions are a superset of the manual dogfood's expected assertions
> - "Coverage assessment" = the layers actually exercised (context / DB schema / wiring / HTTP path / etc.)
> - A row with "real gap = ✅" still allows Overall Decision PASS, but needs a follow-up entry in the retrospective

> **When this section may stay empty**: when plan.md has no `[~]` row at all (empty means PASS).
> As soon as plan.md has any `[~]`, this section must list each one; otherwise Overall Decision drops to FAIL.

---

## Overall Decision

- [ ] ✅ PASS — may proceed to finishing-a-development-branch and archive
- [ ] ⚠️ PASS WITH WARNINGS — may proceed, but note: `<explanation>`
- [ ] ❌ FAIL — go back to the failing artifact, fix it, and run verify again

**Next step**:

<describe the next action>
