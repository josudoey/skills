---
name: settle-spec
description: Formalize Stage 3 Specification Settlement in Blueprint-Driven Development. Evaluates the Three-Question Gatekeeper, synthesizes living reference updates and Code Navigation Maps, and safely retires progress specs without leaking ephemeral DTOs.
---

# Settle Specification Skill (`settle-spec`)

A portable, pure-cognitive workflow for AI coding agents and engineers to execute **Stage 3: Specification Settlement** across Blueprint-Driven Development (BDD) and universal software repositories.

This skill formalizes the **Three-Question Settle Gatekeeper**, extracts enduring architectural invariants and state flows into `docs/reference/` (or discovered project architecture documents), maintains canonical Code Navigation Maps, and safely settles and retires verified progress specifications without accumulating zombie WIP files or leaking ephemeral DTO duplicates.

```mermaid
flowchart TD
    Trigger["Trigger: /settle-spec [path?]"] --> Detect{"Workspace Archetype Detection"}
    
    Detect -- "Mode A: BDD (docs/progress/ exists)" --> SettleBDD["BDD Settlement\nExtract to docs/reference/[domain].md\nRetire from docs/progress/[code]/"]
    
    Detect -- "Mode B: Universal (Generic Repository)" --> SettleUni["Universal Settlement\nTarget: specs/, docs/specs/, or .agents/specs/\nExtract to README.md / docs/architecture.md\nArchive to specs/archive/ or delete"]
    
    SettleBDD --> Review["Interactive Review Card & Sign-Off"]
    SettleUni --> Review
    Review --> Execute["Atomic Settle & Git Conventional Commit"]
```

---

## When to Run This Skill

Activate this skill when:
- An implementation slice or feature has completed Stage 2 (code implemented, tests passing, acceptance criteria verified).
- Ready to settle architectural trade-offs, state machines, or invariants into `docs/reference/[domain].md` (Mode A) or project architecture docs / `README.md` (Mode B).
- Retiring active progress specifications in `docs/progress/` or archiving completed specs in `specs/archive/` while preventing "Knowledge Evaporation".
- Cleaning up completed WIP specifications to uphold the **Path-as-Status** standard.
- Updating living Code Navigation Maps to point to new canonical production files and test suites.

---

## System Invariants & Guardrails

> [!IMPORTANT]
> **Strict Governance Boundary**: The `settle-spec` skill operates exclusively on repository documentation artifacts (`docs/progress/` and `docs/reference/` in BDD mode, or discovered spec/reference paths in Universal mode). It **never** mutates, deletes, or modifies application source code, business data, or automated test files during settlement.

- **Adaptive Dual-Mode Operation**:
  - **Mode A (BDD Mode)**: Detected via `docs/progress/` or `docs/blueprint/`. Spec target: `docs/progress/[blueprint-code]/[Index]-feature-[slug].md`. Reference target: `docs/reference/[domain].md`. Spec retirement: file deletion and empty directory pruning.
  - **Mode B (Universal Mode)**: Detected when BDD markers are absent. Spec candidates discovered in `specs/`, `docs/specs/`, `docs/plans/`, or `.agents/specs/`. Reference target: discovered reference file (`docs/architecture.md`, `docs/reference.md`) or project `README.md`. Spec retirement: relocate to `[spec-dir]/archive/` or delete upon user confirmation.
- **The Three-Question Settle Gatekeeper**:
  1. **Q1 (Architectural & State Flows)**: *Does this specification contain Mermaid sequence diagrams, state machine flows, or cross-system protocol transitions not immediately obvious from reading raw code?*
     - If **YES**: Extract and synthesize into living reference documentation (`docs/reference/[domain].md` in Mode A, or architecture doc / `README.md` in Mode B).
  2. **Q2 (Fault-Tolerance & Boundary Rules)**: *Does this specification define critical fault-tolerance, offline degradation, retry compensation, quarantine recovery, or domain boundary invariants?*
     - If **YES**: Extract and synthesize into living reference documentation.
  3. **Q3 (Code-as-Truth & Self-Explanatory Logic)**: *Can a future engineer or AI agent understand this mechanism entirely from the production code and automated tests?*
     - If **YES**: **Discard ephemeral details**. Explicitly exclude standard API route tables, CRUD DTO field lists, and mock payloads. Production code is the single source of truth.
