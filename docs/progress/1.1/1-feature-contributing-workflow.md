# Contributing Workflow Specification (1-feature-contributing-workflow)

<!-- Ref: [Blueprint 1.1] §2, §4, §5 -->

## 1. Overview & Rationale

This specification defines the migration of the repository's workflow governance engine from `docs/dev-workflow.md` to the repository root **`CONTRIBUTING.md`**, establishing Blueprint-Driven Development (BDD) as the official open-source contributor contract for `josudoey/skills`.

### 1.1 Context & Problem Statement
- **Open-Source Discoverability Barrier**: Currently, workflow rules reside at `docs/dev-workflow.md`. External contributors and automated GitHub bots do not automatically discover internal documentation paths when opening issues or pull requests.
- **Missing GitHub Community Standards Compliance**: GitHub natively checks for `./CONTRIBUTING.md` or `.github/CONTRIBUTING.md` to display automatic contributor warning banners and achieve 100% Community Profile health scores.
- **Alignment with Blueprint 1.1**: Blueprint 1.1 dictates adaptive workflow management and repository self-hosting. Elevating the workflow engine to a standard open-source entrypoint ensures the repository's governance is universally accessible to both external human contributors and autonomous AI agents.

### 1.2 Target Objectives
- Establish root **`CONTRIBUTING.md`** as the canonical single source of truth for repository workflow and contributor governance.
- Retain **`docs/dev-workflow.md`** as a lightweight backwards-compatible forwarding pointer to prevent broken links or external tool disruptions.
- Update repository pointers in `AGENTS.md`, `README.md`, and living references.
- Update `skills/audit-workflow-fitness` diagnostic cataloging to accept `CONTRIBUTING.md` as the primary workflow engine.

---

## 2. Specification Architecture & Invariants

### 2.1 File Placement Architecture
```text
/Users/joey/dev/skills/
├── CONTRIBUTING.md                  <-- [NEW] Canonical Workflow Engine & Contributor Guide
├── AGENTS.md                        <-- [MODIFY] Directives point to CONTRIBUTING.md
├── README.md                        <-- [MODIFY] Docs layout references CONTRIBUTING.md
├── docs/
│   ├── dev-workflow.md              <-- [MODIFY] Backwards-compatible forwarding pointer
│   ├── blueprint/                   <-- Long-term intent (WHY & WHAT)
│   ├── progress/                    <-- In-flight vertical slices (WIP)
│   └── reference/                   <-- Living specs & Code Navigation Maps
└── skills/
    ├── audit-workflow-fitness/      <-- [MODIFY] Audits CONTRIBUTING.md
    └── adopt-blueprint-workflow/    <-- [MODIFY] Supports CONTRIBUTING.md template
```

### 2.2 Invariant Rules

- **Universal Accessibility Invariant**:
  - The workflow engine must serve both human open-source contributors (via GitHub web UI and PR workflows) and AI agents (via `AGENTS.md` and context loaders) without semantic divergence.
- **Stage Gate Isolation Invariant (No Premature Implementation)**:
  - When contributing any feature or refactoring, the contributor/agent MUST draft an active specification under `docs/progress/` and receive approval before touching production code or skill definitions.
- **Backward-Compatibility Invariant**:
  - Existing scripts or historical references pointing to `docs/dev-workflow.md` must not hit a dead link (404/file not found). A forwarding pointer in `docs/dev-workflow.md` must guide users and agents to `../CONTRIBUTING.md`.
- **English-Only Maintenance Invariant**:
  - All sections of `CONTRIBUTING.md`, specifications, code comments, and git commit messages must be authored exclusively in English.

---

## 3. Structural Design of `CONTRIBUTING.md`

`CONTRIBUTING.md` must integrate the existing BDD governance rules with standard open-source ergonomics, organized as follows:

1. **Header & Welcoming Statement**:
   - Welcome contributors to `josudoey/skills`.
   - Brief statement of the repository's mission and engineering standards.
