---
name: audit-workflow-fitness
description: Audit and evaluate project development workflows, markdown governance, and spec fitness. Detects cognitive friction, broken Code Maps, and lifecycle anti-patterns with a token-guarded inspection protocol.
---

# Audit Workflow Fitness (`audit-workflow-fitness`)

A portable, language-agnostic diagnostic skill that operates as a **"Lint for Development Workflow & Markdown Governance"**.

Departing from arbitrary 100-point composite scoring models, this skill eliminates the compensatory fallacy (where high scores in unrelated areas obscure critical navigation failures). It classifies findings into actionable **`error` (blocker)** and **`warn` (advisory smell)** diagnostics with a strict **Quality Gate (`PASSED` vs `BLOCKED`)**.

Adopting a **Pure `SKILL.md` (Zero-Script / Zero-Runtime)** architecture, this skill achieves universal portability across any operating environment (regardless of Node.js or Python availability) and leverages the AI Agent's semantic understanding to avoid rigid, false-positive-heavy regex checks while strictly preventing token blow-up through a metadata-first inspection protocol and UNIX silence ("Silence is golden").

```mermaid
flowchart TD
    subgraph Input["Workspace Inspection"]
        Target["Target Workspace\n(Relative Topology & Governance Docs)"]
    end

    subgraph AgentEngine["Pure SKILL.md Cognitive Engine"]
        Phase1["Phase 1: Metadata Topology Profiler\n(Detect Archetype & File Byte Counts, Fingerprint < 500 tokens)"]
        Phase2["Phase 2: Targeted Probing & Rule Evaluation\n(Evaluate 5 Rule Sets via zero-context grep & file existence)"]
        Phase3["Phase 3: Diagnostic Synthesis & Gate Determination\n(Determine PASSED / BLOCKED Gate + Actionable Remediation)"]
    end

    subgraph Output["Diagnostic Output"]
        Clean["Mode A: Zero-Noise Status\n(0 errors, 0 warnings -> < 50 tokens)"]
        Report["Mode B: ESLint-Style Diagnostic Report\n(Formatted Diagnostics + Remediation Actions)"]
        JSONOutput["Mode C: Structured JSON Output\n(Machine-readable diagnostics)"]
    end

    Target --> Phase1
    Phase1 --> Phase2
    Phase2 --> Phase3
    Phase3 -->|0 Errors, 0 Warns| Clean
    Phase3 -->|Issues Detected| Report
    Phase3 -->|JSON Flag Requested| JSONOutput
```

---

## When to Run This Skill

Activate this skill when:
- Evaluating a repository's documentation architecture and workflow health before starting a major development cycle.
- Checking for workflow drift, broken Code Map pointers, or outdated PRDs in living specifications.
- Validating that active progress specs follow Path-as-Status without prohibited manual status tags.
- Verifying whether rules and conventions have bloated into monolithic token sinks (> 3,000 tokens).
- Running pre-merge or CI workflow quality gates to ensure documentation remains aligned with code as truth.

---

## Non-Invasive Safety Guardrail

> [!IMPORTANT]
> **Strict Read-Only Operations**: The audit engine operates exclusively in read-only mode on repository governance artifacts (`AGENTS.md`, `.agents/`, `docs/`). It **never** mutates, deletes, or modifies application source code or documentation during an audit run. Remediation suggestions are presented in the report for developer review and execution.

---

## Operational Role & Diagnostic Stance

When activated, the agent operates exclusively as a **Strict Workflow & Governance Linter** and uncompromising Quality Gatekeeper:

- **Zero Sycophancy**: Do NOT soften warnings, offer unrequested praise, or make excuses for governance drift. Present diagnostic findings with cold, objective neutrality.
- **Binary Gatekeeping**: Reject compensatory reasoning. High adherence in one area (e.g., clean blueprints) NEVER offsets a violation in another (e.g., broken code maps or manual status tags). A single blocker triggers an absolute `BLOCKED` gate.
- **UNIX Silence ("Silence is golden")**: If zero errors and zero warnings are found, emit only the minimal status line (< 50 tokens). Do not generate conversational preambles, summaries, or pleasantries.
- **Read-Only Invariant**: Act strictly as an analytical inspector. Never attempt to silently mutate or patch files during an audit.

---

## Token-Guarded Inspection Protocol (Strict Constraint)

To prevent cognitive overload and avoid consuming tens of thousands of tokens by indiscriminately dumping full documents into context, the agent must strictly execute the **Metadata-First Protocol**:

1. **Single-pass profiling**: Catalog governance files in a single pass. Gauge file size and token overhead using physical line counts and byte metrics (`bytes / 3.8` for ASCII; `bytes / 2.0` for CJK / multi-byte UTF-8) without iterative per-directory exploration loops.
2. **Static line-count gauge heuristic**:
   - **Safe**: $\le 250$ lines ($\approx 1,800 - 2,500$ tokens in mixed CJK/ASCII environments).
   - **Advisory Smell (`warn`)**: $251 - 400$ lines ($2,500 - 4,000$ tokens).
   - **Blocker (`error` / Split Required)**: $> 400$ lines ($> 4,000$ tokens or $> 12\text{ KB}$).
