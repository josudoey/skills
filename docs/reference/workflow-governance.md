# Workflow Governance Living Specification (`workflow-governance`)

<!-- Ref: [Blueprint 1.1] §2, §4, §5 -->

## 1. Overview

This living specification documents the system invariants, architectural trade-offs, diagnostic rule sets, and navigation maps governing development workflow health across repositories, anchoring directly to [Blueprint 1.1: Workflow Governance](../blueprint/1.1_workflow-governance.md) within [Domain 1: Agentic Engineering Governance](../blueprint/1.0_agentic-engineering-governance.md).

It establishes an **"ESLint for Development Workflow & Markdown Governance"**, replacing arbitrary 100-point composite scoring with a binary **Quality Gate (`PASSED` vs `BLOCKED`)**, zero-noise UNIX silence for clean runs, and an actionable diagnostic engine.

---

## 2. Blueprint Trade-offs & Current Scope

1. **Pure-Skill First (Zero-Script / Zero-Runtime)**:
   - *Blueprint Ambition*: Explored potential auxiliary inspection scripts (`scripts/audit-workflow.py` or `.js`).
   - *Tactical Decision*: Implemented strictly as a Pure `SKILL.md` cognitive workflow without auxiliary scripts. This ensures 100% universal portability across environments lacking Node.js or Python runtimes and leverages LLM semantic evaluation over fragile, regex-based parsing.
2. **Binary Quality Gate vs Composite Scoring**:
   - *Trade-off*: Eliminated numeric composite scoring (e.g. "85/100") to avoid the *compensatory fallacy* where high scores in documentation volume mask critical broken Code Map navigation errors.
   - *Current Scope*: Binary gate where any `error` immediately blocks the gate, while `warn` flags advisories without blocking delivery.
3. **Token-Guarded Inspection Protocol**:
   - *Trade-off*: Imposes strict metadata-first listing and line-range slicing over full file reads, capping diagnostic context overhead at $< 2,000$ tokens.
4. **Unidirectional Navigation Convention**:
   - *Trade-off*: Eliminated bidirectional reverse reference comments (`// Ref: ...` or `<!-- Ref: ... -->`) in production code and skills.
   - *Current Scope*: All navigation pointers are maintained unilaterally in `docs/reference/[domain].md` (Code Navigation Map). Source code and skill definitions remain 100% decoupled and portable, eliminating redundant maintenance overhead when files move.
5. **Canonical Root Contributor Engine (`CONTRIBUTING.md`)**:
   - *Trade-off*: Workflow governance rules were previously housed internally at `docs/dev-workflow.md`, which was not auto-discovered by GitHub contributor onboarding or community health scanners.
   - *Current Scope*: Elevated the workflow governance engine to repository root `CONTRIBUTING.md` to serve as the unified human/agent contributor contract. The transitional forwarding stub at `docs/dev-workflow.md` has completed its sunset window and is retired, maintaining root `CONTRIBUTING.md` as the exclusive entrypoint.


---

## 3. Business Rules & Invariants

### 3.1 Non-Invasive Safety Guardrail
- The audit engine operates strictly in **read-only mode** on repository governance artifacts (`AGENTS.md`, `.agents/`, `docs/`).
- It **never** mutates, deletes, or modifies application source code or documentation during an audit run.

### 3.2 The Four Diagnostic Rule Sets

