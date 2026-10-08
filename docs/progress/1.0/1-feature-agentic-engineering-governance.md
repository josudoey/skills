# Agentic Engineering Governance Domain & Workflow Realignment Specification (1-feature-agentic-engineering-governance)

<!-- Ref: [Blueprint 1.0] §2, §3; [Blueprint 1.1] §2, §5 -->

## 1. Overview & Rationale

This specification defines the architectural separation of concerns between Domain 1's overarching vision and its concrete capabilities, realigning the blueprint layer and living reference layer to eliminate semantic drift and redundant metadata:

1. **Establish Domain Master Blueprint (`1.0_agentic-engineering-governance.md`)**:
   Elevate cross-capability principles—including the Strict Non-Invasive Safety Guardrail, Code as Truth, the Repository Self-Hosting Loop, and cognitive mitigation for AI Agent Attention Loss ("Lost in the Middle")—to a dedicated Domain 1 charter.
2. **Realign Capability 1.1 (`1.1_workflow-governance.md`)**:
   Rename and focus `1.1_adaptive-skill-bootstrap.md` to `1.1_workflow-governance.md`, eliminating the historical `skill-bootstrap` misnomer and achieving 1:1 symmetric parity with `docs/reference/workflow-governance.md`.
3. **Streamline Blueprint Metadata & Hygiene**:
   Remove non-essential metadata (`Target Applications / Modules`) across Domain 1 blueprints to reduce token overhead and match the established minimalist convention.

---

## 2. Specification Architecture & Invariants

### 2.1 Target File Placement Architecture

```text
docs/
├── blueprint/
│   ├── 1.0_agentic-engineering-governance.md   <-- [NEW] Domain Master Blueprint (Vision, Invariants, WBS)
│   ├── 1.1_workflow-governance.md              <-- [RENAME/SLIM] Realigned Capability Blueprint (was 1.1_adaptive-skill-bootstrap.md)
│   ├── 1.2_code-reference-integrity.md         <-- [MODIFY] Metadata hygiene (remove Target Applications / Modules)
│   └── README.md                               <-- [MODIFY] Catalog update (document 1.0 and 1.1 rename)
├── progress/
│   └── 1.0/
│       └── 1-feature-agentic-engineering-governance.md  <-- [ACTIVE SPEC] This specification
└── reference/
    └── workflow-governance.md                  <-- [MODIFY] Realink upstream blueprints to 1.0 & 1.1
```

### 2.2 System Invariants

- **Symmetric WBS Mirroring Invariant**:
  - Capability blueprints in `docs/blueprint/` and living specifications in `docs/reference/` must share identical domain slugs (e.g., `1.1_workflow-governance.md` $\longleftrightarrow$ `workflow-governance.md`, `1.2_code-reference-integrity.md` $\longleftrightarrow$ `code-reference-integrity.md`).
- **Domain Invariant Hoisting Invariant**:
  - System-wide invariant guardrails (Strict Non-Invasive Principle, Code as Truth, Self-Hosting Loop) belong to the Domain Master Blueprint (`1.0`) and must not be redundantly restated as localized novelties in sub-capability blueprints.
- **Stage Gate Isolation Invariant (No Premature Implementation)**:
  - This document represents Stage 1. No blueprint edits, renames, reference modifications, or catalog adjustments may occur until this specification receives explicit human review and approval.
- **Path-as-Status Invariant**:
  - The presence of this file within `docs/progress/1.0/` defines its active in-flight status. No manual status headers may be added.
- **English-Only Maintenance Invariant**:
  - All touched blueprints, references, and progress specifications must be authored strictly in English.

---

## 3. Structural Design of `docs/blueprint/1.0_agentic-engineering-governance.md`

The Domain Master Blueprint establishes the architectural north star for Domain 1:

1. **Metadata**:
   - `Blueprint Code`: `1.0`
   - `Date`: `2026-10-08`
2. **Strategic Vision & Problem Statement**:
   - The AI Agentic Paradigm Shift: Why static rules break down under agent execution (Agent Attention Degradation, "Lost in the Middle", Context Window Exhaustion).
   - Domain Strategic Objective: Modular, token-efficient, non-invasive governance infrastructure.