2. **Quick Contribution Flow (The 5-Step Cycle)**:
   - **Step 1: Discussion / Issue**: Open an issue or align on goals.
   - **Step 2: Stage 1 Specification**: Draft a vertical slice in `docs/progress/[blueprint-code]/[Index]-feature-[slug].md`.
   - **Step 3: Specification Review Gate**: Human approval required before implementation.
   - **Step 4: Stage 2 Implementation & Automated Verification**: Code, test, and pass `audit-workflow-fitness`.
   - **Step 5: Stage 3 Settle Protocol & Pull Request**: Settle invariants to `docs/reference/` and open PR.
3. **Documentation Architecture (Path-as-Status)**:
   - Detailed specification of `docs/blueprint/`, `docs/progress/`, `docs/reference/`, and Resources.
   - Reiteration of the **Strict Prohibition of Manual Status Badges/Headers** in file headers.
4. **Specification Chain & Invariant Guard**:
   - Unidirectional dependency chain: $\text{Mechanism} \to \text{Schemas/DTOs} \to \text{Contracts} \to \text{State} \to \text{Handlers/UI}$.
   - The Three Invariant Rules: *Strict Downstream Inheritance*, *Divergence Escalation*, and *Ghost Field Gatekeeper*.
5. **The Three-Stage Lifecycle & Settle Gatekeeper**:
   - Comprehensive rules for Stage 1, Stage 2, and Stage 3.
   - The Three-Question Test prior to removing completed progress specs.
6. **Code & Commit Hygiene**:
   - **Conventional Commits**: Angular style commit format (`feat: ...`, `fix: ...`, `docs: ...`).
   - **Clean Code Maps**: Unidirectional navigation pointers in `docs/reference/` instead of polluting source code with reverse comments.

---

## 4. Forwarding Pointer Design (`docs/dev-workflow.md`)

`docs/dev-workflow.md` will be condensed into a canonical redirection banner:

```markdown
# Development Workflow & Governance

> [!NOTE]
> **Relocation Notice**:
> The definitive development workflow and governance engine has been elevated to the repository root at **[`CONTRIBUTING.md`](../CONTRIBUTING.md)** to provide native GitHub open-source discoverability and unified contributor guidance.
>
> Please refer directly to **[`CONTRIBUTING.md`](../CONTRIBUTING.md)** for:
> - Documentation Architecture (Path-as-Status)
> - Specification Chain & Invariant Guard
> - Standard Three-Stage Lifecycle & Settle Gatekeeper
```

---

## 5. Affected Components & Stage 2 Execution Scope

### 5.1 Root Governance & Pointers
- **`CONTRIBUTING.md`**: Create new root document with complete BDD and open-source specifications.
- **`docs/dev-workflow.md`**: Replace with forwarding pointer.
- **`AGENTS.md`**: Update line 5 to point to `[CONTRIBUTING.md](CONTRIBUTING.md)`.
- **`README.md`**: Update documentation layout table and links.
- **`docs/reference/workflow-governance.md`**: Update Code Navigation Map and related references.

### 5.2 Tooling & Skills Adaptation
- **`skills/audit-workflow-fitness/SKILL.md`**:
  - Update Phase 1 cataloging: Inspect `CONTRIBUTING.md` (or fallback `docs/dev-workflow.md`).
  - Update `traceability/valid-blueprint-mapping` and link consistency rules.
- **`skills/adopt-blueprint-workflow/`**:
  - Add `templates/CONTRIBUTING.md` to templates directory.
  - Update Phase 3 and Phase 4 in `SKILL.md` to reference root `CONTRIBUTING.md`.

---

## 6. Verification Criteria & Acceptance Tests

1. **GitHub Discoverability**:
   - `CONTRIBUTING.md` exists at repository root and is valid Markdown.
2. **Link Resolution & Zero Broken Links**:
   - Relative links across `CONTRIBUTING.md`, `AGENTS.md`, `README.md`, and `docs/reference/` resolve to existing targets.
3. **Workflow Fitness Quality Gate**:
   - Running the workflow fitness inspection passes with zero `error` severity findings.
4. **Pointer Integrity**:
   - `docs/dev-workflow.md` clearly directs readers and tools to `../CONTRIBUTING.md`.