| Rule ID | Severity | Scope | Invariant Requirement |
| :--- | :--- | :--- | :--- |
| `consistency/no-manual-status-header` | 🔴 `error` | `docs/progress/**` | Documents must never contain manual status headers (`Status: Draft`, `Status: In Progress`). Status is strictly derived from directory path (**Path-as-Status**). |
| `consistency/no-broken-relative-links` | 🔴 `error` | `docs/**`, `AGENTS.md` | All local relative markdown links must resolve to existing files or directories. |
| `friction/max-token-overhead` | 🟡 `warn` | `docs/convention/**`, `.agents/rules/**` | Flag convention files $> 3,000$ tokens ($\text{bytes} / 3.8$ for ASCII; $\text{bytes} / 2.0$ for CJK). Flag $> 6,000$ tokens as monolithic files requiring modular decomposition. |
| `friction/no-bloated-schema-tables` | 🟡 `warn` | `docs/convention/**` | Tables in convention files must not contain $> 8$ rows of type/field DTO definitions. |
| `truth/no-duplicate-api-dictionaries` | 🟡 `warn` | `docs/reference/**` | Living specifications must never duplicate API payload tables or database schema dictionaries (**Code as Truth**). |
| `traceability/valid-codemap-paths` | 🔴 `error` | `docs/reference/*.md` | All file paths declared in Code Navigation Maps must exist in the workspace. |
| `traceability/valid-blueprint-mapping` | 🔴 `error` | `docs/progress/[code]/` | Active slice directories must map to an existing Blueprint under `docs/blueprint/`. For `skills-repository`, skills must follow `skills/<name>/SKILL.md`. |

### 3.3 Quality Gate Invariant
$$\text{Quality Gate} = \begin{cases} \mathbf{PASSED}, & \text{if } \sum \text{errors} = 0 \\ \mathbf{BLOCKED}, & \text{if } \sum \text{errors} > 0 \end{cases}$$

### 3.4 Language Standard (English-Only Maintenance)
- All governance artifacts (`AGENTS.md`, `.agents/rules/**`), lifecycle specifications (`docs/**`), and skill definitions (`skills/**`) must be maintained in English to ensure cross-ecosystem portability and zero cognitive friction for polyglot AI coding agents.

### 3.5 Universal Accessibility Invariant
- Root `CONTRIBUTING.md` serves as the exclusive, canonical entrypoint for both human open-source contributors and autonomous AI agents without semantic divergence.
- Workflow and development governance discovery relies strictly on standard repository root conventions (`CONTRIBUTING.md`, `AGENTS.md`), eliminating internal legacy forwarding stubs.

### 3.6 The Three-Question Settle Gatekeeper Invariant
Before any active specification in `docs/progress/` is retired, the settlement engine must evaluate:
1. **Q1 (Architectural & State Flows)**: *Does this specification contain Mermaid sequence diagrams, state machine flows, or cross-system protocol transitions not immediately obvious from reading raw code?*
   - If **YES**: Extract and synthesize into `docs/reference/[domain].md`.
2. **Q2 (Fault-Tolerance & Boundary Rules)**: *Does this specification define critical fault-tolerance, offline degradation, retry compensation, quarantine recovery, or domain boundary invariants?*
   - If **YES**: Extract and synthesize into `docs/reference/[domain].md`.
3. **Q3 (Code-as-Truth & Self-Explanatory Logic)**: *Can a future engineer or AI agent understand this mechanism entirely from the production code and automated tests?*
   - If **YES**: **Discard ephemeral details**. Explicitly exclude standard API route tables, CRUD DTO field lists, and mock payloads. Production code is the single source of truth.

### 3.7 Interactive Human Confirmation Guardrail
- The settlement engine must **never** execute silent disk mutations.
- Proposed additions to `docs/reference/[domain].md` and files targeted for deletion must be presented in an interactive review card before applying changes.

### 3.8 Automatic WIP Retirement & Directory Pruning
- Retiring a specification removes the target file from `docs/progress/` to uphold the **Path-as-Status** standard.
- If the parent slice directory (e.g., `docs/progress/1.1/`) is left empty after retirement, it must be automatically pruned to maintain repository cleanliness.

---


## 4. State Machines & Critical Flows

### 4.1 3-Phase Cognitive Inspection Engine