3. **Core Invariants & Safety Guardrails**:
   - **Strict Non-Invasive Principle**: Read-only diagnostics and governance file isolation (`docs/`, `AGENTS.md`, `.agents/`). Zero unilateral mutation of business code.
   - **Code as Truth**: Ground truth resides in typed interfaces and tests; no stale duplicate schemas in markdown.
   - **Repository Self-Hosting Loop**: `josudoey/skills` continuously governs itself through its own toolchain.
4. **Domain 1 Capability Landscape (WBS Map)**:
   - Full hierarchy linking `1.1 Workflow Governance`, `1.2 Code Reference Integrity`, `1.3 Progressive Context Loading`, and `1.4 Change & Commit Governance`.
5. **End-to-End Governance Value Stream**:
   - Mermaid diagram illustrating the complete development lifecycle from workflow setup through commit generation.

---

## 4. Realignment Design of `docs/blueprint/1.1_workflow-governance.md`

`docs/blueprint/1.1_adaptive-skill-bootstrap.md` will be moved to `docs/blueprint/1.1_workflow-governance.md` with the following scope refinements:

1. **Title & Header**:
   - Changed to `# Workflow Governance Product Blueprint`.
2. **Metadata Cleanup**:
   - Retain only `Blueprint Code: 1.1` and `Date: 2026-10-06`. Remove `Target Applications / Modules`.
3. **Capability-Level Focus (WHY & WHAT)**:
   - Problem: Inability of static development templates to dynamically scale between heavy BDD spec chains and lightweight agile workflows.
   - Solution: Adaptive mode generation, project topology profiling, workflow mutation, and continuous workflow drift detection.
4. **De-duplication**:
   - Reference the overarching non-invasive and self-hosting principles established in Blueprint 1.0 rather than defining them as isolated concepts.

---

## 5. Metadata Hygiene across Domain 1 Blueprints

To enforce clean, token-efficient metadata across all blueprints:
- **`docs/blueprint/1.1_workflow-governance.md`**: Remove `- **Target Applications / Modules**: ...`.
- **`docs/blueprint/1.2_code-reference-integrity.md`**: Remove `- **Target Applications / Modules**: ...`.

---

## 6. Affected Components & Stage 2 Execution Scope

### 6.1 Blueprint Additions & Renames
- Create `docs/blueprint/1.0_agentic-engineering-governance.md`.
- Move `docs/blueprint/1.1_adaptive-skill-bootstrap.md` $\to$ `docs/blueprint/1.1_workflow-governance.md`.
- Update `docs/blueprint/1.2_code-reference-integrity.md` metadata.
- Update `docs/blueprint/README.md` if blueprint listings are enumerated.

### 6.2 Reference Layer Link Updates
- `docs/reference/workflow-governance.md`:
  - Line 7: Update link from `1.1_adaptive-skill-bootstrap.md` to `1.1_workflow-governance.md`.
  - Line 113: Update upstream blueprint pointer in Code Navigation Map.
  - Add pointer to `1.0_agentic-engineering-governance.md` as domain upstream.

---

## 7. Verification Criteria & Acceptance Tests

1. **Zero Dead Links**:
   - Verify that ripgrep search for `adaptive-skill-bootstrap` across the entire workspace returns 0 occurrences:
     ```bash
     rg "adaptive-skill-bootstrap"
     ```
2. **Blueprint Symmetrical Naming Verification**:
   - `docs/blueprint/1.1_workflow-governance.md` matches `docs/reference/workflow-governance.md`.
   - `docs/blueprint/1.2_code-reference-integrity.md` matches `docs/reference/code-reference-integrity.md`.
3. **Workflow Fitness Audit Quality Gate**:
   - Execute the workflow fitness inspection to ensure all relative links resolve cleanly and no Path-as-Status or formatting violations are introduced.
4. **Language Compliance**:
   - All newly created or modified files pass the English-only invariant.
