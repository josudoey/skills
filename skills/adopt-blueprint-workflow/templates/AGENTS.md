# Project Directives & Governance

<!-- blueprint-workflow:start -->
## Development Workflow & Governance Directives
- **Workflow & Lifecycle**: Follow the Blueprint-Driven Development workflow defined in [CONTRIBUTING.md](CONTRIBUTING.md). You MUST read it before planning new features or refactoring.
- **Stage Gate Isolation (No Premature Implementation)**: When tasked with Stage 1 (drafting/updating specs in `docs/progress/`), the ONLY authorized deliverable is the specification document. You MUST NOT create implementation code, scripts, or modify catalogs in the same turn. After writing the spec, you MUST stop tools and await human review before proceeding to Stage 2.
- **Path-as-Status**: We follow the PARA documentation architecture. Documents in `docs/progress/` represent active WIP; never write manual status tags in file headers.
- **Code as Truth**: Production schemas, interfaces, DTOs, and automated tests are the single source of truth. Documentation never duplicates field lists or API payload tables.
- **Spec Immutability & Append-Only**: Delivered specifications are frozen historical records. Never modify completed specs retrospectively; add new revisions with incremented indices (`[NextIndex]-feature-...`).
<!-- blueprint-workflow:end -->

## Project Specific Standards
<!-- Place project-specific standards, build commands, and custom guidelines below this line -->