```mermaid
flowchart TD
    subgraph Input["Workspace Inspection"]
        Target["Target Workspace\n(Relative Topology & Governance Docs)"]
    end

    subgraph AgentEngine["Pure SKILL.md Cognitive Engine"]
        Phase1["Phase 1: Metadata Topology Profiler\n(Detect Archetype & File Byte Counts, Fingerprint < 500 tokens)"]
        Phase2["Phase 2: Targeted Probing & Rule Evaluation\n(Evaluate 4 Rule Sets via zero-context grep & file existence)"]
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

### 4.2 Standard Diagnostic Output Formats

- **Mode A (Zero Noise)**:
  ```text
  ✔ Checked [N] governance files across 4 dimensions.
  ✨ 0 errors, 0 warnings. Quality Gate: PASSED (Archetype: [archetype]).
  ```
- **Mode B (ESLint-Style Diagnostics)**:
  ```text
  [file]:[line]
    [[rule-id]] [Diagnostic message]. ([severity])

  ✖ [P] problems ([E] errors, [W] warnings)
  Quality Gate: BLOCKED ([Resolution hint])

  🛠️ Recommended Action Items:
  1. [Actionable remediation step]
  ```

### 4.3 5-Phase Cognitive Settlement Engine (`settle-spec`)

```mermaid
flowchart TD
    Trigger["Trigger: /settle-spec [path]"] --> P1["Phase 1: Pre-flight & Target Resolution"]
    P1 --> P2["Phase 2: Three-Question Gatekeeper Evaluation"]
    P2 --> P3["Phase 3: Living Reference & Code Map Synthesis"]
    P3 --> P4["Phase 4: Interactive Review & User Sign-Off"]
    P4 --> P5["Phase 5: Atomic Settle, Retirement & Commit Suggestion"]

    P4 -->|"User Requests Edits / Abort"| P3
```

- **Phase 1 (Pre-flight & Target Resolution)**: Resolves target progress spec path or prompts user with an interactive list of active specs. Verifies production files and automated tests exist.
- **Phase 2 (Three-Question Gatekeeper Evaluation)**: Analyzes spec against Q1 (state flows), Q2 (fault tolerance/invariants), and Q3 (self-explanatory logic), eliminating ephemeral DTO tables.
- **Phase 3 (Living Reference & Code Map Synthesis)**: Synthesizes enduring invariants and diagrams into `docs/reference/[domain].md` and updates the Code Navigation Map.
- **Phase 4 (Interactive Review & Human Sign-Off)**: Renders a structured review card detailing proposed reference updates and targeted file deletions for explicit user approval.
- **Phase 5 (Atomic Settle, Retirement & Commit)**: Applies reference mutations, deletes the retired progress specification, prunes empty parent slice directories, and provides Conventional Commit guidance.

---

## 5. Code Navigation Map (Code Map)

- **Pure Skill (Workflow Audit)**: [skills/audit-workflow-fitness/SKILL.md](../../skills/audit-workflow-fitness/SKILL.md)
- **Pure Skill (Spec Settlement)**: [skills/settle-spec/SKILL.md](../../skills/settle-spec/SKILL.md)
- **Settle Checklist Reference**: [skills/settle-spec/references/settle-checklist.md](../../skills/settle-spec/references/settle-checklist.md)
- **Code Map Design Patterns**: [skills/settle-spec/references/code-map-patterns.md](../../skills/settle-spec/references/code-map-patterns.md)
- **Repository Catalog**: [README.md](../../README.md)
- **Repository Standards**: [.agents/rules/skills-repository.md](../../.agents/rules/skills-repository.md)
- **Governance Directives**: [AGENTS.md](../../AGENTS.md)
- **Lifecycle Engine Guide**: [CONTRIBUTING.md](../../CONTRIBUTING.md)
- **Domain Master Blueprint**: [docs/blueprint/1.0_agentic-engineering-governance.md](../blueprint/1.0_agentic-engineering-governance.md)
- **Upstream Product Blueprint**: [docs/blueprint/1.1_workflow-governance.md](../blueprint/1.1_workflow-governance.md)

