# Annotasi Software Project Template

An opinionated, AI-ready software product development template for fullstack production applications.

This template is designed for teams or individual builders who use AI coding agents such as Claude, Codex, or similar tools, while still preserving clear product intent, architecture discipline, traceable feature behavior, and production engineering standards.

The template intentionally avoids document inflation. Each concern should have one authoritative source of truth.

---

## 1. Why This Template Exists

AI-assisted development is fast, but speed creates risk when product requirements, architecture decisions, API contracts, and implementation rules live only in chat history or are duplicated across many documents.

This template provides a lightweight documentation system that keeps the important decisions durable and gives both humans and AI agents a predictable way to understand a project.

The core flow is:

```text
PRODUCT BRIEF
      ↓
     PRD
      ↓
FEATURE SPECS
      ↓
ARCHITECTURE + ADR
      ↓
MACHINE-READABLE CONTRACTS
      ↓
ENGINEERING STANDARDS
      ↓
IMPLEMENTATION
      ↓
TEST EVIDENCE
      ↓
RELEASE
```

---

## 2. Core Principles

### 2.1 One Concern, One Source of Truth

Do not describe the same decision in several places unless one document only links to the authoritative source.

Examples:

- Product purpose and target users → `PRODUCT_BRIEF.md`
- Product-level capabilities and scope → `PRD.md`
- Detailed behavior of one feature → `docs/01_features/<feature>.md`
- System structure and technical boundaries → `SYSTEM_ARCHITECTURE.md`
- Important architecture decisions → `docs/02_architecture/adr/`
- REST interface → `contracts/openapi/`
- Async/event interface → `contracts/asyncapi/`
- Development rules → `docs/standards/`

### 2.2 Documentation Must Help Delivery

A document is useful when it helps answer a real engineering or product question.

Do not create documentation only because a template contains a section. Remove sections that do not apply.

### 2.3 Contracts Before Implementations

When an externally consumed API, event, schema, or persistent format changes, update its contract or migration definition before or together with the implementation.

### 2.4 Decisions Must Be Explicit

Material architecture changes should not exist only in code or chat. Record them as ADRs.

### 2.5 AI Agents Read Selectively

Do not instruct AI agents to read the entire repository.

Agents should read:

1. `AGENTS.md`
2. the relevant product or feature specification
3. relevant architecture documentation
4. relevant ADRs
5. relevant contracts
6. relevant engineering standards

---

## 3. Recommended Repository Structure

```text
.
├── README.md
├── AGENTS.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── .env.example
│
├── docs/
│   ├── 00_product/
│   │   ├── PRODUCT_BRIEF.md
│   │   ├── PRD.md
│   │   └── ROADMAP.md
│   │
│   ├── 01_features/
│   │   ├── README.md
│   │   └── FEATURE_TEMPLATE.md
│   │
│   ├── 02_architecture/
│   │   ├── SYSTEM_ARCHITECTURE.md
│   │   ├── DATA_MODEL.md
│   │   ├── NON_FUNCTIONAL_REQUIREMENTS.md
│   │   └── adr/
│   │       └── ADR_TEMPLATE.md
│   │
│   ├── 03_design/
│   │   ├── UX_FLOWS.md
│   │   └── DESIGN_SYSTEM.md
│   │
│   ├── 04_engineering/
│   │   ├── TEST_STRATEGY.md
│   │   └── THREAT_MODEL.md
│   │
│   ├── 05_operations/
│   │   ├── DEVELOPER_SETUP.md
│   │   ├── CONFIGURATION.md
│   │   ├── DEPLOYMENT.md
│   │   └── RUNBOOK.md
│   │
│   ├── 06_delivery/
│   │   ├── RISKS.md
│   │   ├── RELEASE_CHECKLIST.md
│   │   └── KNOWN_LIMITATIONS.md
│   │
│   └── standards/
│       ├── 00_STANDARD_INDEX.md
│       ├── 01_ENGINEERING_WORKFLOW.md
│       ├── 02_CODE_QUALITY.md
│       ├── 03_ARCHITECTURE.md
│       ├── 04_BACKEND_STANDARD.md
│       ├── 05_FRONTEND_STANDARD.md
│       ├── 06_API_INTEGRATION_STANDARD.md
│       ├── 07_DATA_PERSISTENCE_STANDARD.md
│       ├── 08_SECURITY_STANDARD.md
│       ├── 09_TESTING_STANDARD.md
│       ├── 10_OBSERVABILITY_RELIABILITY.md
│       ├── 11_PERFORMANCE_STANDARD.md
│       ├── 12_DEPENDENCY_SUPPLY_CHAIN.md
│       ├── 13_CI_CD_RELEASE.md
│       └── 14_AI_ASSISTED_DEVELOPMENT.md
│
├── contracts/
│   ├── openapi/
│   │   └── openapi.yaml
│   ├── asyncapi/
│   │   └── asyncapi.yaml
│   └── schemas/
│
└── src/
```

Not every project needs every file. Project profiles may remove sections that are not relevant.

---

