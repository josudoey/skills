# Project Directives & Governance

## 1. Core Principles (Non-Negotiable)

- **Path-as-Status**: We follow the PARA-based documentation architecture. The location of a document defines its lifecycle status. Never write manual status badges (e.g., `Status: Draft / Approved / In Progress`) inside document headers.
- **Stage Gate Isolation (No Premature Implementation)**: When tasked with Stage 1 (drafting/updating specs in `docs/progress/`), the ONLY authorized deliverable is the specification document. Never create implementation code, scripts, or modify catalogs in the same turn. Stop and await human review before proceeding to Stage 2.
- **Code as Truth**: Production schemas, interfaces, DTOs, and automated tests are the single source of truth for implementation reality. Never maintain duplicate field lists or API payload tables in markdown documentation.
- **Spec Immutability & Append-Only**: Delivered specifications (where code and tests are verified) are frozen historical facts. Never retrospectively rewrite completed specs. Requirements evolutions must be introduced as append-only revisions (`[NextIndex]-feature-...`).

## 2. On-Demand Governance Pointers

- **When planning new features, refactoring, or handling tasks**:
  You MUST read and follow [CONTRIBUTING.md](file://CONTRIBUTING.md) before writing implementation plans or code.
- **When organizing modules and dependencies**:
  Maintain strict unidirectional dependency flow (Shared/Domain Contracts ➔ Application Services ➔ Infrastructure & Presentation). Never introduce circular dependencies.
- **When testing and verifying**:
  Always anchor changes with corresponding automated tests (unit, contract, or integration) before declaring work complete.
