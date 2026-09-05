# AGENTS.md

Repository-wide instructions for AI coding agents and automated engineering assistants.

This file is intentionally small. It defines **how to work in this repository**, not every engineering rule. Detailed guidance belongs in `docs/standards/` and should be loaded only when relevant.

## 1. Core Rule

Do not treat chat history, assumptions, generated code, or current implementation as a substitute for authoritative project documentation.

Before a non-trivial change, determine:
1. what behavior is requested;
2. which source owns that behavior;
3. which architecture boundaries apply;
4. which contracts or persistent data may change;
5. which standards apply;
6. what evidence is required for completion.

Do not silently invent product or architecture decisions.

### Initialization Trigger

If this repository still contains project-template placeholders such as `<PROJECT_NAME>` and the task is to start/adapt a new project, read `docs/PROJECT_INITIALIZATION.md` before normal feature implementation.

Do not treat template placeholder content as confirmed project facts.

## 2. Source of Truth

| Concern | Authoritative Source |
|---|---|
| Product purpose, users, outcomes, constraints | `docs/00_product/PRODUCT_BRIEF.md` |
| Product capabilities and scope | `docs/00_product/PRD.md` |
| Detailed feature behavior | `docs/01_features/<feature>.md` |
| System structure and boundaries | `docs/02_architecture/SYSTEM_ARCHITECTURE.md` |
| Architecture rationale | `docs/02_architecture/adr/` |
| Persistent domain model | migrations/schema + `docs/02_architecture/DATA_MODEL.md` |
| REST interface | `contracts/openapi/` when used |
| Async/event interface | `contracts/asyncapi/` or schemas when used |
| UI system | `docs/03_design/DESIGN_SYSTEM.md` + relevant feature spec |
| Engineering rules | `docs/standards/` |
| Test approach | `docs/04_engineering/TEST_STRATEGY.md` + relevant feature spec |
| Runtime and deployment | `docs/05_operations/` |

When sources conflict, follow the source that owns the concern, or update that source when the requested change intentionally changes the decision.

## 3. Read Selectively

Do **not** read all project documentation by default.

Default context order:
1. `AGENTS.md`
2. relevant PRD section
3. relevant feature spec
4. relevant System Architecture section
5. relevant ADRs
6. relevant contracts
7. relevant engineering standards
8. related source code and tests

Read `PRODUCT_BRIEF.md` when product intent, users, goals, scope, or non-goals matter. Read operations docs only when configuration, deployment, runtime, or release behavior is affected.

## 4. Standards Routing

Load only standards relevant to the task.

| Area | Standard |
|---|---|
| Workflow / review | `docs/standards/01_ENGINEERING_WORKFLOW.md` |
| Code quality | `docs/standards/02_CODE_QUALITY.md` |
| Architecture | `docs/standards/03_ARCHITECTURE.md` |
| Backend | `docs/standards/04_BACKEND_STANDARD.md` |
| Frontend | `docs/standards/05_FRONTEND_STANDARD.md` |
| API / integrations / events | `docs/standards/06_API_INTEGRATION_STANDARD.md` |
| Database / persistence | `docs/standards/07_DATA_PERSISTENCE_STANDARD.md` |
| Security | `docs/standards/08_SECURITY_STANDARD.md` |
| Testing | `docs/standards/09_TESTING_STANDARD.md` |
| Reliability / observability | `docs/standards/10_OBSERVABILITY_RELIABILITY.md` |
| Performance | `docs/standards/11_PERFORMANCE_STANDARD.md` |
| Dependencies / supply chain | `docs/standards/12_DEPENDENCY_SUPPLY_CHAIN.md` |
| CI/CD / release | `docs/standards/13_CI_CD_RELEASE.md` |
| AI-assisted development | `docs/standards/14_AI_ASSISTED_DEVELOPMENT.md` |

## 5. Before Coding

For non-trivial work, identify:
- requirement or feature IDs;
- likely files to change;
- affected API/event contracts;
- affected schema or migrations;
- affected architecture boundaries;
- applicable standards;
- security, reliability, or compatibility implications;
- required tests.

