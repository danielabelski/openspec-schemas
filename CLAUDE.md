# CLAUDE.md

> Context for Claude Code when working in this repo. Write everything in American English.
>
> For what this repo is, why it exists, and which bridges it has, see [README.md](./README.md).
> This file focuses on the **conventions and red flags** Claude needs when working here.

---

## Structure

```
openspec-schemas/                     ← this repo
├── README.md                         ← GitHub's default render
├── CLAUDE.md                         ← what you are reading (for Claude)
├── LICENSE                           ← MIT
├── .gitignore
├── .github/workflows/
│   ├── validate-schemas.yml          ← CI runs openspec schema validate on each bridge
│   └── version-check.yml             ← weekly check of upstream OpenSpec / Superpowers; opens an issue when behind
├── docs/
│   ├── roadmap.md                    ← public roadmap
│   └── superpowers/
│       ├── specs/                    ← design specs (brainstorming output)
│       └── plans/                    ← implementation plans (writing-plans output)
└── superpowers-bridge/                ← the first bridge, a self-contained schema bundle
    ├── README.md                     ← full bridge documentation (install + integration runbook)
    ├── schema.yaml                   ← the schema definition OpenSpec reads
    └── templates/                    ← artifact templates
        ├── brainstorm.md
        ├── proposal.md
        ├── design.md
        ├── spec.md
        ├── tasks.md
        ├── plan.md
        ├── verify.md
        └── retrospective.md
```

Adding a bridge later: add a `<new-bridge>/` subdirectory at the repo root with the same structure as `superpowers-bridge/`. In CI, add one line to `matrix.bridge` in `.github/workflows/validate-schemas.yml`.

## Naming

- **Repo / directory / schema name**: lowercase + hyphen + the right number
  - repo: `openspec-schemas` (plural, can hold several bridges)
  - bridge dir / schema name: `superpowers-bridge` (singular)
  - no PascalCase (OpenSpec's own repo is `OpenSpec`, but its CLI and npm package are lowercase; we follow the functional naming)

## Language

Everything in this repo is written in American English: READMEs, this file, the roadmap, `schema.yaml`, `templates/*.md`, commit messages, and code comments. There are no translated copies to keep in sync.

## Changing a schema

1. Edit `<bridge>/schema.yaml` or `<bridge>/templates/*.md`
2. Validate locally:
   ```bash
   mkdir -p /tmp/test-project/openspec/schemas
   cp -R <bridge>/ /tmp/test-project/openspec/schemas/
   cd /tmp/test-project
   openspec schema validate <bridge-name>
   openspec schemas
   ```
3. If a timing mismatch or a behavior change is involved, **also update the "six design touchpoints worth remembering" section of `superpowers-bridge/README.md`** (especially the verify/retrospective timing mismatch).
4. Commit messages in English, following conventional commits (`feat:`, `fix:`, `refactor:`, `chore:`, `docs:`, `ci:`)
5. Pushing triggers CI

## How the three alfred-openspec concerns are addressed (keep in mind)

The PR #970 review raised three concerns, and this schema addresses them concretely in v1. Before changing any schema behavior in this repo, Claude must keep them in mind:

| Concern | Response |
|---------|----------|
| #3 Commits the user's git on its own | **Removed completely.** Step 0 became a skill PRECHECK that only checks skills and never touches git |
| #1 Tight coupling to Superpowers with no capability detection | **Layer 1**: every instruction that invokes a skill starts with a PRECHECK and STOPs when the skill is missing. **Layer 2**: verify / retrospective add evidence-based PRECHECKs (`git log`, `grep` on observable state) |
| #2 verify timing mismatch (and the same shape in retrospective) | Known limitation, documented as "design touchpoint #6" in the bridge README. The full fix waits for the OpenSpec engine to introduce a `post_apply` phase. The Layer 2 evidence-based PRECHECK is the current mitigation |

**Red flags when changing the schema** — **do not** do the following (it would undo the PR #970 responses):

- ❌ Write "run git add / git commit on your own" in an instruction
- ❌ Remove a PRECHECK without replacing it with something stronger
- ❌ Drop verify / retrospective from the artifacts without updating the limitation in the README's "design touchpoints" section
- ❌ Rename the schema without updating every document in the bridge and the bridge index in the top-level README

## Related links

- Design spec: [`docs/superpowers/specs/2026-05-02-openspec-schemas-monorepo-design.md`](./docs/superpowers/specs/2026-05-02-openspec-schemas-monorepo-design.md)
- Implementation plan: [`docs/superpowers/plans/2026-05-02-phase-1-implementation.md`](./docs/superpowers/plans/2026-05-02-phase-1-implementation.md)
- PR #970 review: <https://github.com/Fission-AI/OpenSpec/pull/970>
- Existing spec-kit superpowers bridges for reference:
  - [RbBtSn0w/spec-kit-extensions/superpowers-bridge](https://github.com/RbBtSn0w/spec-kit-extensions/tree/main/superpowers-bridge)
  - [WangX0111/superspec](https://github.com/WangX0111/superspec)
