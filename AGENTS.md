# AGENTS.md

Instructions for AI coding agents and automated engineering assistants working in this repository.

This file defines how an agent should gather context, interpret project documentation, make changes, and report evidence.

It applies to Claude, Codex, and other AI-assisted development tools unless a tool-specific instruction explicitly overrides a non-project-critical behavior.

---

## 1. Primary Rule

Do not treat chat history, assumptions, generated code, or existing implementation as a substitute for the project's authoritative specifications.

Before changing code, determine:

1. what behavior is requested;
2. which document owns that behavior;
3. which architecture boundaries apply;
4. which contracts may be affected;
5. which tests are required.

Do not silently invent missing product or architecture decisions.

---

## 2. Read Selectively, Not Broadly

Do **not** read every document in the repository by default.

Start with the minimum context required for the task.

### Default Reading Order

1. `AGENTS.md`
2. relevant section of `docs/00_product/PRD.md`
3. relevant file under `docs/01_features/`
4. relevant section of `docs/02_architecture/SYSTEM_ARCHITECTURE.md`
5. relevant ADRs
6. relevant machine-readable contracts
7. relevant files under `docs/standards/`
8. source code related to the task

Read `PRODUCT_BRIEF.md` when the task depends on product intent, target users, scope, goals, or non-goals.

Read operational documentation only when the task affects configuration, deployment, runtime operations, or release behavior.

---

## 3. Source of Truth

Use the following authority model.

| Concern | Source of Truth |
|---|---|
| Product purpose, users, outcomes, constraints | `PRODUCT_BRIEF.md` |
| Product capabilities and scope | `PRD.md` |
| Detailed feature behavior | relevant feature spec |
| System structure and boundaries | `SYSTEM_ARCHITECTURE.md` |
| Architecture rationale | relevant ADR |
| REST contract | OpenAPI |
| Async/event contract | AsyncAPI / schema |
| Persistent schema | migrations/schema |
| UI system | `DESIGN_SYSTEM.md` + feature spec |
| Engineering rules | `docs/standards/` |
| Test approach | `TEST_STRATEGY.md` + feature spec |
| Deployment/runtime behavior | operations documentation |

When two sources conflict, do not silently choose whichever is easier to implement.

Identify the conflict and follow the more authoritative source for that concern. If the task explicitly changes the authoritative decision, update the source of truth as part of the work.

---

## 4. Before Coding

Before implementation, establish a compact working model.

For non-trivial tasks, identify:

- the feature or requirement IDs involved;
- files likely to change;
- affected contracts;
- affected database schema or migrations;
- affected architecture boundaries;
- required tests;
- security or reliability implications.

Do not perform unrelated refactoring unless it is necessary for the requested change.

Do not broaden scope merely because an adjacent improvement appears useful.

---

## 5. Requirement Changes

Feature behavior belongs in the relevant feature specification.

When behavior changes:

1. update the relevant requirement or acceptance criteria;
2. preserve stable requirement IDs whenever the underlying requirement remains the same;
3. create new IDs for genuinely new behavior;
4. do not reuse deleted requirement IDs;
5. update implementation and tests to match.

A code change that alters user-visible or externally observable behavior should not leave the corresponding feature specification stale.

---

## 6. Architecture Changes

Do not change major architecture implicitly.

Create or update an ADR when a change:

- alters a system or module boundary;
- introduces a strategic framework, datastore, broker, or provider;
- changes synchronization vs asynchronous processing;
- changes deployment topology;
- changes authentication or authorization strategy;
- changes persistence strategy;
- changes an important reliability or scalability approach;
- is expensive to reverse.

Routine implementation choices do not require an ADR.

When an existing ADR is superseded, preserve the old ADR and mark its status accordingly.

---

## 7. Contract-First Changes

Externally consumed contracts are authoritative interfaces.

### REST

Update OpenAPI before or together with implementation when request, response, status code, or endpoint behavior changes.

### Async Events

Update AsyncAPI or event schema before or together with producers and consumers.

### Database

Use migrations for persistent schema changes.

Never depend on undocumented manual database changes.

### Compatibility

For breaking changes:

- identify affected consumers;
- document migration or rollout strategy;
- prefer additive changes when practical;
- do not silently remove or rename public fields.

---

## 8. Backend Engineering Rules

When working on backend code:

- preserve domain and module boundaries;
- keep transport concerns out of domain logic where architecture requires separation;
- validate inputs at appropriate boundaries;
- define transaction boundaries explicitly;
- treat retries and idempotency as separate concerns;
- do not make remote calls inside database transactions unless architecture explicitly permits it;
- handle timeouts and partial failures deliberately;
- avoid leaking sensitive information through errors or logs;
- update migrations and data contracts when persistence changes;
- add observability for important business and failure paths;
- follow `docs/standards/04_BACKEND_STANDARD.md` when present.

Do not introduce a new architectural pattern solely to solve one local coding problem.

