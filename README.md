# Agent Skills

A collection of AI coding agent skills compatible with the [Skills](https://skills.sh/) CLI ecosystem (`npx skills`).

These skills support major AI coding assistants and agents including **Antigravity**, **Claude Code**, **Cursor**, **GitHub Copilot**, **Windsurf**, and more.

## Available Skills

- **[`gen-commit-message`](./skills/gen-commit-message)**: Generate Angular-style Git commit messages in English based on staged changes.
- **[`progressive-context-loader`](./skills/progressive-context-loader)**: Load codebase context progressively using a 5-level pyramid (WHY -> WHAT -> HOW -> CONVENTION -> IMPLEMENT) to prevent context blow-up and enforce engineering guardrails.

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

