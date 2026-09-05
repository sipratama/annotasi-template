# Product Brief — <PROJECT_NAME>

> **Document role:** Authoritative source for **why this product exists, who it serves, what outcomes it targets, and which business/product constraints shape it**.
>
> Detailed feature behavior belongs in the PRD and feature specifications. Technical design belongs in architecture documentation.

---

## Document Metadata

| Field | Value |
|---|---|
| Product | `<PROJECT_NAME>` |
| Status | Draft / Review / Locked |
| Version | `0.1` |
| Owner | `<OWNER>` |
| Last Updated | `<YYYY-MM-DD>` |
| Primary Market | `<MARKET>` |

---

## 1. Product Vision

### Vision

<Describe the long-term change this product should create in one short paragraph.>

### Product Statement

For `<TARGET_USERS>` who `<CORE_NEED>`, `<PROJECT_NAME>` is a `<PRODUCT_CATEGORY>` that `<PRIMARY_VALUE>`. Unlike `<ALTERNATIVE_OR_STATUS_QUO>`, it `<KEY_DIFFERENTIATOR>`.

---

## 2. Problem

### Core Problem

<Describe the primary problem in user or business terms. Do not describe the planned solution yet.>

### Why It Matters

<Explain the cost, friction, missed opportunity, risk, or user pain created by the problem.>

### Current Alternatives

How do users solve this today?

- `<ALTERNATIVE_1>`
- `<ALTERNATIVE_2>`
- `<MANUAL_WORKAROUND>`
- `<DO_NOTHING / STATUS_QUO>`

### Evidence

List the evidence currently available.

| Evidence | Source | Confidence |
|---|---|---|
| `<OBSERVATION>` | `<INTERVIEW / DATA / EXPERIENCE / RESEARCH>` | Low / Medium / High |

Do not present unvalidated assumptions as established facts.

---

## 3. Target Users

### Primary User

**Who:** `<PRIMARY_USER>`

**Context:**  
<When and where does this user experience the problem?>

**Primary job-to-be-done:**  
> When `<SITUATION>`, I want to `<MOTIVATION>`, so I can `<EXPECTED_OUTCOME>`.

### Secondary Users

| User | Need | Why They Matter |
|---|---|---|
| `<USER>` | `<NEED>` | `<RATIONALE>` |

### Explicitly Not Targeted Yet

- `<USER_SEGMENT>`
- `<USER_SEGMENT>`

---

## 4. Value Proposition

### Primary Value

<What useful outcome does the product create?>

### Differentiation

Why should the target user choose this product instead of the current alternative?

1. `<DIFFERENTIATOR>`
2. `<DIFFERENTIATOR>`
3. `<DIFFERENTIATOR>`

### Product Promise

> `<ONE-SENTENCE PROMISE>`

The promise should describe an outcome, not a feature list.

---

## 5. Desired Outcomes

### User Outcomes

- `<USER_OUTCOME_1>`
- `<USER_OUTCOME_2>`
- `<USER_OUTCOME_3>`

### Business / Product Outcomes

- `<BUSINESS_OUTCOME_1>`
- `<BUSINESS_OUTCOME_2>`

---

## 6. Goals

Goals should describe measurable or observable outcomes.

### G-01 — `<GOAL_NAME>`

**Goal:**  
<Description>

**Evidence of success:**  
<Metric or observable condition>

### G-02 — `<GOAL_NAME>`

**Goal:**  
<Description>

**Evidence of success:**  
<Metric or observable condition>

---

## 7. Non-Goals

The following are intentionally outside the current product direction or current phase.

- `<NON_GOAL_1>`
- `<NON_GOAL_2>`
- `<NON_GOAL_3>`

Non-goals prevent AI agents and contributors from expanding scope accidentally.

---

## 8. Product Principles

These principles guide product decisions when detailed requirements are incomplete.

### P-01 — `<PRINCIPLE_NAME>`

