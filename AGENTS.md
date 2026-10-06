# Project Directives & Governance

<!-- blueprint-workflow:start -->
## Development Workflow & Governance Directives
- **Workflow & Lifecycle**: Follow the Blueprint-Driven Development workflow defined in [docs/dev-workflow.md](docs/dev-workflow.md). You MUST read it before planning new features or refactoring.
- **Path-as-Status**: We follow the PARA documentation architecture. Documents in `docs/progress/` represent active WIP; never write manual status tags in file headers.
- **Code as Truth**: Production schemas, interfaces, DTOs, and automated tests are the single source of truth. Documentation never duplicates field lists or API payload tables.
- **Spec Immutability & Append-Only**: Delivered specifications are frozen historical records. Never modify completed specs retrospectively; add new revisions with incremented indices (`[NextIndex]-feature-...`).
<!-- blueprint-workflow:end -->

## Project Specific Standards
See [.agents/rules/skills-repository.md](.agents/rules/skills-repository.md) for skill directory structure, validation, and README guidelines.
