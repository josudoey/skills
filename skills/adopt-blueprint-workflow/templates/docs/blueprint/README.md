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
- **Owner**: [Team or Lead]
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