<Short explanation.>

### P-02 — `<PRINCIPLE_NAME>`

<Short explanation.>

### P-03 — `<PRINCIPLE_NAME>`

<Short explanation.>

Example principles:

- outcome before feature count;
- user control before automation;
- progressive disclosure before overwhelming configuration;
- safe defaults before maximum flexibility.

Use only principles that genuinely apply.

---

## 9. MVP Boundary

### In Scope

The MVP must prove:

- `<CAPABILITY / HYPOTHESIS>`
- `<CAPABILITY / HYPOTHESIS>`
- `<CAPABILITY / HYPOTHESIS>`

### Out of Scope

The MVP will not include:

- `<CAPABILITY>`
- `<CAPABILITY>`
- `<CAPABILITY>`

### MVP Exit Condition

The MVP is considered validated enough to move forward when:

<Describe the evidence required to justify the next investment stage.>

---

## 10. Business Model

Complete only when relevant.

### Monetization

`<FREE / ONE-TIME / SUBSCRIPTION / TRANSACTION / B2B / OTHER>`

### Payer

`<WHO PAYS>`

### Pricing Assumption

`<CURRENT ASSUMPTION>`

### Cost Drivers

- `<INFRASTRUCTURE>`
- `<THIRD-PARTY SERVICE>`
- `<OPERATIONS>`
- `<SUPPORT>`

Do not treat pricing assumptions as final product requirements.

---

## 11. Success Metrics

Prefer a small number of metrics that indicate real product value.

### Primary Metric

| Metric | Definition | Target / Direction |
|---|---|---|
| `<METRIC>` | `<HOW IT IS CALCULATED>` | `<TARGET>` |

### Supporting Metrics

| Metric | Why It Matters |
|---|---|
| `<METRIC>` | `<RATIONALE>` |
| `<METRIC>` | `<RATIONALE>` |

### Guardrail Metrics

Metrics that should not degrade while optimizing the primary metric.

| Metric | Guardrail |
|---|---|
| `<METRIC>` | `<LIMIT OR EXPECTATION>` |

---

## 12. Constraints

### Product Constraints

- `<CONSTRAINT>`

### Business Constraints

- `<CONSTRAINT>`

### Legal / Compliance Constraints

- `<CONSTRAINT OR N/A>`

### Technical Constraints

Only include constraints that materially shape the product, such as:

- mandatory integration;
- platform restriction;
- data residency requirement;
- offline requirement;
- compatibility requirement.

Detailed architecture choices do not belong here.

---

## 13. Dependencies

External conditions required for the product to succeed.

| Dependency | Why Needed | Risk |
|---|---|---|
| `<DEPENDENCY>` | `<RATIONALE>` | Low / Medium / High |

---

## 14. Assumptions

Assumptions are beliefs that still require validation.

| ID | Assumption | Validation Method | Status |
|---|---|---|---|
| A-01 | `<ASSUMPTION>` | `<HOW TO TEST>` | Open |
| A-02 | `<ASSUMPTION>` | `<HOW TO TEST>` | Open |

---

## 15. Open Product Questions

Only unresolved product-level questions belong here.

| ID | Question | Owner | Target Decision |
|---|---|---|---|
| Q-01 | `<QUESTION>` | `<OWNER>` | `<DATE / MILESTONE>` |

When resolved, move the resulting decision into the appropriate authoritative document.

---

## 16. Related Documents

- Product Requirements: `./PRD.md`
- Product Roadmap: `./ROADMAP.md`
- Feature Specifications: `../01_features/`
- System Architecture: `../02_architecture/SYSTEM_ARCHITECTURE.md`
- Risks: `../06_delivery/RISKS.md`

---

## 17. Change Log

| Version | Date | Change | Author |
|---|---|---|---|
| 0.1 | `<YYYY-MM-DD>` | Initial draft | `<AUTHOR>` |
