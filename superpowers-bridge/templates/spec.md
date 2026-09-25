<!--
Delta spec template for a change.

This template shows the 4 delta sections; use the ones you need:
- ADDED / MODIFIED / REMOVED / RENAMED
File name and location: openspec/changes/<change-name>/specs/<capability>/spec.md
(`<capability>` matches the openspec/specs/<capability>/ directory name)

Hard format rules (validated by OpenSpec):
- A Requirement sentence MUST contain `SHALL` or `MUST`
- Every Requirement MUST have at least one `#### Scenario:`
- A Scenario MUST use level 4 (`####`); level 3 or a bullet fails silently
-->

## ADDED Requirements

<!-- New behavior. List the new Requirements this change adds to the capability. -->

### Requirement: <!-- requirement name -->
<!-- requirement text — must contain SHALL or MUST -->

#### Scenario: <!-- scenario name -->
- **WHEN** <!-- condition -->
- **THEN** <!-- expected outcome -->

---

## MODIFIED Requirements

<!--
Change an existing Requirement. **MUST use exactly the same normalized header as
openspec/specs/<capability>/spec.md** (compared case-sensitively after trimming);
otherwise applying the delta at archive fails because the requirement is not found.

**MUST paste the full modified content** (not only a diff), because OpenSpec
archive applies MODIFIED by replacing the whole text.
-->

### Requirement: <!-- the same header as in the existing spec -->
<!-- the full modified requirement text — must contain SHALL or MUST -->

#### Scenario: <!-- scenario name (may be added or modified) -->
- **WHEN** <!-- condition -->
- **THEN** <!-- expected outcome -->

---

## REMOVED Requirements

<!--
Remove an existing Requirement. MUST include Reason and Migration so the reviewer
understands why it is retired and how existing references should migrate.
-->

### Requirement: <!-- the header to remove, exactly as in the existing spec -->

**Reason**: <!-- why it is retired -->

**Migration**: <!-- how existing callers and dependents should adjust -->

---

## RENAMED Requirements

<!--
Rename a Requirement header. The format is fixed: FROM / TO with code-fenced headers.
If both the name and the content change, list the name change in RENAMED **and**
write the full content again in MODIFIED under the **new** header.

Apply order at archive: RENAMED → REMOVED → MODIFIED → ADDED
-->

- FROM: `### Requirement: <Old Name>`
- TO: `### Requirement: <New Name>`
