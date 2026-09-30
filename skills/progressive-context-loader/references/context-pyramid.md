# Context Pyramid Architecture & Mapping Guide

This guide outlines how to apply the 5-Level Context Pyramid across different software architectures using universal patterns, without binding to any specific project or proprietary codebase.

---

## 1. Modular Monorepo Architecture (Multi-package / Workspace)

In a workspace-based monorepo containing shared libraries and application consumers:

### Level 1: WHY (Intent & Objectives)
- **Target Sources**: Task ticket, feature proposal, user story, or high-level architecture note.
- **Typical Locations**: `docs/proposals/`, `rfc/`, or issue trackers.
- **Key Extraction**: The user problem, primary user journey, and acceptance criteria.

### Level 2: WHAT (Domain Invariants & Business Rules)
- **Target Sources**: Domain documentation, ADRs (Architecture Decision Records), or state machine definitions.
- **Typical Locations**: `docs/adr/`, `docs/domain/`, or package-level READMEs.
- **Key Extraction**: Allowed state transitions, permission boundaries, and domain invariants.

### Level 3: HOW (Shared Contracts & Types)
- **Target Sources**: Public API definitions, schema validators, and data contracts.
- **Typical Locations**: `packages/core/types/`, `packages/schema/`, or `libs/contracts/`.
- **Key Extraction**: Exact interface keys, enum values, and nullability (Code as Truth).

### Level 4: CONVENTION (Engineering & Layer Guardrails)
- **Target Sources**: Repository coding standards, linters, and architectural guidelines.
- **Typical Locations**: `docs/conventions/`, `.eslintrc`, or `CONTRIBUTING.md`.
- **Key Extraction**: Layering boundaries (e.g. shared packages cannot import from apps), naming conventions, and shared error wrappers.

### Level 5: IMPLEMENT (Target Consumer Slices)
- **Target Sources**: The consuming app/package implementation and its test suite.
- **Typical Locations**: `apps/[app-name]/src/features/` and adjacent `__tests__/`.
- **Key Extraction**: Local state slice, hook/component integration, and test assertions.

---

## 2. Standard Web & Fullstack Application

In modern fullstack or modular web applications (e.g., Next.js, Nuxt, Vite + REST/GraphQL):

### Level 1: WHY (Intent & Objectives)
- **Target Sources**: Product spec, bug report, or sprint backlog item.
- **Typical Locations**: `specs/`, issue templates, or PR descriptions.
- **Key Extraction**: UI interaction goal, trigger condition, and expected outcome.

### Level 2: WHAT (Domain Invariants & Business Rules)
- **Target Sources**: Business logic specifications or feature guidelines.
- **Typical Locations**: `docs/features/` or domain specifications.
- **Key Extraction**: Validation rules, edge-case limits, and business calculations.

### Level 3: HOW (API Schemas & State Interfaces)
- **Target Sources**: Data transfer objects (DTO), OpenAPI specs, or TypeScript models.
- **Typical Locations**: `src/types/`, `src/api/schema.ts`, or generated API client types.
- **Key Extraction**: Request payload shape, response status codes, and entity schemas.

### Level 4: CONVENTION (Framework & Code Standards)
- **Target Sources**: Project style guide, hook usage guidelines, and UI design tokens.
- **Typical Locations**: `.stylelintrc`, `docs/guidelines.md`, or coding convention docs.
- **Key Extraction**: State management patterns, hook rules, i18n localization constraints, and component hierarchy.

### Level 5: IMPLEMENT (Component, Hook & Test Slices)
- **Target Sources**: Specific component/hook files and corresponding unit/e2e tests.
- **Typical Locations**: `src/features/[feature]/` and `*.test.tsx`.
- **Key Extraction**: Function body, JSX structure, and mock test setup.

---

## 3. Layered / Clean Architecture Backend

In backend services adopting hexagonal, onion, or clean architecture patterns:

### Level 1: WHY (Intent & Objectives)
- **Target Sources**: Technical design document (TDD), RFC, or user story.
- **Typical Locations**: `docs/rfc/` or Jira task description.
- **Key Extraction**: System interaction goal, upstream trigger, and downstream effect.

### Level 2: WHAT (Domain Rules & Entities)
- **Target Sources**: Core domain entities and domain service rules.
- **Typical Locations**: `internal/domain/` or `src/core/entities/`.
- **Key Extraction**: Entity validation methods, domain events, and business invariants.

### Level 3: HOW (Ports & DTO Contracts)
- **Target Sources**: Repository interfaces, input/output port definitions, and database schemas.
- **Typical Locations**: `internal/ports/`, `src/core/interfaces/`, or migration SQL files.
- **Key Extraction**: Interface method signatures, database table definitions, and DTO constraints.

### Level 4: CONVENTION (Architecture Rules & Error Discipline)
- **Target Sources**: Architectural boundary rules and cross-cutting standards.
- **Typical Locations**: `docs/architecture/` or package guidelines.
- **Key Extraction**: Dependency direction (inner layers must not know outer layers), transaction boundaries, and standard application error formats.

### Level 5: IMPLEMENT (Adapters, Handlers & Tests)
- **Target Sources**: Specific controller/handler, repository implementation, and integration test.
- **Typical Locations**: `internal/adapters/` and `*_test.go` (or `*.spec.ts`).
- **Key Extraction**: Request parsing, use-case invocation, and assertion statements.

---

## Token Budget Allocation Rule of Thumb

To ensure the agent stays within a sharp context window:

- **Level 1 (WHY)**: ~5% (300 – 500 tokens)
- **Level 2 (WHAT)**: ~15% (800 – 1,200 tokens)
- **Level 3 (HOW)**: ~30% (1,500 – 2,500 tokens)
- **Level 4 (CONVENTION)**: ~20% (1,000 – 1,500 tokens)
- **Level 5 (IMPLEMENT)**: ~30% (2,000 – 2,500 tokens)

**Target Maximum Context Loaded per Task Context**: <= 6,000 ~ 8,000 tokens.
