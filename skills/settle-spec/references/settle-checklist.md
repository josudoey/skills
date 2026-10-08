# Three-Question Settle Gatekeeper Checklist

This checklist guides the AI agent and engineers through evaluating active specifications in `docs/progress/` during **Stage 3: Settle, Triage & Retention** of the Blueprint-Driven Development lifecycle.

---

## 1. The Three-Question Evaluation Protocol

Before retiring any specification from `docs/progress/`, run the following three evaluation filters:

### Q1: State Machines & Architectural Flows
- **Question**: *Does this specification contain Mermaid sequence diagrams, state machine flows, or cross-system protocol transitions not immediately obvious from reading raw code?*
- **Action**:
  - **YES**: Extract the diagrams and flow descriptions into `docs/reference/[domain].md` under `## 4. State Machines & Critical Flows`. Ensure Mermaid diagrams render cleanly and represent the current production reality.
  - **NO**: Skip flow extraction. Do not create redundant diagrams for trivial single-function calls or standard request handlers.

### Q2: Fault-Tolerance & Boundary Invariants
- **Question**: *Does this specification define critical fault-tolerance, offline degradation, retry compensation, quarantine recovery, or domain boundary invariants?*
- **Action**:
  - **YES**: Extract concise invariant rules into `docs/reference/[domain].md` under `## 3. Business Rules & Invariants`. Use bold keys and structured lists rather than bloated tables.
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
  - **NO**: If a concept cannot be understood from code, re-evaluate Q1/Q2 to articulate the missing invariant in `docs/reference/[domain].md`.

---

## 2. Specification Type Triage Guide

Different specification archetypes have distinct retention profiles:

| Specification Archetype | Retention Profile | Settle Action |
| :--- | :--- | :--- |
| **Code-Alongside (`ui`, `handler`, `repo`)** | High Ephemerality | Code and automated tests are the truth. Verify Code Map in `docs/reference/` points to implementation files and test suites, then retire the progress file immediately. |
| **Vertical Slice (`feature`)** | Mixed (Flows + Endpoints) | Extract high-level interaction diagrams and core invariants to `docs/reference/[domain].md`. Discard endpoint payload tables and component prop lists. Register primary entrypoints in Code Map, then retire the progress file. |
| **Architectural Mechanism (`mechanism`)** | High Architectural Value | Never retire prematurely. Cross-boundary state machines, protocol handshakes, and degradation policies must be 100% captured in `docs/reference/` before deletion. |

---

## 3. Settle Anti-Patterns to Reject

- ❌ **Compensatory DTO Duplication**: Copy-pasting TypeScript interfaces, Zod schemas, or DB table DDL into reference docs.
- ❌ **Zombie WIP Accumulation**: Leaving completed, passing specifications inside `docs/progress/` because "they might be useful later".
- ❌ **Unverified Retirement**: Retiring a progress spec when the corresponding code or automated tests were never implemented or committed.
- ❌ **Silent Deletions**: Deleting progress files without showing the user what was extracted and what is being removed.
- ❌ **Dangling Empty Directories**: Leaving empty slice folders (e.g. `docs/progress/1.1/`) after deleting the last specification in that directory.
