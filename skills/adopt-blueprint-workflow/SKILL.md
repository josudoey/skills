---
name: adopt-blueprint-workflow
description: Initialize or adapt a repository into an enterprise-grade Blueprint-Driven Development (BDD) workflow. Sets up self-contained docs/ (blueprint, progress, reference, dev-workflow.md) and lightweight AGENTS.md pointers with non-destructive brownfield adoption. Use when establishing development conventions, bootstrapping new projects, or upgrading existing codebases into structured living-spec governance.
---

# Adopt Blueprint Workflow

A portable, language-agnostic skill that establishes or upgrades a repository's engineering governance into the **Blueprint-Driven Development (BDD)** workflow.

This skill automates the setup of:
1. **Self-Contained `docs/` Layout**: `docs/blueprint/`, `docs/progress/`, `docs/reference/`, and `docs/dev-workflow.md`.
2. **Lightweight `AGENTS.md` Pointer**: Injects non-destructive pointers into the project root, keeping conversation tokens lean (< 45 lines) while enforcing strict invariant guardrails.
3. **Dual-Mode Compatibility**: Supports greenfield empty repositories and non-destructive brownfield adoption for existing codebases.

---

## When to Run This Skill

Activate this skill when:
- Bootstrapping a new repository and establishing Day-0 engineering conventions.
- Upgrading an existing codebase that suffers from outdated PRDs, context drift, or messy manual `TODO.md` / `progress.md` tracking.
- Aligning human teams and AI coding agents to a single source of truth without token bloat.
- Running a workflow audit (`check` mode) to verify repository documentation health.

---

## Execution Protocol

When the user runs `/adopt-blueprint-workflow` (or asks to set up/adopt the blueprint workflow), execute the following 5-phase procedure:

### Phase 1: Workspace & Ecosystem Inspection

1. **Check Project Root State**:
   - Check if the repository is empty (greenfield) or contains existing code (brownfield).
   - Check for pre-existing agent instruction files: `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, or `GEMINI.md`.
2. **Detect Polyglot Ecosystem & Topology**:
   - **Rust**: `Cargo.toml` (single crate or workspace)
   - **Go**: `go.work` or `go.mod`
   - **Python**: `pyproject.toml`, `poetry.lock`, `Pipfile`, or `requirements.txt`
   - **Node / TypeScript**: `pnpm-workspace.yaml`, `nx.json`, `package.json`
   - **JVM**: `settings.gradle(.kts)`, `pom.xml`
3. **Run Documentation Diagnostics**:
   - Check if `docs/progress.md` or root `TODO.md` exists (legacy manual tracking).
   - Check if markdown files in `docs/` contain manual status declarations (e.g., `Status: Draft`, `Status: In Progress`).

---

### Phase 2: Directory Scaffolding

Ensure the following directory structure exists in the target repository root:

```bash
docs/
├── blueprint/      # Long-term vision and business goals (frozen intent archive)
├── progress/       # Active in-flight slices and contract deltas (path-as-status)
└── reference/      # Living specifications, invariants, and code maps (Code as Truth)
```

For any directory created or lacking an explanatory guide, write the corresponding README:
- `docs/blueprint/README.md`: Sourced from [templates/docs/blueprint/README.md](file://templates/docs/blueprint/README.md).
- `docs/progress/README.md`: Sourced from [templates/docs/progress/README.md](file://templates/docs/progress/README.md).
- `docs/reference/README.md`: Sourced from [templates/docs/reference/README.md](file://templates/docs/reference/README.md).

*(If the directory already contains user files, preserve all existing files and do not overwrite unless instructed).*

---

### Phase 3: Workflow Document Deployment

Deploy or verify the definitive workflow specification at **`docs/dev-workflow.md`**:
- Sourced from [templates/docs/dev-workflow.md](file://templates/docs/dev-workflow.md).
- If `docs/dev-workflow.md` already exists, compare content. If updates are needed, prompt the user before modifying.

---

### Phase 4: `AGENTS.md` Pointer Configuration (Non-Destructive)

Configure the root `AGENTS.md` file using the **Two-Tier Pointer Pattern**:

#### Case A: Greenfield (No Existing `AGENTS.md`)
- Copy [templates/AGENTS.md](file://templates/AGENTS.md) directly to the root `AGENTS.md`.

#### Case B: Brownfield (Existing `AGENTS.md` Found)
- **STRICT NON-DESTRUCTIVE RULE**: Never overwrite pre-existing instructions, build commands, or test guidelines.
- Search for the marker block in the existing `AGENTS.md`:
  ```markdown
  <!-- blueprint-workflow:start -->
  ...
  <!-- blueprint-workflow:end -->
  ```
- **If the marker exists**: Update only the content between the start and end markers with the latest pointer directives.
- **If no marker exists**: Safely append the bounded block to the end of `AGENTS.md`:

```markdown

<!-- blueprint-workflow:start -->
## Development Workflow & Governance Directives
- **Workflow & Lifecycle**: Follow the Blueprint-Driven Development workflow defined in [docs/dev-workflow.md](file://docs/dev-workflow.md). You MUST read it before planning new features or refactoring.
- **Path-as-Status**: We follow the PARA documentation architecture. Documents in `docs/progress/` represent active WIP; never write manual status tags in file headers.
- **Code as Truth**: Production schemas, interfaces, DTOs, and automated tests are the single source of truth. Documentation never duplicates field lists or API payload tables.
- **Spec Immutability & Append-Only**: Delivered specifications are frozen historical records. Never modify completed specs retrospectively; add new revisions with incremented indices (`[NextIndex]-feature-...`).
<!-- blueprint-workflow:end -->
```

---

### Phase 5: Output Summary & Onboarding Guidance

Conclude execution by presenting a clean, structured summary card:

```markdown
### 🚀 Blueprint-Driven Development Workflow Configured

- **Mode**: [Greenfield Initialized | Brownfield Adopted]
- **Ecosystem Detected**: [e.g., TypeScript Monorepo (pnpm/nx) | Rust Workspace | Go | Python]
- **Document Structure**:
  - `docs/dev-workflow.md` (Workflow guide, Spec Chain Invariant, Settle Gatekeeper)
  - `docs/blueprint/` (Product vision & intent)
  - `docs/progress/` (Active vertical slices)
  - `docs/reference/` (Living specs & Code Maps)
- **Agent Directives**: Root `AGENTS.md` configured with non-destructive pointers.

#### Next Steps:
1. **Anchor Product Vision**: Create your first blueprint at `docs/blueprint/1.1_[feature-name].md`.
2. **Start First Vertical Slice**: When ready to implement, create `docs/progress/1.1/1-feature-[feature-name].md` spanning contract, logic, presentation, and tests.
3. **Verify Context Loader**: Use `/progressive-context-loader docs/dev-workflow.md` whenever an agent needs to align on development governance.
```

---

## References

- [Architectural Guide & BDD Whitepaper](./references/bdd-workflow-guide.md)
- [Workflow Guide Template](./templates/docs/dev-workflow.md)
- [Root Pointer Template](./templates/AGENTS.md)
