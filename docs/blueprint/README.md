# Product Blueprints (`docs/blueprint/`)

## Purpose & Scope
This directory archives **Product Blueprints**—high-level design documents defining the **long-term product vision, user personas, end-to-end user journeys, and business objectives (WHY & WHAT)**.

## Retention & Immutability Principle
- **Frozen Intent**: Blueprints capture the ideal product state. During tactical execution, engineering teams frequently make pragmatic trade-offs or defer scope (MVP phasing).
- **Never Retroactively Edit**: Tactical trade-offs do **not** trigger revisions to the blueprint. The blueprint permanently anchors long-term intent. Actual realized scope and architectural decisions are recorded in `docs/reference/` and code types.

## File Naming Convention
Files in this directory follow the 3-Tier Pragmatic WBS pattern:
```
[domain].[capability]_[slug].md
```
*(No leading zeros: use natural numbers like `1.1`, `1.2`, `10.1`)*

*Examples*:
- `1.1_user-onboarding.md`
- `2.3_payment-checkout.md`

## Standard Blueprint Structure
```markdown
# [Feature Name] Product Blueprint

## 1. Metadata
- **Blueprint Code**: [e.g., 1.1]
- **Target Applications / Modules**: [e.g., web-client, api-server, cli]
- **Date**: YYYY-MM-DD

## 2. Overview & Problem Statement
- **Problem**: [User friction or business challenge]
- **Solution**: [Proposed capability]
- **Business Value**: [Measurable outcome or metric impact]

## 3. Personas & Scenarios
- **[User Role]**: [Context of use and expected experience]

## 4. User Journey & Flow
[Mermaid diagram illustrating user interaction flow, decisions, and system boundaries]

## 5. Functional Scope
### P0 (MVP / Required)
- [ ] Essential core capability
### P1 (Enhancements)
- [ ] Secondary capability
```

---

## 6. Abstraction Boundary: Blueprint vs Spec (No Implementation Bleed)

Blueprints permanently anchor long-term vision and system capabilities (WHY & WHAT). They must remain decoupled from tactical execution deltas (HOW).

### 1. Functional Scope
- **Blueprint Level (✅ Required)**: Declare high-level capability objectives (e.g., `Reference Extraction Capability`, `Grounding Verification Capability`).
- **Spec Level (❌ Prohibited in Blueprint)**: Concrete rule identifiers, validation regexes, or parsing AST nodes (e.g., `ref/dead-file-path`, `ref/dead-symbol`).

### 2. Interaction & Execution
- **Blueprint Level (✅ Required)**: High-level architectural value streams (User/Agent -> Auditor -> Actionable Diagnostic Feedback).
- **Spec Level (❌ Prohibited in Blueprint)**: Concrete CLI command lines, slash commands, flags, or script arguments (e.g., `/audit-stale-ref --json`, `npx skills ...`).

### 3. Non-Functional Guarantees
- **Blueprint Level (✅ Required)**: Architectural principles and safety invariants (e.g., *Strict Read-Only Non-Invasive Safety*, *Code as Truth*).
- **Spec Level (❌ Prohibited in Blueprint)**: Specific tactical runtime benchmarks or token budgets (e.g., `< 2,500 tokens`, timeout millisecond limits).

### 4. Target Entities
- **Blueprint Level (✅ Required)**: Coarse-grained module or subsystem domains (e.g., `skills/`, `docs/`, `apps/web`).
- **Spec Level (❌ Prohibited in Blueprint)**: Specific source implementation file paths (e.g., `skills/audit-stale-ref/SKILL.md`).

