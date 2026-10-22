---
name: craft-spec
description: Formalize Stage 1 Specification Authoring across BDD and Universal repositories. Evaluates the Zero-Assumption Gatekeeper, strictly maintains Code Immunity, and crafts high-density, contract-driven specifications optimized for downstream AI coding agents.
---

# Craft Specification (`craft-spec`)

A portable, pure-cognitive workflow for engineers and AI agents to execute **Stage 1: Specification Authoring** across Blueprint-Driven Development (BDD) and universal software repositories.

This skill introduces the **Zero-Assumption Gatekeeper** to fail-fast against ambiguous requirements, strictly enforces **Code Immunity** (zero changes to application code), and authors high-density, contract-driven specifications optimized for downstream AI coding agents to implement during Stage 2 without architectural drift or hallucination.

```mermaid
flowchart TD
    UserReq["User Requirement / Intent"] --> Gate{"Zero-Assumption\nGatekeeper"}
    
    Gate -- "Unclear / Missing Invariants / No Oracle" --> Clarify["🛑 Halt & Targeted Clarification\n(Single/Multi-choice Inquiries)"]
    Clarify --> UserReq
    
    Gate -- "100% Clear & Verified" --> Archetype{"Workspace Archetype\nDetection"}
    
    Archetype -- "BDD Mode (docs/progress/)" --> GroundBDD["Grounding via Blueprint & Living Specs\nTarget: docs/progress/[code]/[Index]-feature-[slug].md"]
    Archetype -- "Universal Mode (Generic Repo)" --> GroundUni["Grounding via Manifests, Types & Readme\nTarget: specs/ or .agents/specs/[slug].md"]
    
    GroundBDD --> Draft["Draft Agent-Ready Spec\n(Boundaries, Mutation Matrix, Contracts, Oracle)"]
    GroundUni --> Draft
    
    Draft --> Sim["Agent Execution Feasibility Simulation\n(Self-Audit: Zero-Guesswork Check)"]
    Sim --> Stage1Done["Stage 1 Gate Delivered\n🛑 Immediate Tool Stop (Await Human Review)"]
    
    Stage1Done -.->|"After Approval (Stage 2)"| Downstream["Downstream AI Coding Agent\n(Implements Code & Passes Tests)"]
```

---

## When to Run This Skill

Activate this skill when:
- Starting a new feature, vertical slice, or architectural mechanism before writing any code.
- Formulating Stage 1 specifications in a BDD repository (`docs/progress/`).
- Authoring structured, machine-executable specifications in a non-BDD generic repository.
- Preventing AI agents from rushing into premature code implementation or making unverified assumptions.
- Establishing crisp execution guardrails, file mutation matrices, and automated verification oracles for downstream agents.

---

## System Invariants & Guardrails

> [!IMPORTANT]
> **Code Immunity Guardrail**: The `craft-spec` skill operates exclusively in **read-only mode** on codebase implementation files. It is strictly forbidden from creating, updating, or deleting application code, test implementations, package manifests, or tool configs (`src/**`, `lib/**`, `apps/**`, `packages/**`, etc.). The **only permitted persistent artifact** is the Stage 1 specification markdown file.

- **The Zero-Assumption Gatekeeper**: Never extrapolate or assume default technical choices. Evaluate the **4-Pillar Clarity Test** before drafting:
  1. *Scope & Intent (WHY)*: Core user problem, business goal, and out-of-scope boundaries defined.
  2. *Inputs & Dependencies (WHAT)*: Data models, configs, environment prerequisites, and APIs verified.
  3. *Architectural Invariants (CONSTRAINTS)*: Framework conventions, design systems, unidirectional code maps acknowledged.
  4. *Verification Oracle (ACCEPTANCE)*: Deterministic, automated CLI command and assertable pass/fail criteria identified.
  - If any pillar fails, **immediately halt** and execute the Targeted Clarification Protocol.
- **Adaptive Dual-Mode Operation**:
  - **Mode A (BDD Mode)**: Detected via `docs/progress/` or `docs/blueprint/`. Spec target: `docs/progress/[blueprint-code]/[Index]-feature-[slug].md`.
  - **Mode B (Universal Mode)**: Detected when BDD markers are absent. Target: discovered spec directory (`specs/`, `docs/specs/`, `docs/plans/`) or fallback to `.agents/specs/[feature-slug].md`.
- **Stage Gate Isolation (No Premature Implementation)**: The deliverable of Stage 1 is strictly the specification document. After writing the spec, stop tools immediately and await human review.
- **Pure-Skill First (Zero-Runtime Dependency)**: Implemented strictly as a cognitive Markdown workflow (`SKILL.md`) without auxiliary script binaries.
- **English-Only Maintenance**: All specifications, frontmatter, diagrams, and commit suggestions must be authored exclusively in English.
- **Path Portability & Zero-`file://` Invariant**:
  All file paths, symbol references, and markdown links inside the generated specification document MUST strictly use repository-relative paths (e.g., `docs/reference/...`, `libs/...`) or plain inline code backticks (e.g., `StartupChecklistItemView.tsx`).
  The `file://` URI scheme and machine-specific absolute workstation paths (e.g., `/Users/*`, `/home/*`, `C:\*`) are **STRICTLY FORBIDDEN** within any repository documents. `file://` links are exclusively reserved for interactive chat dialogue, never repository files.
