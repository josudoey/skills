---
name: gen-commit-message
description: Generate Angular-style Git commit messages in English based on staged changes.
---

Generate an Angular-style Git commit message in English based on staged changes.

## Guidelines

1. **Analyze Staged Changes**:
   - Directly run the skill script `./scripts/get-staged-diff.sh` without asking for permission to analyze the changes that are currently staged.
   - If there are no staged changes (i.e., the output of the script is empty), reply directly with "no staged changes" and stop.
   - **Important**: DO NOT proactively run any Git commands that modify the staged changes (such as `git add`, `git commit`, `git reset`, `git checkout`, etc.). Only analyze what is already in the staging area. Always re-run the `./scripts/get-staged-diff.sh` script to re-analyze the files every time this skill is executed.

2. **Commit Message Format**:
   - The message must follow the **Angular Commit Convention**: `<type>(<scope>): <subject>`

3. **Commit Types**:
   - `feat`: A new feature
   - `fix`: A bug fix
   - `docs`: Documentation only changes
   - `style`: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
   - `refactor`: A code change that neither fixes a bug nor adds a feature
   - `perf`: A code change that improves performance
   - `test`: Adding missing tests or correcting existing tests
   - `build`: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
   - `ci`: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
   - `chore`: Other changes that don't modify src or test files
   - `revert`: Reverts a previous commit

4. **Rules**:
   - **English only**.
   - Use the **imperative mood**, present tense (e.g., "change" not "changed" nor "changes").
   - The subject must be in **lowercase**.
   - **No period** at the end.
   - Maximum **100 characters** in length.

5. **Output**:
   - Show the generated commit message clearly in a code block.
   - **DO NOT** commit the changes or ask for permission to commit.