3. **Targeted probing**: Search for broken relative links, invalid Code Map references, and governance anti-patterns using zero-context pattern searching (`grep_search` / `grep` / existence tests) without loading full file bodies.
4. **Selective slice reading**: If a violation or broken link is suspected, view only the relevant line range (`StartLine` / `EndLine`) rather than loading entire files.
5. **Context Budget**: The complete audit workflow should consume $< 2,000$ tokens of context overhead.

---

## 3-Phase Cognitive Evaluation Procedure

### Phase 1: Metadata Topology Profiler (< 500 tokens)

1. **Identify Project Archetype**:
   - `skills-repository`: Presence of a top-level `skills/` directory containing `*/SKILL.md` files.
   - `monorepo`: Presence of `pnpm-workspace.yaml`, `nx.json`, `lerna.json`, `go.work`, or `Cargo.toml` with `[workspace]`.
   - `application`: Standard single-package configurations (`package.json`, `Cargo.toml`, `go.mod`, `pyproject.toml`, etc.) without workspace files.
2. **Catalog Governance Artifacts**:
   - Check presence, line counts, and file sizes of:
     - Root governance: `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `GEMINI.md`.
     - Spec directories: `docs/blueprint/`, `docs/progress/`, `docs/reference/`, `docs/convention/`, `.agents/rules/`.
     - Workflow engine: `CONTRIBUTING.md`.
3. **Compute Byte & Token Footprint**:
   - Calculate total byte counts and line counts for governance documents.
   - Derive estimated token counts:
     $$\text{Tokens}_{\text{est}} \approx \begin{cases} \text{bytes} / 3.8, & \text{ASCII} \\ \text{bytes} / 2.0, & \text{CJK / Multi-byte} \end{cases}$$

---

### Phase 2: Targeted Probing Across 5 Rule Sets

Categorize all findings into two strict severity levels:
- 🔴 **`error` (Blocker)**: Critical failures that break agent navigation, cause runtime tool-call crashes, or violate core lifecycle invariants. **Any `error` immediately blocks the Quality Gate.**
- 🟡 **`warn` (Advisory Smell)**: High token friction, documentation bloat, or anti-patterns that degrade agent context without completely breaking execution. **Warnings do not block the gate.**

$$\text{Quality Gate} = \begin{cases} \mathbf{PASSED}, & \text{if } \text{errors} = 0 \\ \mathbf{BLOCKED}, & \text{if } \text{errors} > 0 \end{cases}$$

#### Rule Set 1: `consistency` (Governance Consistency & Anti-Pattern Rules)

- **`consistency/no-manual-status-header` (`error`)**:
  - Scan `docs/progress/**` for prohibited manual lifecycle status fields (`Status: Draft`, `Status: In Progress`, `Status: Completed`, etc.).
  - Lifecycle status must be strictly inferred from the directory path (Path-as-Status).
- **`consistency/no-broken-relative-links` (`error`)**:
  - Scan markdown links inside `docs/` and `AGENTS.md` targeting local workspace files using relative paths (e.g., `[text](./path)` or `[text](../path)`).
  - Verify every referenced relative path resolves to an existing file or directory.

#### Rule Set 2: `friction` (Cognitive & Token Friction Rules)

- **`friction/max-token-overhead` (`warn` / `error`)**:
  - Check physical line counts and estimated tokens across all rule and convention files (`docs/convention/**`, `.agents/rules/**`, `AGENTS.md`).
  - Severity thresholds:
    - $\le 250$ lines ($\le 2,500$ tokens): **Clean**.
    - $251 - 400$ lines ($2,500 - 4,000$ tokens): 🟡 `warn` (Advisory smell; recommend topical decomposition).
    - $> 400$ lines ($> 4,000$ tokens or $> 12\text{ KB}$): 🔴 `error` (Blocker; monolithic document requiring mandatory decomposition).
  - **Anti-Loop Remediation Mandate**: Strictly forbid iterative sentence micro-trimming loops (editing text $\to$ script counting $\to$ repeating). Enforce **Decomposition-First**: relocate domain logic to `docs/reference/` or split into sibling topic documents (e.g., `01-architecture-core.md`, `02-naming-conventions.md`).
- **`friction/no-bloated-schema-tables` (`warn`)**:
  - Inspect markdown convention files for prohibited bloated schema/field tables (tables containing $> 8$ rows of type/field DTO definitions, rather than concise architectural comparison tables).

#### Rule Set 3: `truth` (Code-as-Truth Purity Rules)

- **`truth/no-duplicate-api-dictionaries` (`warn`)**:
  - Verify that living specifications in `docs/reference/` do not duplicate API payload tables, JSON request bodies, or database schema column dictionaries.
  - Ensure reference files focus strictly on business invariants, trade-offs, state machines (Mermaid), and Code Maps, delegating data structures to production code contracts.

#### Rule Set 4: `traceability` (Traceability & Lifecycle Alignment Rules)

- **`traceability/valid-codemap-paths` (`error`)**:
  - Validate that paths referenced in `docs/reference/*.md` Code Navigation Maps exist in the codebase.
  - Prevents agent hallucination and navigation failure caused by stale code pointers.
- **`traceability/valid-blueprint-mapping` (`error`)**:
  - Validate that active slice directories under `docs/progress/[code]/` correspond to a valid blueprint code in `docs/blueprint/`.
  - For `skills-repository` archetypes, verify adherence to `.agents/rules/skills-repository.md` (e.g., standard skill directory structure `skills/<skill-name>/SKILL.md` and bulleted catalog links).

#### Rule Set 5: `purity` (Convention Purity & Decoupling Rules)

- **`purity/convention-portability-leak` (`error`)**:
  - Verify that `docs/convention/**` remains **cross-project portable** per the **4-Pillar Litmus Test**:
    1. *Portability*: Conventions must apply universally across projects; project-specific business narratives belong in `docs/reference/`.
    2. *Naming Abstraction*: Must use semantic Roles (`[Role]Executor`, `BaseHandler`) rather than production domain symbols.
    3. *Path Expression*: **Path Patterns / Globs** (`skills/*/...`, `packages/**`) are explicitly allowed. Exact production file paths are prohibited.
    4. *Lifecycle Trigger*: Conventions evolve during architectural shifts, not product feature PRs.
- **`purity/no-concrete-implementation-leak` (`error`)**:
  - Scan `.agents/rules/**`, `docs/convention/**`, and `AGENTS.md` for concrete business logic, state reducers, or full component implementations verified to exist in active production code.
  - Illustrative code snippets in conventions must remain minimal syntax skeletons ($\le 10$ lines) using Role-based abstractions.
- **`purity/no-search-collision-symbol` (`warn`)**:
  - Scan convention files for concrete PascalCase or camelCase production symbols in examples or narrative text that match active workspace symbols, polluting global searches.
  - Recommend semantic Role-based abstractions (e.g., `SecondaryOperationPanel`, `[Role]Executor`).
- **`purity/no-reference-pointer-leak` (`warn`)**:
  - Scan convention files for explicit links pointing to domain living references (`docs/reference/*.md`).
  - Conventions must remain pure architectural patterns decoupled from volatile domain documents.

---

### Phase 3: Diagnostic Synthesis & Gate Determination

Aggregate findings and evaluate the binary Quality Gate:

#### Mode A: Clean Run (UNIX Silence / Zero Noise)
When 0 errors and 0 warnings are detected:
```text
✔ Checked [N] governance files across 5 dimensions.
✨ 0 errors, 0 warnings. Quality Gate: PASSED (Archetype: [archetype]).
```

#### Mode B: Issues Detected (ESLint-Style Diagnostic Report)
When diagnostics are present:
```text
[file]:[line]
  [[rule-id]] [Diagnostic message]. ([severity])

✖ [P] problems ([E] errors, [W] warnings)
Quality Gate: [BLOCKED/PASSED] ([Resolution hint])

🛠️ Recommended Action Items:
1. [Actionable step for issue 1]
2. [Actionable step for issue 2]
```

#### Mode C: Structured JSON Output (Optional)
When structured output is requested:
```json
{
  "gate": "PASSED | BLOCKED",
  "archetype": "skills-repository | monorepo | application",
  "summary": {
    "filesChecked": 14,
    "errors": 0,
    "warnings": 0
  },
  "diagnostics": [
    {
      "rule": "consistency/no-manual-status-header",
      "severity": "error",
      "file": "docs/progress/1.1/1-feature.md",
      "line": 4,
      "message": "Found prohibited 'Status: Draft'. Infer status from directory path.",
      "suggestedFix": "Remove line 4."
    }
  ]
}
```

---

## Actionable Remediation Guidelines

When diagnosing violations, provide direct, copy-pasteable remediation instructions:
1. **Manual Status Header**: "Remove explicit status declarations from header. Move document to appropriate lifecycle folder (`docs/progress/` for WIP, `docs/reference/` for settled invariants)."
2. **Broken Link / Stale Code Map**: "Update relative path `[broken/path]` to existing file `[valid/path]`, or prune obsolete pointer."
3. **Token Friction & Monolithic Bloat (Anti-Loop)**: "Apply **Decomposition-First**. Do NOT perform iterative text micro-trimming loops. Split file into topical sub-documents (target $\le 250$ lines each) or extract domain logic into `docs/reference/<domain>.md`."
4. **Convention Portability Leak**: "Apply the **4-Pillar Litmus Test**. Relocate project-specific domain narratives and exact file paths to `docs/reference/<domain>.md`. Retain only cross-project portable macro-patterns with path patterns / globs."
5. **Duplicate API Dictionary**: "Remove static table and replace with a direct pointer to production schema or typed contract in code."
6. **Concrete Implementation Leak**: "Extract business logic and domain components to `docs/reference/<domain>.md`. Completely delete implementation block from convention without leaving reverse links."
7. **Search Collision Symbol**: "Replace concrete production symbol with a semantic Role-based abstraction (e.g. `SecondaryOperationPanel`, `[Role]Executor`)."
8. **Reference Link Leak**: "Prune domain reference link from convention. Keep conventions pattern-pure and decoupled from domain documents."
