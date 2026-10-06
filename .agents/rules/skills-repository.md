# Skills Repository Standards

## Directory Structure
- Place each skill in `skills/<skill-name>/` containing a `SKILL.md` file.
- `SKILL.md` must include valid YAML frontmatter with `name` and `description`.
- Store auxiliary scripts under `skills/<skill-name>/scripts/` and ensure they have executable permissions (`chmod +x`).

## Skill Design Principles (Pure-Skill First)
- **Cognitive Workflow as Core**: Design skills with pure Markdown (`SKILL.md`) instructions, reasoning steps, and semantic criteria as the primary driver.
- **Universal Portability (Zero-Runtime)**: Do not impose hard dependencies on specific language runtimes (Node.js, Python) unless strictly necessary. Skills must remain functional in bare environments and across varied project stacks.
- **Auxiliary Scripts as Optional Fast-Paths**: Scripts stored under `skills/<skill-name>/scripts/` must be treated strictly as optional acceleration tools or CLI wrappers. `SKILL.md` must provide clear instructions so an Agent can reason through the task even if scripts are not run.

## Verification
- Validate discovery locally before pushing using:
  - `npx skills add . -l`
  - `npx skills use . --skill <skill-name>`

## Documentation & README Guidelines
- **Do not use Markdown tables** to display the list of available skills.
- Always use a bulleted list with repository-relative links:
  `- **[<skill-name>](./skills/<skill-name>)**: <description>`
- Include standard `npx skills` command examples:
  - `npx skills add <repo>`
  - `npx skills add <repo> --skill <name>`
  - `npx skills add <repo> -g`
  - `npx skills use <repo>@<name>`

## Path Portability & Standards
- **Strict Relative Paths**: All documentation links, skill manifests, script execution parameters, and configuration files must use repository-relative paths (`./` or `../`).
- **Zero Absolute Paths**: Hardcoded local machine paths (e.g., `/Users/...` or `/home/...`) are strictly prohibited in all committed files.

