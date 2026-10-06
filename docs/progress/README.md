# Active Project Specifications (`docs/progress/`)

## Purpose & Scope
This directory houses **in-flight project specifications and vertical slices** currently pending or actively being developed.

## Core Directives

### 1. Path-as-Status
- The directory location itself signifies active status.
- **Strictly prohibit explicit status fields** in file metadata (e.g., do not write `Status: Draft`, `Status: In Progress`, or `Status: Approved`).

### 2. Append-Only Indexing & Spec Immutability
- Specifications whose implementation and tests are complete represent immutable historical milestones. **Never retrospectively edit delivered specs**.
- Requirements revisions must be created under the next sequential index (e.g., if `1-feature-auth.md` is complete, create `2-feature-oauth-extension.md` to document the delta).

### 3. Settle & Cleanup
- When a specification is verified by automated tests:
  - Extract architectural trade-offs, business invariants, and Mermaid diagrams to `docs/reference/[domain].md`.
  - Update the `Code Map`.
  - Pass the **Settle Gatekeeper (Three-Question Test)** before removing ephemeral specs from this directory.

## File Organization & Naming (Symmetric Pragmatic WBS)

Subdirectories strictly mirror the parent Blueprint code (`[domain].[capability]`):
```
docs/progress/[blueprint-code]/[slice]-[layer]-[slug]-[type].md
```
*(No leading zeros: use `1.1`, `1.2`, `10.1`)*

*Examples*:
- `docs/progress/1.2/1-feature-stripe-terminal.md` (Vertical slice for Blueprint 1.2)
- `docs/progress/1.2/2-feature-offline-fallback.md` (Append-only slice for Blueprint 1.2)

### Preferred: Vertical Slice
- `[Slice]-feature-[slug].md`: End-to-end slice spanning schemas, backend logic, and frontend/CLI presentation (recommended for most feature work).

### Horizontal Layer Tokens (When Applicable)
- `data-type`: Domain schema, entity structures, DTO definitions.
- `contract`: API endpoints, request/response contracts, RPC signatures.
- `mechanism`: Cross-cutting protocols, synchronization, state machines.
- `handler`: Controller/handler logic.
- `repo`: Data access layer, persistence queries, DDL migrations.
- `ui`: Presentation components, state containers, interaction specs.
