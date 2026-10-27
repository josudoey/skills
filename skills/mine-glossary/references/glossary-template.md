# [Domain / Workspace] Domain Glossary & Ubiquitous Language

<!-- Invariant: All paths must be repository-relative or enclosed in inline code backticks. NEVER use file:// or workstation-absolute paths (/Users/*, /home/*). -->

## Purpose & Scope
This living document maintains the authoritative Ubiquitous Language and domain glossary for [Domain / Workspace]. It anchors business concepts directly to verified code symbols, resolves multilingual terminological discrepancies, and defines non-negotiable domain invariants.

---

## 1. [Primary Bounded Context / Subsystem Name]

- **[Canonical English Term]**:
  - **Bounded Context**: [Subsystem / domain package, e.g., Order Processing]
  - **Code Anchor**: `[Symbol / Interface / Enum]` in `[path/to/types.ts]`
  - **Localized Synonyms (zh-TW)**: [Traditional Chinese translations or colloquial synonyms, e.g., 作廢]
  - **Forbidden Aliases**: [Ambiguous or prohibited synonyms to reject, e.g., cancel, delete]
  - **Domain Invariant**: [1–2 sentences on core state machine rules, calculations, or invariants]

- **[Contrasting / Paired Concept]**:
  - **Bounded Context**: [Subsystem / domain package]
  - **Code Anchor**: `[Symbol / Interface / Enum]` in `[path/to/types.ts]`
  - **Localized Synonyms (zh-TW)**: [Traditional Chinese translation, e.g., 退款]
  - **Forbidden Aliases**: [Prohibited synonyms]
  - **Domain Invariant**: [1–2 sentences contrasting boundary conditions against the paired concept]

---

## 2. [Secondary Bounded Context / Subsystem Name]

- **[Canonical English Term]**:
  - **Bounded Context**: [Subsystem / domain package]
  - **Code Anchor**: `[Symbol / Interface / Enum]` in `[path/to/types.ts]`
  - **Localized Synonyms (zh-TW)**: [Localized synonyms]
  - **Forbidden Aliases**: [Prohibited synonyms]
  - **Domain Invariant**: [Domain invariant rule]