## 4. Source of Truth Map

| Question | Authoritative Source |
|---|---|
| Why does this product exist? | `docs/00_product/PRODUCT_BRIEF.md` |
| Who is it for? | `docs/00_product/PRODUCT_BRIEF.md` |
| What should the product provide? | `docs/00_product/PRD.md` |
| How should feature X behave? | `docs/01_features/<feature>.md` |
| How is the system structured? | `docs/02_architecture/SYSTEM_ARCHITECTURE.md` |
| Why was architecture decision X made? | `docs/02_architecture/adr/` |
| What is the API contract? | `contracts/openapi/` |
| What is the event contract? | `contracts/asyncapi/` |
| What is the persistent data model? | schema/migrations + `DATA_MODEL.md` |
| How should the UI look and behave? | `DESIGN_SYSTEM.md` + relevant feature spec |
| How should code be implemented? | `docs/standards/` |
| How should the system be tested? | `TEST_STRATEGY.md` + relevant feature spec |
| How is the project run locally? | `DEVELOPER_SETUP.md` |
| How is the system deployed? | `DEPLOYMENT.md` |
| What known risks exist? | `RISKS.md` |
| What is intentionally unsupported? | `KNOWN_LIMITATIONS.md` |
| Where is the product going next? | `ROADMAP.md` |

---

## 5. Quick Start

### Step 1 — Define Product Context

Complete:

```text
docs/00_product/PRODUCT_BRIEF.md
```

Do not start by choosing frameworks. Start with the problem, target users, desired outcomes, scope, constraints, and success metrics.

### Step 2 — Define Product Scope

Create or complete:

```text
docs/00_product/PRD.md
```

Keep the PRD product-oriented. Detailed technical design belongs in architecture documentation.

### Step 3 — Create Feature Specs

For each significant capability, copy:

```text
docs/01_features/FEATURE_TEMPLATE.md
```

Example:

```text
docs/01_features/authentication.md
docs/01_features/course-catalog.md
docs/01_features/checkout.md
docs/01_features/payment.md
```

### Step 4 — Establish Architecture

Complete:

```text
docs/02_architecture/SYSTEM_ARCHITECTURE.md
```

Create an ADR whenever a material architectural decision must be recorded.

### Step 5 — Define Contracts

Use machine-readable contracts where possible:

```text
REST          → OpenAPI
Async events  → AsyncAPI / JSON Schema
GraphQL       → GraphQL schema
Database      → migrations/schema
```

### Step 6 — Implement With Selective Context

AI agents and contributors should follow `AGENTS.md`.

Do not provide the entire documentation tree to an agent unless the task genuinely requires it.

---

## 6. Requirement IDs

Use stable requirement identifiers for important feature behavior.

Recommended format:

```text
FR-<FEATURE>-<NUMBER>
```

Examples:

```text
FR-AUTH-001
FR-CHECKOUT-004
FR-PAYMENT-012
```

Rules:

- IDs are stable after publication.
- Removed IDs are not reused.
- Tests, API operations, ADRs, or issues may reference these IDs.
- Do not create IDs for trivial implementation details.

---

## 7. Architecture Decision Records

Create an ADR when a decision is:

- difficult or expensive to reverse,
- affects several features or modules,
- introduces a major dependency,
- changes a system boundary,
- changes a persistence or integration strategy,
- changes deployment architecture,
- changes a security model.

Do not create ADRs for routine coding decisions.

---

## 8. Project Profiles

The baseline structure is intended for fullstack products. Optional profiles may add or remove documentation.

### Fullstack

Default profile.

### Backend Service

Frontend and design documentation may be omitted.

### Frontend Application

Backend implementation standards may be reduced, while contracts remain important.

### SaaS

Add stronger guidance for tenancy, billing, deployment, operations, and data isolation.

### Event-Driven

Add event catalog, AsyncAPI, retry, idempotency, ordering, and DLQ rules.

### AI-Enabled

Add model/provider architecture, evaluation, prompt/versioning, privacy, and AI safety rules.

### Open Source

Add governance, release notes, contribution, licensing, and compatibility policies.

### Regulated

Add formal traceability, audit evidence, compliance controls, and stricter release gates.

---

## 9. Definition of Done

A feature is not complete only because its code compiles.

At minimum, applicable items should be true:

- feature behavior matches its specification;
- relevant API/event contracts are synchronized;
- architecture boundaries are respected;
- migrations are safe and reversible where appropriate;
- relevant automated tests pass;
- security-sensitive paths are reviewed;
- observability is sufficient for important production behavior;
- documentation affected by the change is updated;
- known limitations are recorded;
- release-impacting changes are documented.

The exact project-specific Definition of Done belongs in `docs/standards/01_ENGINEERING_WORKFLOW.md`.

---

## 10. Template Philosophy

This repository is not intended to maximize documentation.

It is intended to maximize **shared understanding with minimum duplication**.

If a document no longer helps product or engineering decisions, simplify it.

If the same fact exists in multiple documents, select one authoritative source and replace the others with references.