- **Workspace Boundary & Context Isolation Invariant**:
  The specification MUST be anchored strictly within the active target repository workspace (`CWD` / Workspace Root).
  The agent MUST ignore any open editor documents or conversation history belonging to external directories or different repositories. All analyzed blueprints, living references, and File Mutation Matrix paths must reside 100% within the current workspace boundary.

---

## 5-Phase Execution Protocol

```mermaid
sequenceDiagram
    autonumber
    actor User as Engineer / User
    participant Craft as craft-spec Skill
    participant Repo as Target Workspace

    User->>Craft: Trigger /craft-spec [intent / requirement]
    Craft->>Craft: Phase 1: 4-Pillar Clarity Gatekeeper Test
    alt Ambiguity Detected
        Craft-->>User: 🛑 Halt: Targeted Clarification (Options / Inquiries)
        User-->>Craft: Provide Clarification
    end
    Craft->>Repo: Phase 2: Archetype Profiling & Read-Only Grounding
    Repo-->>Craft: Return workspace mode, manifests, types & living specs
    Craft->>Craft: Phase 3: Synthesize Agent-Ready Spec
    Craft->>Craft: Phase 4: Downstream Agent Feasibility Simulation
    Craft->>Repo: Phase 5: Write Spec to Resolved Target Directory
    Craft-->>User: Present Spec Link & Freeze Tools (Await Review)
```

### Phase 1: Zero-Assumption Gatekeeper Evaluation
1. Parse user requirement or issue description.
2. Evaluate against the 4-Pillar Clarity Test (see [clarity-gatekeeper-checklist.md](./references/clarity-gatekeeper-checklist.md)).
3. If any requirement, boundary, or verification oracle is ambiguous:
   - **HALT IMMEDIATELY**. Do not write any file to disk.
   - Emit the structured clarification block (see below) with 2–4 targeted options or direct questions.
4. If the prompt is ambiguous and the active document belongs to an external project, halt and trigger clarification rather than guessing or borrowing foreign domain context.

### Phase 2: Archetype Profiling & Read-Only Grounding
1. **Enforce Workspace Anchor**: Grounding MUST strictly resolve relative to the current workspace root (`CWD`). Explicitly disregard open editor tabs (`Active Document`, `Other open documents`) that reside outside the active repository root.
2. **Detect Mode**:
   - `docs/progress/` or `docs/blueprint/` present in current workspace ➔ **Mode A (BDD)**.
   - Otherwise ➔ **Mode B (Universal)**.
3. **Context Grounding (Read-Only)**:
   - *Mode A*: Ground from upstream blueprint (`docs/blueprint/[code]_*.md`) and living references (`docs/reference/`). Resolve next sequential index in `docs/progress/[code]/`.
   - *Mode B*: Ground from repository `README.md`, package manifests (`package.json`, `Cargo.toml`, etc.), and exported types. Resolve spec directory (`specs/`, `docs/specs/`, or `.agents/specs/`).

### Phase 3: Agent-Ready Spec Synthesis
Draft the specification using the mandatory 6-section schema (see [spec-template.md](./references/spec-template.md)):
1. `## 1. Overview & Rationale` (Mermaid flowchart + problem statement)
2. `## 2. System Invariants & Guardrails` (Explicit boundaries & Out-of-Scope list)
3. `## 3. Cognitive / Execution Workflow Protocol` (Deterministic steps)
4. `## 4. File Mutation Matrix` (`CREATE`, `MODIFY`, `DELETE`, `FORBIDDEN`)
5. `## 5. Interface Contract & Schema Deltas` (Code as Truth)
6. `## 6. Verification Oracle & Quality Gate` (Deterministic CLI commands)

### Phase 4: Downstream Agent Feasibility Simulation
Execute a cognitive simulation before writing:
- *Check 1*: Can a fresh AI agent execute Stage 2 without guessing any file path or type signature?
- *Check 2*: Are all qualitative adjectives replaced with measurable invariants?
- *Check 3*: Is the Verification Oracle fully automated and executable in terminal?
- *Check 4 (Path Purity Check)*: Verify that the drafted specification markdown contains **ZERO occurrences** of `file://`, `/Users/`, `/home/`, or OS-specific absolute roots before invoking `write_to_file`. If found, convert them to repository-relative paths or inline backticks immediately.
- *Check 5 (Workspace Containment Check)*: Verify that all declared paths in the File Mutation Matrix reside 100% within the current target repository workspace.

### Phase 5: Delivery & Stage Gate Isolation
1. Write the completed spec to the resolved target path.
2. Present a concise summary (Mode, File link, Mutation Matrix summary, Verification command).
3. **STOP CALLING TOOLS**: Freeze execution immediately and await human approval.

---

## Clarification Output Format (When Gatekeeper Halts)

When requirements are ambiguous or incomplete, output this exact structure:

```markdown
> [!CAUTION]
> **Stage 1 Gatekeeper Blocker: Requirement Ambiguity Detected**
> Specification authoring has been halted to prevent architectural hallucination.

### 🔴 Blocking Ambiguities:
1. **[Dimension Name]**: [Explanation of why this cannot be drafted without user input]

### ❓ Clarification Needed:
- **Question 1**: [Specific question with 2-4 mutually exclusive options (A/B/C) or direct answer requirement]
- **Question 2**: [Scope / Out-of-Scope boundary confirmation]
```

---

## Additional References

- [Specification Template](./references/spec-template.md)
- [Clarity Gatekeeper Checklist](./references/clarity-gatekeeper-checklist.md)
