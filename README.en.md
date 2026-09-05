# Annotasi Template

> 🇬🇧 English · [🇮🇩 Bahasa Indonesia](./README.md)

An **AI-ready, opinionated, production-oriented** software development template for fullstack, backend, and frontend product development.

Annotasi Template helps humans and AI coding agents such as **Codex** and **Claude Code** work from the same sources of truth—from product intent and feature behavior to architecture, contracts, engineering standards, and release evidence.

> The goal is not maximum documentation. The goal is **shared understanding with minimum duplication**.

---

## What problem does this template solve?

AI-assisted development can accelerate coding, but it creates risk when:

- requirements live only in chat history;
- architecture changes without explicit decisions;
- API contracts drift from implementation;
- agents load too much irrelevant context;
- business rules are duplicated across frontend, backend, and tests;
- a repository has many documents but no clear authority model.

Annotasi Template uses this flow:

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

## Core principles

### One Concern, One Source of Truth

| Question | Source of Truth |
|---|---|
| Why does the product exist and for whom? | `docs/00_product/PRODUCT_BRIEF.md` |
| Which product capabilities are required? | `docs/00_product/PRD.md` |
| How should one feature behave? | `docs/01_features/<feature>.md` |
| How is the system structured? | `docs/02_architecture/SYSTEM_ARCHITECTURE.md` |
| Why was an architecture decision made? | `docs/02_architecture/adr/` |
| What quality targets are required? | `docs/02_architecture/NON_FUNCTIONAL_REQUIREMENTS.md` |
| What is the persistent data model? | migrations/schema + `DATA_MODEL.md` |
| What are the REST/event contracts? | `contracts/` when applicable |
| How should engineering be performed? | `docs/standards/` |
| How is testing planned? | `docs/04_engineering/TEST_STRATEGY.md` |
| How is the system released/operated? | `docs/05_operations/` + `docs/06_delivery/` |

### AI agents read selectively

```text
AGENTS.md
   ↓
relevant PRD section
   ↓
relevant feature spec
   ↓
relevant architecture / ADR
   ↓
relevant contract
   ↓
relevant engineering standard
   ↓
source code + tests
```

### Contracts before implementation drift

Changes to APIs, events, schemas, or persistent formats should update their contract/migration before or together with implementation.

### Architecture decisions are explicit

Material architecture decisions belong in ADRs, not only in code or chat history.

---

## Quick Start

### 1. Create a repository from this template

Recommended: enable **Template repository** in GitHub settings and use **Use this template**.

### 2. Run guided initialization

Open the new project with Codex or Claude Code and use:

```text
Initialize this repository as a new project using AGENTS.md and
docs/PROJECT_INITIALIZATION.md.

Use existing repository evidence and the context I provide.
Do not invent missing product decisions.

Project: <project name>
Profile: <fullstack | backend-service | frontend-app | prototype>
Modifiers: <saas | event-driven | ai-enabled | open-source | regulated | none>

After initialization:
- summarize the selected document profile,
- report unresolved product/architecture decisions,
- report files created/removed/updated,
- run the template/project validation checks where possible.
```

See [`docs/PROJECT_INITIALIZATION.md`](./docs/PROJECT_INITIALIZATION.md).

### 3. Start feature development

Copy `docs/01_features/FEATURE_TEMPLATE.md`, create stable requirement IDs such as `FR-PAYMENT-001`, and follow `AGENTS.md` for selective context routing.

---

## Template repository structure

The template itself provides:

```text
.
├── README.md
├── README.en.md
├── AGENTS.md
├── CLAUDE.md
│
├── docs/
│   ├── PROJECT_INITIALIZATION.md
│   ├── 00_product/
│   ├── 01_features/
│   ├── 02_architecture/
│   ├── 03_design/
│   ├── 04_engineering/
│   ├── 05_operations/
│   ├── 06_delivery/
│   └── standards/
│
└── scripts/
    └── validate_template.py
```

Directories such as `src/`, `backend/`, `frontend/`, `contracts/openapi/`, `contracts/asyncapi/`, migrations, and deployment manifests are created according to project needs rather than forced by the template.

---

## Required vs conditional documents

### Core

- `README.md`
- `AGENTS.md` for AI-assisted projects
- `PRODUCT_BRIEF.md`
- `PRD.md` for non-trivial products
- `SYSTEM_ARCHITECTURE.md` for non-trivial software
- `FEATURE_TEMPLATE.md`
- `ADR_TEMPLATE.md`
- `docs/standards/` retained and loaded selectively

### Conditional

- `ROADMAP.md` — multiple milestones/directions
- `DATA_MODEL.md` — persistent/domain data
- `NON_FUNCTIONAL_REQUIREMENTS.md` — explicit quality targets
- `UX_FLOWS.md` / `DESIGN_SYSTEM.md` — user-facing UI
- `TEST_STRATEGY.md` — multi-layer testing
- `THREAT_MODEL.md` — meaningful trust/security boundaries
- operations docs — deployed/operated systems
- delivery docs — material risks, releases, known limitations

Engineering standards remain in the repository even when they are not loaded for every task.

---

## Project profiles

Base profiles:

- `fullstack`
- `backend-service`
- `frontend-app`
- `prototype`

Optional modifiers:

- `saas`
- `event-driven`
- `ai-enabled`
- `open-source`
- `regulated`

See `docs/PROJECT_INITIALIZATION.md` for the activation matrix.

---

## Codex and Claude

`AGENTS.md` is the canonical repository-wide instruction source.

`CLAUDE.md` remains a thin Claude Code adapter importing:

```text
@AGENTS.md
```

Detailed AI-specific engineering behavior lives in:

```text
docs/standards/14_AI_ASSISTED_DEVELOPMENT.md
```

---

## Language policy

Human-facing product thinking uses Indonesian or Indonesian/English technical vocabulary:

- primary `README.md`
- initialization
- Product Brief
- PRD
- Roadmap
- Feature Spec template
- UX Flows
- Design System

Engineering and machine-oriented artifacts use English:

- `AGENTS.md`
- `CLAUDE.md`
- architecture and ADRs
- engineering/security/testing/operations docs
- engineering standards
- source code and schemas/contracts

Only the README is mirrored bilingually. Other specifications keep one canonical language to avoid drift.

---

## Requirement IDs

```text
FR-<FEATURE>-<NUMBER>
```

Examples:

```text
FR-AUTH-001
FR-CHECKOUT-004
FR-PAYMENT-012
```

IDs remain stable across refactoring and retired IDs are not reused.

---

## Versioning

Use Git Tags and GitHub Releases for template versions. Repository/folder names do not need embedded version numbers.

---

## Validation

Template mode:

```bash
python scripts/validate_template.py
```

Initialized project mode:

```bash
python scripts/validate_template.py --project-mode
```

The validator checks basic structure and local Markdown links. It does not replace content review.

---

## Philosophy

1. **Keep the source of truth clear.**
2. **Delete or ignore what does not help delivery.**
3. **Load only the context needed for the current task.**

AI accelerates implementation; it does not own product truth.