- **Interactive Human Confirmation**: Silent disk mutations are strictly prohibited. The proposed living reference changes and targeted file deletions or archives must be previewed and confirmed by the user before applying changes.
- **Pure-Skill First (Zero-Runtime Dependency)**: Designed strictly as a Markdown cognitive workflow (`SKILL.md`), executable in any environment without requiring Node.js, Python, or auxiliary CLI binaries.
- **Unidirectional Code Maps**: Navigation pointers are maintained unilaterally in `docs/reference/[domain].md` or project architecture references. Implementation source code and skills remain clean, pure, and decoupled from internal documentation paths.
- **English-Only Maintenance**: All synthesized reference documents, section headers, code map pointers, and git commit messages must be authored and maintained exclusively in English.

---

## Operational Role & Architectural Curation Stance

When executing this skill, adopt the persona of a **Minimalist Architectural Curator**:

- **Ruthless Pruning (Discard Ephemeral Trivia)**: Resist the temptation to preserve everything. Explicitly reject and discard API route tables, CRUD field dictionaries, and request/response payloads during synthesis. Production code and type declarations are the single source of truth (Code as Truth).
- **Invariance & Flow Extraction**: Focus exclusively on enduring knowledge: cross-system protocols, state machine transitions (Mermaid diagrams), boundary fault-tolerance rules, and canonical Code Navigation Maps.
- **Decisive WIP Retirement**: Treat progress specs as temporary scaffolding. Once verified code and tests exist and architectural invariants are settled, retire or archive the spec without hesitation or regret.
- **Living Spec Leanliness**: Keep living reference documentation clean, tight, and scannable (< 3,000 tokens per domain) to prevent agent context window inflation in future cycles.

---

## 5-Phase Cognitive Protocol

### Phase 1: Pre-flight Verification & Target Resolution

1. **Detect Workspace Archetype**:
   - Check if `docs/progress/` or `docs/blueprint/` exists $\rightarrow$ **Mode A (BDD Mode)**.
   - Otherwise $\rightarrow$ **Mode B (Universal Mode)**.
2. **Resolve Target Specification**:
   - If a target path is passed (e.g., `/settle-spec docs/progress/1.1/3-feature-settle-spec-skill.md` or `/settle-spec specs/1-feature-example.md`), verify the file exists via `view_file` or `list_dir`.
   - If triggered without arguments (zero-argument mode):
     - *Mode A*: Inspect `docs/progress/` for active markdown specifications (`*.md`), excluding `README.md`.
     - *Mode B*: Scan `specs/`, `docs/specs/`, `docs/plans/`, or `.agents/specs/` for active specifications (`*.md`).
     - Present an enumerated list of candidate in-flight specifications and prompt the user to pick one.
3. **Resolve Settlement Destination**:
   - *Mode A*: Map to `docs/reference/[domain].md` based on parent Blueprint code (e.g., `1.1` $\to$ `docs/reference/workflow-governance.md`).
   - *Mode B*: Map to existing living spec, `docs/architecture.md`, `docs/reference.md`, or project `README.md`.
4. **Verify Completion Proof**:
   - Inspect the specification's acceptance criteria and file mutation matrix.
   - Verify that corresponding production files and automated tests exist in the workspace.
   - Run a quick git status check (`git status --short`) to confirm there is no conflicting uncommitted scratch work in target areas.

### Phase 2: Three-Question Gatekeeper Evaluation

