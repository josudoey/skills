# Project Directives & Governance

<!-- blueprint-workflow:start -->
## Development Workflow & Governance Directives
- **Workflow & Lifecycle**: Follow the Blueprint-Driven Development workflow defined in [docs/dev-workflow.md](docs/dev-workflow.md). You MUST read it before planning new features or refactoring.
- **Stage Gate Isolation (No Premature Implementation)**: When tasked with Stage 1 (drafting/updating specs in `docs/progress/`), the ONLY authorized deliverable is the specification document. You MUST NOT create implementation code, scripts, or modify catalogs in the same turn. After writing the spec, you MUST stop tools and await human review before proceeding to Stage 2.
- **Path-as-Status**: We follow the PARA documentation architecture. Documents in `docs/progress/` represent active WIP; never write manual status tags in file headers.
- **Code as Truth**: Production schemas, interfaces, DTOs, and automated tests are the single source of truth. Documentation never duplicates field lists or API payload tables.
- **Language Directive (English-Only Maintenance)**: All repository files—including blueprints, specifications in `docs/progress/`, living references in `docs/reference/`, rules, skill definitions (`SKILL.md`), scripts, code comments, and commit messages—MUST be authored and maintained exclusively in English. Even when user conversations or prompts occur in other languages, all committed files and documentation must strictly remain in English.
- **Spec Immutability & Append-Only**: Delivered specifications are frozen historical records. Never modify completed specs retrospectively; add new revisions with incremented indices (`[NextIndex]-feature-...`).
<!-- blueprint-workflow:end -->

## Project Specific Standards
See [.agents/rules/skills-repository.md](.agents/rules/skills-repository.md) for skill directory structure, design principles (Pure-Skill First), validation, and README guidelines.