Prefer the smallest coherent change that satisfies the requirement. Do not perform unrelated refactoring or broaden scope because an adjacent improvement is possible.

## 6. Change Discipline

### Product and Feature Behavior

When observable behavior changes:
- update the relevant PRD or feature spec;
- preserve stable requirement IDs when the requirement remains the same;
- create new IDs for genuinely new behavior;
- never reuse retired IDs;
- keep tests aligned with the specification.

### Architecture

Do not change major architecture implicitly. Create or update an ADR when a decision materially changes:
- system or module boundaries;
- strategic frameworks, datastores, brokers, or providers;
- sync vs async interaction;
- deployment topology;
- authentication or authorization strategy;
- persistence strategy;
- major reliability/scalability behavior;
- a decision that is expensive to reverse.

Routine implementation choices do not require ADRs.

### Contracts

Public and cross-component interfaces are contract-first:
- REST changes → update OpenAPI;
- event changes → update AsyncAPI/schema;
- persistent schema changes → add version-controlled migration;
- breaking changes → document consumer impact and rollout strategy.

Do not silently rename, remove, or invent contract fields.

## 7. Non-Negotiable Guardrails

Do not:
- invent requirements or silently change scope;
- silently change architecture or public contracts;
- bypass validation or authorization to simplify implementation;
- disable security controls or meaningful tests to make a build pass;
- commit/hard-code secrets or log sensitive credentials/tokens/keys;
- introduce destructive data changes without a migration or rollout strategy;
- mix unrelated refactors into requested work;
- introduce project-wide abstractions for hypothetical future needs;
- claim work or tests are complete without evidence.

Architecture invariants remain binding unless an accepted ADR changes them.

## 8. Documentation Synchronization

Update documentation only when the change makes its authoritative source inaccurate.

| Change | Update |
|---|---|
| Product capability/scope | `docs/00_product/PRD.md` |
| Detailed feature behavior | relevant feature spec |
| Architecture decision | ADR |
| System/module boundary | System Architecture |
| REST contract | OpenAPI |
| Event contract | AsyncAPI/schema |
| Persistent model | migration/schema + Data Model |
| Runtime configuration | Configuration |
| Security/trust boundary | Threat Model |
| Operational procedure | Runbook |
| Unsupported behavior | Known Limitations |

Do not duplicate the same fact across documents. Link to the authoritative source instead.

## 9. Incomplete Specifications

If implementation details are missing but the behavior fits existing architecture and patterns, use the established approach.

Do **not** silently guess when a missing decision materially affects product behavior, security/privacy, public contracts, data integrity, major architecture, or destructive/irreversible migration.

Surface the unresolved decision explicitly. Temporary assumptions must be labeled and must not become accidental architecture.

## 10. Testing and Evidence

Use the smallest meaningful test set while iterating, then run broader checks required by affected standards before completion.

Tests should prove behavior, contracts, and important failure paths. For defect fixes, add regression coverage when practical.

Never delete or weaken a meaningful failing test solely to make the build pass. Do not claim a command or test passed unless it was actually executed.

## 11. Completion Report

For non-trivial work, report:
- **Changed** — behavior or structure changed.
- **Requirements** — relevant IDs/spec sections.
- **Contracts / Data** — API, event, schema, or migration changes.
- **Tests** — commands/checks executed and results.
- **Architecture** — ADR/architecture changes, or explicitly none.
- **Risks / Limitations** — unresolved, deferred, or out-of-scope items.

## 12. Definition of Done

A task is complete when all applicable conditions are satisfied:
- requested behavior is implemented;
- acceptance criteria are met;
- authoritative documentation is current;
- contracts and migrations are synchronized;
- architecture rules and accepted ADRs are respected;
- relevant tests pass;
- applicable security and reliability concerns are addressed;
- no unrelated scope was introduced;
- remaining limitations are explicit.

Project-specific standards may strengthen this definition.