---

## 9. Frontend Engineering Rules

When working on frontend code:

- follow the design system and feature UX states;
- keep business behavior aligned with feature specs;
- distinguish server state from local UI state;
- implement loading, empty, success, validation, and error states where applicable;
- preserve accessibility and keyboard behavior;
- avoid duplicating server authorization logic as a security boundary;
- do not invent API fields that are absent from the contract;
- follow established component and feature boundaries;
- update frontend tests for changed behavior;
- follow `docs/standards/05_FRONTEND_STANDARD.md` when present.

UI convenience must not silently change product rules.

---

## 10. Security Rules

Security-sensitive changes require deliberate review.

Pay special attention to:

- authentication;
- authorization;
- sessions and tokens;
- secrets;
- personal or sensitive data;
- file upload;
- user-generated content;
- payments;
- administrative actions;
- third-party integrations;
- deserialization and parsing;
- SQL/query construction;
- redirects and callback URLs.

Never commit secrets.

Never log credentials, tokens, private keys, full sensitive payloads, or unnecessary personal data.

When a change introduces a new trust boundary or material threat, update the threat model.

---

## 11. Database and Migration Rules

When persistent data changes:

- use version-controlled migrations;
- assess backward compatibility;
- consider existing production data;
- add indexes intentionally;
- avoid destructive migration patterns without a rollout plan;
- separate schema migration from large data backfills when appropriate;
- define rollback or recovery strategy when practical;
- keep code compatible with phased deployment when zero-downtime deployment is required.

Do not treat a successful migration on an empty local database as sufficient production evidence.

---

## 12. Testing Rules

Run the smallest meaningful test set during iteration, then the required broader checks before completion.

Depending on the change, testing may include:

- unit tests;
- integration tests;
- contract tests;
- component tests;
- end-to-end tests;
- architecture tests;
- security tests;
- migration tests;
- performance tests;
- smoke tests.

Tests should prove important behavior, not mirror implementation details.

When fixing a defect, add or update a regression test when practical.

Do not delete or weaken a failing test merely to make the build pass unless the requirement itself changed and the test is updated to the new expected behavior.

---

## 13. Observability and Reliability

For important production behavior, consider:

- structured logs;
- metrics;
- traces;
- correlation/request identifiers;
- actionable error classification;
- retry visibility;
- dead-letter handling;
- timeout behavior;
- health/readiness signals.

Do not log every internal detail by default.

Prefer signals that help answer:

- what failed?
- for which operation?
- how often?
- which dependency was involved?
- can the system recover automatically?
- is user or business data affected?

---

## 14. Documentation Synchronization

Update documentation when the change makes an authoritative document inaccurate.

Typical triggers:

| Change | Documentation |
|---|---|
| New product behavior | Feature spec / PRD |
| New architecture decision | ADR |
| New module boundary | System Architecture |
| API change | OpenAPI |
| Event change | AsyncAPI/schema |
| Persistent model change | migration + Data Model |
| New runtime configuration | Configuration |
| New security boundary | Threat Model |
| New known limitation | Known Limitations |
| New operational procedure | Runbook |

Do not update unrelated documents just to increase documentation coverage.

---

## 15. Implementation Discipline

Do not:

- invent requirements;
- silently change product scope;
- silently change architecture;
- silently change public contracts;
- bypass validation to simplify implementation;
- disable security controls to make tests pass;
- hard-code secrets;
- mix unrelated refactors into feature work;
- replace a working dependency without architectural justification;
- add abstraction only for hypothetical future needs;
- mark work complete without evidence.

Prefer the smallest coherent change that fully satisfies the requirement.

---

## 16. Completion Report

When completing a non-trivial task, report:

### Changed

What behavior or structure changed.

### Requirements

Relevant requirement IDs or feature spec sections.

### Contracts

Any API, event, or schema changes.

### Tests

Tests executed and their result.

### Architecture

Any ADR or architecture update.

### Risks / Limitations

Anything still unresolved, deferred, or requiring follow-up.

Do not claim tests passed unless they were actually executed.

---

## 17. Working With Incomplete Specifications

If implementation details are missing but product intent is clear, prefer the existing architecture and established patterns.

If a missing decision would materially affect:

- product behavior,
- security,
- public contracts,
- data integrity,
- major architecture,
- irreversible migration,

do not silently guess.

Record the unresolved decision and surface it explicitly.

Temporary implementation assumptions must be clearly labeled and should not become accidental architecture.

---

## 18. Definition of Done

A task is complete when applicable conditions are satisfied:

- requested behavior is implemented;
- acceptance criteria are met;
- contracts are synchronized;
- architecture rules are respected;
- migrations are included where required;
- relevant tests pass;
- security implications are addressed;
- relevant observability exists;
- affected documentation is current;
- known limitations are recorded;
- no unrelated scope is introduced.

Project-specific rules may strengthen this definition.
