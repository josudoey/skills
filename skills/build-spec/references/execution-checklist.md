# Stage 2 Checkpointed Execution Checklist

The **Stage 2 Checkpointed Execution Checklist** ensures deterministic execution, enforces zero scope creep via the File Mutation Matrix, and guarantees verifiable quality via automated Verification Oracles.

---

## 1. Phase 1: Target Resolution & Matrix Lock Checklist

Before touching any code or making disk edits, verify:
- [ ] **Target Specification Resolved**:
  - Direct path verified to exist (e.g., `docs/progress/[domain]/[spec].md`), or candidate spec selected from interactive discovery.
- [ ] **File Mutation Matrix Parsed & Locked**:
  - Explicitly list all `CREATE` targets.
  - Explicitly list all `MODIFY` targets.
  - Explicitly list all `DELETE` targets.
  - Explicitly record all `FORBIDDEN` patterns and paths.
- [ ] **Execution Sequence Extracted**:
  - Note sequential implementation steps (Types -> Logic -> Tests).
- [ ] **Verification Oracle Extracted**:
  - Exact test/lint CLI commands extracted from Section 6 of target spec.

---

## 2. Phase 2: Pre-Implementation Cleanliness Checklist

- [ ] Run `git status --short` to inspect working directory state.
- [ ] Compare dirty/untracked files against the parsed File Mutation Matrix:
  - If **no collisions**: Proceed safely.
  - If **collisions detected**: Pause and seek user confirmation before proceeding to avoid overwriting uncommitted work.

---

## 3. Phase 3: Sequential Implementation Checklist

- [ ] **Step 1: Types & Interfaces First**:
  - Declare data models, DTOs, interfaces, or YAML frontmatter before business logic.
- [ ] **Step 2: Core Logic & Handlers**:
  - Implement handlers, utilities, or cognitive workflows adhering to upstream contracts.
  - Maintain unidirectional code maps; avoid reverse pointers back to ephemeral specs.
- [ ] **Step 3: Accompanying Tests**:
  - Write unit, integration, or contract tests matching the feature slice.
- [ ] **Continuous Boundary Guard**:
  - Before every file modification or creation, verify the target path exists in the File Mutation Matrix.
  - If an unlisted file requires changes, **STOP** and propose an upstream spec amendment.

---

## 4. Phase 4: Automated Verification Oracle Checklist

- [ ] Execute all declared verification commands via CLI (e.g., `npm test`, `cargo test`, `npm run type-check`).
- [ ] Inspect exit codes:
  - If exit code is `0`: Verification passed.
  - If exit code is non-zero:
    - [ ] Enter bounded self-correction loop (attempt $\le 3$).
    - [ ] Inspect failure logs and apply localized fixes strictly within the Matrix.
    - [ ] Re-run verification commands.
    - [ ] If failing after 3 attempts, halt and report raw logs to user.

---

## 5. Phase 5: Stage 2 Completion Sign-off Checklist

- [ ] Verify 100% of modified files match the declared File Mutation Matrix.
- [ ] Verify all Verification Oracle commands completed with exit code 0.
- [ ] Output the standard Stage 2 Completion Proof card.
- [ ] Provide next-stage lifecycle recommendations:
  - `audit-workflow-fitness` (Workflow linting)
  - `gen-commit-message` (Staged commit generation)
  - `settle-spec [spec-path]` (Stage 3 reference settlement and WIP spec retirement)
