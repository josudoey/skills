# Code Navigation Map Design Patterns

This guide defines the standards and authoring conventions for maintaining **Code Navigation Maps (Code Maps)** in living reference documentation (`docs/reference/*.md`).

---

## 1. Purpose of the Code Navigation Map

In Blueprint-Driven Development, documentation is explicitly decoupled from code to prevent maintenance friction:
- **No Reverse Coupling**: Source code, test files, and skill manifests do **not** contain reverse documentation pointers (e.g., `// Ref: docs/reference/...`).
- **Unidirectional Navigation**: `docs/reference/[domain].md` serves as the authoritative map directing human engineers and AI coding agents to canonical implementation files and automated test suites.

---

## 2. Structure & Formatting Rules

A canonical Code Navigation Map sits at the conclusion of each living reference document:

```markdown
## 5. Code Navigation Map (Code Map)

- **Pure Skill Implementation**: [skills/settle-spec/SKILL.md](../../skills/settle-spec/SKILL.md)
- **Checklist Reference**: [skills/settle-spec/references/settle-checklist.md](../../skills/settle-spec/references/settle-checklist.md)
- **Code Map Patterns**: [skills/settle-spec/references/code-map-patterns.md](../../skills/settle-spec/references/code-map-patterns.md)
- **Repository Catalog**: [README.md](../../README.md)
- **Governance Directives**: [AGENTS.md](../../AGENTS.md)
- **Lifecycle Engine Guide**: [CONTRIBUTING.md](../../CONTRIBUTING.md)
- **Domain Master Blueprint**: [docs/blueprint/1.0_agentic-engineering-governance.md](../blueprint/1.0_agentic-engineering-governance.md)
- **Upstream Product Blueprint**: [docs/blueprint/1.1_workflow-governance.md](../blueprint/1.1_workflow-governance.md)
```

### Standard Formatting Guidelines
1. **Bold Role Descriptor**: Describe the architectural role of the target file (`- **[Role Description]**: [path](relative-link)`).
2. **Strict Relative Links**: Always use relative paths (`../../` or `../`) from the reference file to the target. Never use absolute paths (e.g., `/Users/...`).
3. **Canonical Files Only**: Target primary entries, interfaces, domain engines, and test suites. Do not list dozens of trivial utility or helper files.
4. **Link Integrity**: Every linked path must exist on disk. Broken links in Code Maps will trigger an `error` in `audit-workflow-fitness` (`traceability/valid-codemap-paths`).

---

## 3. Recommended Code Map Groupings

For larger domains spanning multiple layers, group entries logically:

```markdown
## 5. Code Navigation Map (Code Map)

### Core Interfaces & Domain Types
- **Domain Entities & Types**: [libs/billing/types.ts](../../libs/billing/types.ts)
- **Validation Schemas**: [libs/billing/schemas.ts](../../libs/billing/schemas.ts)

### Production Services & Handlers
- **Subscription Engine**: [libs/billing/subscription-engine.ts](../../libs/billing/subscription-engine.ts)
- **Payment Webhook Handler**: [apps/api/handlers/billing-webhook.ts](../../apps/api/handlers/billing-webhook.ts)

### Automated Tests
- **Subscription Unit Tests**: [tests/unit/subscription.spec.ts](../../tests/unit/subscription.spec.ts)
- **Webhook Integration Tests**: [tests/integration/billing-webhook.spec.ts](../../tests/integration/billing-webhook.spec.ts)

### Governance & Blueprints
- **Domain Blueprint**: [docs/blueprint/2.0_billing-engine.md](../blueprint/2.0_billing-engine.md)
```
