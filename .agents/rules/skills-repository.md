# Skills Repository Standards

## Directory Structure
- Place each skill in `skills/<skill-name>/` containing a `SKILL.md` file.
- `SKILL.md` must include valid YAML frontmatter with `name` and `description`.
- Store auxiliary scripts under `skills/<skill-name>/scripts/` and ensure they have executable permissions (`chmod +x`).

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
