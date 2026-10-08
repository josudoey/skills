# Retire Development Workflow Stub Specification (2-feature-retire-dev-workflow-stub)

<!-- Ref: [Blueprint 1.1] §2, §4, §5 -->

## 1. Overview & Rationale

This specification defines the formal retirement and removal of the legacy `docs/dev-workflow.md` forwarding stub, transitioning `josudoey/skills` and downstream templates to treat the repository root **`CONTRIBUTING.md`** as the exclusive, canonical entrypoint for development workflow and governance.

### 1.1 Context & Problem Statement
- **Transitional Stub Redundancy**: During the workflow elevation in slice `1-feature-contributing-workflow` (Commit `743051b`), `docs/dev-workflow.md` was preserved as an 11-line relocation notice for temporary backwards compatibility.
- **Repository Cleanliness & Single Source of Truth**: With all internal governance directives (`AGENTS.md`, `README.md`, `.agents/rules/`) and external contributor paths fully adapted to `CONTRIBUTING.md`, maintaining a lingering stub file in `docs/` introduces redundant clutter and cognitive friction.
- **Alignment with Living Reference Invariants**: `docs/reference/workflow-governance.md` currently codifies Invariant 3.5 (*Universal Accessibility & Backward-Compatibility Invariant*), which mandates keeping the stub active. Retiring the stub requires officially completing the sunset period and revising the living reference invariant accordingly.

### 1.2 Target Objectives
- Remove `docs/dev-workflow.md` from the repository root documentation layout.
- Remove `skills/adopt-blueprint-workflow/templates/docs/dev-workflow.md` and update `skills/adopt-blueprint-workflow/SKILL.md` along with its references so newly adopted repositories deploy only `CONTRIBUTING.md`.
- Adjust `skills/audit-workflow-fitness/SKILL.md` to catalog `CONTRIBUTING.md` exclusively (retiring or marking fallback pointers as deprecated).
- Reconcile `docs/reference/workflow-governance.md` Section 2.5 and Section 3.5 to reflect the completed deprecation and sunset of the forwarding pointer.

---

## 2. Specification Architecture & Invariants

### 2.1 File Mutation Matrix (Stage 2 Execution Targets)

```text
/Users/joey/dev/skills/
├── docs/
│   ├── dev-workflow.md                                      <-- [DELETE] Redundant forwarding stub
│   └── reference/
│       └── workflow-governance.md                           <-- [MODIFY] Reconcile Invariant 3.5 & trade-offs
└── skills/
    ├── adopt-blueprint-workflow/
    │   ├── SKILL.md                                         <-- [MODIFY] Remove dev-workflow.md from layout
    │   ├── templates/docs/dev-workflow.md                   <-- [DELETE] Remove stub template
    │   └── references/bdd-workflow-guide.md                 <-- [MODIFY] Point resources to CONTRIBUTING.md
    └── audit-workflow-fitness/
        └── SKILL.md                                         <-- [MODIFY] Catalog CONTRIBUTING.md exclusively
```

### 2.2 Invariant Rules

- **Stage Gate Isolation Invariant (No Premature Implementation)**:
  - During Stage 1, only this specification file is committed. No files shall be deleted, updated, or modified until human review and sign-off are completed.
- **Path-as-Status Invariant**:
  - The specification status is determined exclusively by its residency in `docs/progress/1.1/`. No explicit status tags (`Status: Draft`, `Status: In Progress`) are permitted.
- **Zero Broken Links Invariant (`consistency/no-broken-relative-links`)**:
  - All markdown links pointing to `docs/dev-workflow.md` must be redirected to `CONTRIBUTING.md` or removed prior to/concurrently with the file deletion.
- **English-Only Maintenance Invariant**:
  - All specifications, comments, commit messages, and references must strictly remain in English.

---

## 3. Detailed Deprecation & Cleanup Scope

### 3.1 Retiring Repository Stub (`docs/dev-workflow.md`)
- Delete `docs/dev-workflow.md`.
- Ensure no lingering references in repository-level configurations or documentation.

### 3.2 Realigning Living Reference (`docs/reference/workflow-governance.md`)
- **Section 2 (Architectural Decisions & Trade-Offs)**:
  - Update Subsection 5 (*Canonical Root Contributor Engine*): Document that the backwards-compatible forwarding pointer at `docs/dev-workflow.md` has completed its transition window and is retired.
- **Section 3 (Business Rules & Invariants)**:
  - Update Subsection 3.5: Supersede the backward-compatibility requirement for `docs/dev-workflow.md` with standard canonical root resolution at `CONTRIBUTING.md`.
- **Section 5 (Code Navigation Map)**:
  - Remove `docs/dev-workflow.md` row if present.

### 3.3 Updating Skill Templates & Guides (`skills/adopt-blueprint-workflow/`)
- Delete `templates/docs/dev-workflow.md`.
- Update `skills/adopt-blueprint-workflow/SKILL.md`:
  - Update description to omit `dev-workflow.md`.
  - Update Section 1 (*Self-Contained Governance Layout*) and Section 4 (*Phases & Protocol* Phase 3 & 4) to eliminate the forwarding pointer file and deployment step.
- Update `skills/adopt-blueprint-workflow/references/bdd-workflow-guide.md`:
  - Update Table row under **Resources** from `docs/dev-workflow.md` to `CONTRIBUTING.md`.

### 3.4 Tuning Inspection Rules (`skills/audit-workflow-fitness/`)
- Update `skills/audit-workflow-fitness/SKILL.md`:
  - Line 83: Simplify workflow engine detection to `CONTRIBUTING.md` (or treat legacy `docs/dev-workflow.md` as an advisory migration finding).

---

## 4. Verification Criteria & Acceptance Tests

1. **Physical Deletion**:
   - `docs/dev-workflow.md` and `skills/adopt-blueprint-workflow/templates/docs/dev-workflow.md` do not exist in workspace.
2. **Zero Broken Links**:
   - Running full workspace search for `docs/dev-workflow.md` returns zero unresolved active links in living references or skill definitions.
3. **Audit Workflow Fitness**:
   - Execution of `audit-workflow-fitness` protocol passes with zero errors.
4. **Git Tree Cleanliness**:
   - All deletions and modifications cleanly committed adhering to Conventional Commits format (`refactor(workflow): retire dev-workflow forwarding stub`).