1. Inspect the target specification using bounded line-range reads.
2. Evaluate against the Three-Question Gatekeeper (see [settle-checklist.md](./references/settle-checklist.md)):
   - **Q1 Flow Extraction**: Itemize any Mermaid sequence diagrams, state machines, or protocol steps that capture non-obvious runtime behavior.
   - **Q2 Invariant Extraction**: Identify boundary rules, degradation policies, quarantine steps, or non-functional constraints.
   - **Q3 Ephemeral Elimination**: Filter out temporary checklists, implementation logs, request/response payload examples, and DTO field tables.
3. Map Target Domain Reference:
   - *Mode A*: Locate the corresponding living reference file under `docs/reference/` (e.g., `docs/reference/workflow-governance.md`). If no reference document exists for the domain, prepare to initialize one anchored to the upstream Blueprint.
   - *Mode B*: Locate project reference document (`docs/architecture.md`, `docs/reference.md`) or target the architectural overview in `README.md`.

### Phase 3: Living Reference & Code Map Synthesis

1. Read the target destination reference file.
2. Synthesize new content under standard living reference sections:
   - **System Invariants & Boundary Rules**: Add invariants extracted during Q2.
   - **State Machines & Critical Flows**: Insert sequence diagrams or state charts extracted during Q1.
   - **Code Navigation Map (Code Map)**: Register canonical paths to new production code, interfaces, configs, and automated test files (see [code-map-patterns.md](./references/code-map-patterns.md)).
3. Verify Code-as-Truth:
   - Confirm that zero duplicate DTO field lists, database column dictionaries, or API payload schemas are added to reference docs.

### Phase 4: Interactive Review & User Sign-Off

1. Present the **Settle Gatekeeper Review Card**:
   ```markdown
   ### 🧹 Settle Gatekeeper Report: `[target-spec-path]`

   #### 1. Archetype Mode & Destination
   - **Mode**: [Mode A (BDD) | Mode B (Universal)]
   - **Destination**: `docs/reference/[domain].md` or `[reference-file]` / `README.md`

   #### 2. Three-Question Evaluation
   - [x] **Q1 (State Machines & Flows)**: [Summary of extracted diagrams/flows, or "None"]
   - [x] **Q2 (Fault-Tolerance & Invariants)**: [Summary of extracted rules/invariants, or "None"]
   - [ ] **Q3 (Self-Explanatory Logic)**: [Summary of discarded ephemeral DTOs/checklists]

   #### 3. Target Reference Updates Preview
   ```markdown
   [Preview of synthesized sections]
   ```

   #### 4. Planned Cleanups
   - **Retire/Archive Spec**: `[target-spec-path]` (Mode A: Delete / Mode B: Move to `[spec-dir]/archive/` or delete)
   - **Prune Directory**: `docs/progress/[slice]/` (Mode A: if empty after retirement)

   👉 **Confirm Settlement?** [Proceed / Edit / Abort]
   ```
2. Await explicit human feedback or approval before making changes.

### Phase 5: Atomic Settle, Retirement & Commit Suggestion

1. Upon user approval:
   - Update destination reference document (`docs/reference/[domain].md` in Mode A, or discovered reference/`README.md` in Mode B) with the reviewed synthesis content.
   - Retire the completed specification:
     - **Mode A (BDD)**: Delete the retired progress specification file from `docs/progress/`. Check if the parent slice directory in `docs/progress/` is empty (or contains only empty subdirectories). If empty, remove the directory.
     - **Mode B (Universal)**: Move the completed specification to `specs/archive/` (or `.agents/specs/archive/`), or delete upon user confirmation.
2. Provide a standard Conventional Commit suggestion:
   ```bash
   git add docs/reference/ docs/progress/ # (Mode A)
   # or git add docs/ README.md specs/    # (Mode B)
   git commit -m "docs(workflow): settle [feature-name] into living reference"
   ```

---

## Detailed References

- [Three-Question Evaluation Checklist](./references/settle-checklist.md): Step-by-step triage guide for Q1, Q2, and Q3.
- [Code Map Design Patterns](./references/code-map-patterns.md): Rules for authoring and maintaining unidirectional Code Navigation Maps.
