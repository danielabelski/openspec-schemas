# Retrospective: <change-name>

> Written: <YYYY-MM-DD> (after verify passed)
> Commit range: `<base-sha>..<head-sha>`
> Worktree: <path or "merged to main">

---

## 0. Evidence

> Quantified up-front data — the Wins / Misses bullets below cite it directly instead of
> repeating [evidence: ...] on every line. When written cold (some time after the cycle
> ended), this section should still be reconstructable from `git log` + `tasks.md` +
> commit messages alone.

- **Commit range**: `<base-sha>..<head-sha>` (<n> commits)
- **Diff size**: <+X / -Y lines across N files>
- **Tasks done**: <x>/<y> (`grep -cE '^\s*- \[x\]' tasks.md` → x; the regex allows indented sub-tasks)
- **Active hours**: <estimate>
- **Subagent dispatches**: <count or "n/a">
- **New external dependencies**: <list, with license + version, or "none">
- **Bugs encountered post-merge**: <count, one-line each, or "none">
- **OpenSpec validate state at archive**: <pass / fail / not-run>
- **Test coverage signal**: <e.g. jacoco %, pytest count, vitest count, or "n/a">

Commit chain (chronological):

```
<base-sha> <one-line summary>
...
<head-sha> <archive commit one-line>
```

---

## 1. Wins

- [evidence: <commit/file/test>] <description>

## 2. Misses

- 🔴 [blocking | evidence: ...] <description>
- 🟡 [painful  | evidence: ...] <description>
- 📌 [nit      | evidence: ...] <description>

## 3. Plan deviations

| Plan task | What changed | Why |
|-----------|--------------|-----|
| 1.2       | ...          | ... |

## 4. Skill / workflow compliance

| Skill                                            | Used |
|--------------------------------------------------|------|
| superpowers:brainstorming                        |      |
| superpowers:writing-plans                        |      |
| superpowers:using-git-worktrees                  |      |
| superpowers:subagent-driven-development          |      |
| (transitive) superpowers:test-driven-development |      |
| (transitive) superpowers:requesting-code-review  |      |
| superpowers:finishing-a-development-branch       |      |

> **Default expectation**: all ✓. Every skill is part of the schema's design;
> skipping one is an exception. Any ✗ must give its reason and prevention in the
> `### Deliberately Skipped Skills` subsection below.

### Deliberately Skipped Skills

> Skipping a skill is a designed escape hatch, not the normal path. Each ✗ must answer
> the three questions below; an empty section (all green) is the expected state.

- **`<skill name>`**
  - **What was skipped**: <the whole skill, or a specific sub-step>
  - **Why this cycle**: <the concrete cycle condition — no vague reasons such as "not needed" / "too small" / "no time" / "blocked by an external dependency" / "the skill output looked wrong"; name the actual trigger (a specific commit / log line / observed behavior)>
  - **How to prevent recurrence**: how does the next cycle avoid skipping under the same conditions? Pick one:
    - `schema graph fix` — name the exact part of schema.yaml to change
    - `skill description tightening` — name the exact skill frontmatter / instruction to change
    - `CLAUDE.md trigger` — name the exact rule to add to the adopter CLAUDE.md.fragment
    - `scope-judgment rule` — state how this cycle's scope should have been judged
    - `one-off — schema boundary case, no prevention possible` — but state explicitly why it is a boundary case (no vague reservations)

> **Relation to §6 Promote candidates**: when several cycles give the same `How to prevent`
> answer for the same skill, promote the pattern to §6 and open a schema / skill PR directly;
> never let it accumulate into the norm.

## 5. Surprises

- <assumption that turned out wrong>

## 6. Promote candidates → long-term learning

Each candidate is a `- [ ]` checklist item:

- Title: severity emoji (🔴/🟡/📌) + a one-sentence learning
- `→ **Promote to** <destination>`(memory / CLAUDE.md / schema / skill / one-off)
- A two-line body (matching the superpowers feedback memory body schema):
  - `> **Why**: <reason; often a past incident or strong preference>`
  - `> **How to apply**: <when/where this guidance kicks in>`

An unchecked `- [ ]` means the candidate is not promoted yet — carry it to the next
cycle's retro for re-evaluation, or keep it as a cross-cycle observation point.

> **Carry-forward**: when writing the next cycle's retro,
> `grep -A 5 '^- \[ \]' openspec/changes/archive/*/retrospective.md` lists earlier
> unchecked candidates; decide for each whether to carry it forward to this cycle's §6,
> promote it on the spot, or mark it stale and stop tracking it.

Example:

- [ ] 🔴 **<short rule>** → **Promote to memory** (type: feedback)
  > **Why**: <past incident or strong preference that motivated this rule>
  > **How to apply**: <which file / cycle phase / decision moment this kicks in>

- [ ] 🟡 **<another candidate>** → **Promote to project CLAUDE.md** (`<path/to/CLAUDE.md>` section)
  > **Why**: ...
  > **How to apply**: ...

- [ ] 📌 **<third candidate>** → **One-off** (record only, do not promote)
  > **Why**: <why it doesn't generalize>
