# Agent Skills

A collection of AI coding agent skills compatible with the [Skills](https://skills.sh/) CLI ecosystem (`npx skills`).

These skills support major AI coding assistants and agents including **Antigravity**, **Claude Code**, **Cursor**, **GitHub Copilot**, **Windsurf**, and more.

## Available Skills

- **[`adopt-blueprint-workflow`](./skills/adopt-blueprint-workflow)**: Initialize or adapt a repository into an enterprise-grade Blueprint-Driven Development (BDD) workflow with self-contained `docs/` and lightweight `AGENTS.md` pointers.
- **[`audit-stale-ref`](./skills/audit-stale-ref)**: Audit code comments for dead file paths, broken symbol pointers, and reverse documentation coupling with a read-only diagnostic engine.
- **[`audit-workflow-fitness`](./skills/audit-workflow-fitness)**: Audit and evaluate project development workflows, markdown governance, and spec fitness with a token-guarded diagnostic engine.
- **[`gen-commit-message`](./skills/gen-commit-message)**: Generate Angular-style Git commit messages in English based on staged changes.
- **[`progressive-context-loader`](./skills/progressive-context-loader)**: Load codebase context progressively using a 5-level pyramid (WHY -> WHAT -> HOW -> CONVENTION -> IMPLEMENT) to prevent context blow-up and enforce engineering guardrails.
- **[`settle-spec`](./skills/settle-spec)**: Formalize Stage 3 Specification Settlement in Blueprint-Driven Development, enforcing the Three-Question Gatekeeper and maintaining Code Navigation Maps.

---

## Installation & Usage

### Gemini CLI (`gemini skills`)

Install skills directly using the `gemini` CLI:

```bash
# Install from a local path
gemini skills install ~/.agents/skills/gen-commit-message

# Install from local repository folder
gemini skills install ./skills/gen-commit-message

# Install from GitHub repository (requires --path for subdirectories)
gemini skills install https://github.com/josudoey/skills --path skills/gen-commit-message

# Install to workspace scope (default is user/global)
gemini skills install ~/.agents/skills/gen-commit-message --scope workspace

# Link for local development (changes reflect immediately)
gemini skills link ./skills/gen-commit-message
```

### `npx skills` CLI

Install skills into your agents using `npx skills`:

#### Install to Project (Local)

```bash
# Add all skills from this repository
npx skills add josudoey/skills

# Or install a specific skill
npx skills add josudoey/skills --skill gen-commit-message
```

#### Install Globally (User-level)

```bash
# Install globally across supported agents
npx skills add josudoey/skills -g

# Or specific skill globally
npx skills add josudoey/skills --skill gen-commit-message -g
```

#### Install via GitHub URL

```bash
npx skills add https://github.com/josudoey/skills

# Or direct subfolder URL
npx skills add https://github.com/josudoey/skills/tree/main/skills/gen-commit-message
```

#### List Available Skills in Repository

```bash
npx skills add josudoey/skills -l
```

#### One-off Usage (Without installing)

```bash
npx skills use josudoey/skills@gen-commit-message
```

---

## Skill Details

### `adopt-blueprint-workflow`

- **Description**: Bootstraps or upgrades any software repository (polyglot: Rust, Go, Python, TypeScript, Java, etc.) into an enterprise-grade Blueprint-Driven Development (BDD) engineering workflow.
- **Key Features**:
  - **Self-Contained `docs/` Layout**: Standardizes `docs/blueprint/` (frozen product intent), `docs/progress/` (active vertical slices), `docs/reference/` (living specifications & code maps), and `CONTRIBUTING.md` (the canonical lifecycle guide and contributor contract).
  - **Lightweight Pointer Pattern**: Maintains an ultra-lean root `AGENTS.md` (< 45 lines) directing AI agents to load workflow details on-demand, preventing context window bloat.
  - **Spec Immutability & Settle Gatekeeper**: Enforces append-only feature revision and structured knowledge settlement before ephemeral WIP specs are deleted.
  - **Dual-Mode Greenfield / Brownfield**: Safely adopts existing codebases using bounded marker blocks (`<!-- blueprint-workflow:start -->`), preserving 100% of pre-existing commands and instructions.

### `audit-workflow-fitness`

- **Description**: Evaluates and inspects project development workflows, markdown governance, and specification fitness using an ESLint-style diagnostic engine with strict Quality Gates (`PASSED` vs `BLOCKED`).
- **Key Features**:
  - **4-Dimensional Rule Engine**: Covers `consistency` (no manual status tags, valid relative links), `friction` (max token overhead, no bloated schema tables), `truth` (no duplicate API dictionaries, code as truth), and `traceability` (valid Code Maps and blueprint mappings).
  - **Binary Quality Gate**: Eliminates compensatory composite score fallacies; any `error` immediately blocks the gate, while `warn` flags advisories.
  - **Token-Guarded Inspection Protocol**: Employs metadata-first inspection with byte-to-token ratio estimation and UNIX silence, keeping diagnostic context overhead $< 2,000$ tokens.
  - **Pure-Skill Portability**: Built as a pure cognitive Markdown engine (`SKILL.md`) with zero scripts and zero runtime dependencies.

### `gen-commit-message`

- **Description**: Inspects git staged changes via `scripts/get-staged-diff.sh` and crafts Angular commit convention compliant messages (`<type>(<scope>): <subject>`).
- **Rules**:
  - Format: `<type>(<scope>): <subject>`
  - English only, imperative mood, lowercase, no ending period, ≤ 100 characters.
  - Read-only analysis: only inspects staged changes without mutating git state or committing.

### `progressive-context-loader`

- **Description**: Guides coding agents through a structured, 5-level retrieval pyramid (`WHY -> WHAT -> HOW -> CONVENTION -> IMPLEMENT`) to build accurate context with minimal token usage.
- **Key Features**:
  - **Context Pyramid**: Level 1 (WHY: Intent) ➔ Level 2 (WHAT: Domain Rules) ➔ Level 3 (HOW: Contracts & Code as Truth) ➔ Level 4 (CONVENTION: Targeted Engineering Guardrails) ➔ Level 5 (IMPLEMENT: Slices & Tests).
  - **Convention Guardrails**: Automatically routes to specific naming, framework, and error handling conventions based on the change layer.
  - **Token Discipline**: Keeps overall context retrieval tightly budgeted (< 6,000 ~ 8,000 tokens) using slice reading and interface-first discovery.
  - **Context Summary Card**: Outputs a concise summary card before implementation begins.

### `settle-spec`

- **Description**: Formalizes Stage 3 Specification Settlement in Blueprint-Driven Development (BDD). Evaluates the Three-Question Settle Gatekeeper, extracts enduring architectural invariants and state flows to `docs/reference/`, maintains living Code Navigation Maps, and safely retires progress specs without leaking ephemeral DTO duplicates.
- **Key Features**:
  - **Three-Question Settle Gatekeeper**: Evaluates Q1 (Mermaid state machines & sequence flows), Q2 (fault tolerance & boundary invariants), and Q3 (self-explanatory code & discarding ephemeral DTOs).
  - **Interactive Human Sign-Off**: Generates a clear review card with proposed reference additions and deletion targets before executing mutations.
  - **Automatic WIP Retirement**: Retires completed progress specifications and prunes empty slice directories to uphold Path-as-Status.
  - **Pure-Skill Portability**: 100% pure cognitive Markdown workflow (`SKILL.md`) with zero script or runtime dependencies.

---

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) for details on our Blueprint-Driven Development (BDD) workflow, specification guidelines, and code hygiene standards.

