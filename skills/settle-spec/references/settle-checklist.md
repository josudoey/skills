# Three-Question Settle Gatekeeper Checklist

This checklist guides AI agents and engineers through evaluating active specifications during **Stage 3: Settle, Triage & Retention** across Blueprint-Driven Development (BDD Mode) and generic software repositories (Universal Mode).

---

## 1. Archetype Mode Resolution

Before evaluating the Three Questions, identify the active repository mode and configure target destinations:

- **Mode A: BDD Mode**
  - **Archetype Marker**: `docs/progress/` or `docs/blueprint/` exists in repository root.
  - **Specification Source**: `docs/progress/[blueprint-code]/[spec-file].md`.
  - **Settlement Destination**: `docs/reference/[domain].md`.
  - **Retirement Strategy**: Delete progress spec and prune empty parent slice directory (`docs/progress/[slice]/`).
- **Mode B: Universal Mode**
  - **Archetype Marker**: BDD directory markers are absent.
  - **Specification Source**: Discovered in `specs/`, `docs/specs/`, `docs/plans/`, or `.agents/specs/`.
  - **Settlement Destination**: Discovered reference document (`docs/architecture.md`, `docs/reference.md`) or project `README.md`.
  - **Retirement Strategy**: Archive to `[spec-dir]/archive/` or delete upon explicit user confirmation.

---

## 2. The Three-Question Evaluation Protocol

Before retiring or archiving any specification, run the following three evaluation filters:

### Q1: State Machines & Architectural Flows
- **Question**: *Does this specification contain Mermaid sequence diagrams, state machine flows, or cross-system protocol transitions not immediately obvious from reading raw code?*
- **Action**:
  - **YES**: Extract the diagrams and flow descriptions into living reference documentation (`docs/reference/[domain].md` in Mode A, or architecture doc / `README.md` in Mode B) under `## State Machines & Critical Flows`. Ensure Mermaid diagrams render cleanly and represent the current production reality.
  - **NO**: Skip flow extraction. Do not create redundant diagrams for trivial single-function calls or standard request handlers.

### Q2: Fault-Tolerance & Boundary Invariants
- **Question**: *Does this specification define critical fault-tolerance, offline degradation, retry compensation, quarantine recovery, or domain boundary invariants?*
- **Action**:
  - **YES**: Extract concise invariant rules into living reference documentation (`docs/reference/[domain].md` in Mode A, or architecture doc / `README.md` in Mode B) under `## Business Rules & Invariants` (or System Invariants). Use bold keys and structured lists rather than bloated tables.
  - **NO**: Skip invariant extraction if the business logic consists solely of standard CRUD validation handled by validation schemas.

### Q3: Code-as-Truth & Self-Explanatory Logic
- **Question**: *Can a future engineer or AI agent understand this mechanism entirely from the production code and automated tests?*
- **Action**:
  - **YES**: **Discard ephemeral details**. Explicitly exclude:
    - Standard API route/endpoint tables.
    - DTO request/response field lists and type definitions (production code is the single source of truth).
    - Database schema column dictionaries.
    - Step-by-step task checklists or work logs.
    - Temporary debugging notes or mock test payloads.
  - **NO**: If a concept cannot be understood from code, re-evaluate Q1/Q2 to articulate the missing invariant in living reference documentation.

---

## 3. Specification Type Triage Guide

Different specification archetypes have distinct retention profiles:

| Specification Archetype | Retention Profile | Settle Action |
| :--- | :--- | :--- |
| **Code-Alongside (`ui`, `handler`, `repo`)** | High Ephemerality | Code and automated tests are the truth. Verify Code Map in living reference points to implementation files and test suites, then retire or archive the spec file immediately. |
| **Vertical Slice (`feature`)** | Mixed (Flows + Endpoints) | Extract high-level interaction diagrams and core invariants to living reference documentation. Discard endpoint payload tables and component prop lists. Register primary entrypoints in Code Map, then retire or archive the spec. |
| **Architectural Mechanism (`mechanism`)** | High Architectural Value | Never retire prematurely. Cross-boundary state machines, protocol handshakes, and degradation policies must be 100% captured in living reference documentation before deletion or archiving. |

---

## 4. Settle Anti-Patterns to Reject

- ❌ **Compensatory DTO Duplication**: Copy-pasting TypeScript interfaces, Zod schemas, or DB table DDL into reference docs.
- ❌ **Zombie WIP Accumulation**: Leaving completed, passing specifications inside `docs/progress/` or active spec folders because "they might be useful later".
- ❌ **Unverified Retirement**: Retiring a progress spec when the corresponding code or automated tests were never implemented or committed.
- ❌ **Silent Deletions**: Deleting progress files without showing the user what was extracted and what is being removed.
- ❌ **Dangling Empty Directories**: Leaving empty slice folders (e.g. `docs/progress/1.1/`) after deleting the last specification in that directory (Mode A).
- ❌ **Unstructured Archive Clutter**: Dumping unverified or broken specifications into `archive/` without user confirmation (Mode B).
