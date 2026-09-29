# Agent Skills

A collection of AI coding agent skills compatible with the [Skills](https://skills.sh/) CLI ecosystem (`npx skills`).

These skills support major AI coding assistants and agents including **Antigravity**, **Claude Code**, **Cursor**, **GitHub Copilot**, **Windsurf**, and more.

## Available Skills

- **[`gen-commit-message`](./skills/gen-commit-message)**: Generate Angular-style Git commit messages in English based on staged changes.

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
