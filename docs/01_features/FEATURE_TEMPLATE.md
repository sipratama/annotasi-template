# Feature Specification — <FEATURE_NAME>

> **Document role:** Authoritative source for the detailed behavior of one product feature.
>
> Product-level scope belongs in the PRD. Cross-cutting technical design belongs in System Architecture or ADRs. Public interface definitions belong in machine-readable contracts.

---

## Document Metadata

| Field | Value |
|---|---|
| Feature ID | `<FEATURE_ID>` |
| Feature Name | `<FEATURE_NAME>` |
| Status | Draft / Review / Locked / Deprecated |
| Owner | `<OWNER>` |
| Priority | P0 / P1 / P2 |
| Target Release | `<RELEASE / MILESTONE>` |
| Last Updated | `<YYYY-MM-DD>` |

### Related Sources

- PRD: `<LINK OR SECTION>`
- Architecture: `<LINK OR SECTION>`
- ADRs: `<LINKS>`
- API Contract: `<LINK>`
- Event Contract: `<LINK>`
- UX Flow / Design: `<LINK>`

---

## 1. Feature Intent

### Problem Addressed

<What user or product problem does this feature address?>

### Desired Outcome

<What should become possible or better after this feature exists?>

### Actors

| Actor | Role in Feature |
|---|---|
| `<ACTOR>` | `<ROLE>` |

---

## 2. Scope

### In Scope

- `<BEHAVIOR>`
- `<BEHAVIOR>`

### Out of Scope

- `<BEHAVIOR>`
- `<BEHAVIOR>`

Out-of-scope items should not be implemented opportunistically.

---

## 3. User Flow

Describe the primary flow before listing detailed requirements.

```text
<START>
   ↓
<STEP>
   ↓
<DECISION>
  ↙   ↘
<A>   <B>
   ↓
<END>
```

### Primary Flow

1. `<STEP>`
2. `<STEP>`
3. `<STEP>`

### Alternate Flows

#### AF-01 — `<NAME>`

1. `<STEP>`
2. `<STEP>`

---

## 4. Functional Requirements

Use stable IDs.

### FR-<FEATURE>-001 — `<REQUIREMENT_TITLE>`

**Requirement**  
<Describe observable behavior, not implementation details.>

**Rationale**  
<Why this behavior matters.>

**Acceptance Criteria**

- Given `<PRECONDITION>`, when `<ACTION>`, then `<OUTCOME>`.
- Given `<PRECONDITION>`, when `<ACTION>`, then `<OUTCOME>`.

**Priority**  
P0 / P1 / P2

---

### FR-<FEATURE>-002 — `<REQUIREMENT_TITLE>`

**Requirement**  
<Description>

**Acceptance Criteria**

- Given `<PRECONDITION>`, when `<ACTION>`, then `<OUTCOME>`.

**Priority**  
P0 / P1 / P2

---

## 5. Business Rules

Rules should be deterministic and testable.

| ID | Rule |
|---|---|
| BR-01 | `<RULE>` |
| BR-02 | `<RULE>` |

Examples:

- an order cannot move from `CANCELLED` back to `PAID`;
- only the owner or an administrator may edit a private resource;
- a promotion is valid only inside its configured campaign window.

---

## 6. State Model

Use this section when the feature has meaningful lifecycle states.

### States

| State | Meaning | Allowed Next States |
|---|---|---|
| `<STATE>` | `<MEANING>` | `<STATE_2>, <STATE_3>` |

### State Invariants

- `<INVARIANT>`
- `<INVARIANT>`

If the lifecycle is complex, add a state diagram.

---

## 7. Permissions and Authorization

| Action | Actor / Role | Condition |
|---|---|---|
| `<ACTION>` | `<ROLE>` | `<CONDITION>` |

Authorization rules must be enforced server-side when the backend is the security boundary.

Frontend visibility rules are not a substitute for authorization.

---

## 8. Data Requirements

Describe product-relevant data, not physical database design.

### Inputs

| Field / Concept | Required | Rules |
|---|---:|---|
| `<INPUT>` | Yes / No | `<VALIDATION>` |

### Outputs

| Field / Concept | Description |
|---|---|
| `<OUTPUT>` | `<DESCRIPTION>` |

### Sensitive Data

Identify personal, confidential, financial, credential, or otherwise sensitive information handled by this feature.

`<NONE / DESCRIPTION>`

Physical schema belongs in the data model and migrations.

---

## 9. API and Integration Dependencies

Do not duplicate full interface definitions here. Link to contracts.

### APIs

| Operation | Contract | Purpose |
|---|---|---|
| `<METHOD / OPERATION>` | `<OPENAPI LINK>` | `<PURPOSE>` |

### Events

| Event | Direction | Contract | Purpose |
|---|---|---|---|
| `<EVENT>` | Produce / Consume | `<SCHEMA LINK>` | `<PURPOSE>` |

### External Services

| Service | Purpose | Failure Impact |
|---|---|---|
| `<SERVICE>` | `<PURPOSE>` | `<IMPACT>` |

---

## 10. UX and UI States

Describe states that the user must experience correctly.

### Required States

- Default
- Loading
- Empty
- Success
- Validation error
- Server error
- Unauthorized / forbidden, if applicable
- Offline / degraded, if applicable

### UX Rules

- `<RULE>`
- `<RULE>`

### Accessibility

- `<KEYBOARD / SCREEN READER / FOCUS / CONTRAST REQUIREMENT>`

Visual tokens and reusable component rules belong in `DESIGN_SYSTEM.md`.

---

## 11. Failure and Edge Cases

| ID | Scenario | Expected Behavior |
|---|---|---|
| EC-01 | `<SCENARIO>` | `<EXPECTED BEHAVIOR>` |
| EC-02 | `<SCENARIO>` | `<EXPECTED BEHAVIOR>` |

Consider where relevant:

- duplicate requests;
- retries;
- partial failures;
- timeouts;
- race conditions;
- stale data;
- expired credentials;
- invalid state transitions;
- unavailable dependencies;
- malformed input;
- large input;
- repeated user action.

---

## 12. Security and Privacy

### Threat-Sensitive Behavior

- `<AUTHENTICATION / AUTHORIZATION / INPUT / FILE / PAYMENT / ETC.>`

### Security Requirements

- `<REQUIREMENT>`
- `<REQUIREMENT>`

### Privacy Requirements

- `<RETENTION / MASKING / CONSENT / DATA MINIMIZATION / N/A>`

If this feature creates a new trust boundary or material threat, update the project threat model.

---

## 13. Observability

Define what is necessary to understand important production behavior.

### Logs

- `<IMPORTANT STRUCTURED EVENT>`

### Metrics

- `<METRIC>`

### Traces

- `<IMPORTANT SPAN / EXTERNAL CALL>`

### Business Events

- `<PRODUCT OR DOMAIN EVENT>`

Do not include sensitive values in telemetry.

---

## 14. Test Scenarios

Tests should reference requirement IDs where practical.

| Test ID | Requirement | Level | Scenario |
|---|---|---|---|
| T-001 | `FR-<FEATURE>-001` | Unit / Integration / E2E / Contract | `<SCENARIO>` |

### Minimum Regression Coverage

- `<CRITICAL PATH>`
- `<FAILURE PATH>`
- `<PERMISSION PATH>`

---

## 15. Rollout and Migration

Complete when the feature affects production rollout.

### Rollout Strategy

`<DIRECT / FEATURE FLAG / PHASED / CANARY / OTHER>`

### Data Migration

`<NONE / DESCRIPTION>`

### Backward Compatibility

`<NOT APPLICABLE / REQUIREMENTS>`

### Rollback / Recovery

`<STRATEGY>`

---

## 16. Dependencies

### Upstream

- `<FEATURE / SERVICE / CONTRACT>`

### Downstream

- `<FEATURE / SERVICE / CONSUMER>`

---

## 17. Open Questions

| ID | Question | Owner | Blocking? |
|---|---|---|---|
| Q-01 | `<QUESTION>` | `<OWNER>` | Yes / No |

Do not hide unresolved product decisions inside implementation comments.

---

## 18. Definition of Done

The feature is complete when all applicable conditions are satisfied:

- [ ] P0 requirements are implemented.
- [ ] Acceptance criteria pass.
- [ ] Relevant API/event contracts are synchronized.
- [ ] Authorization rules are enforced.
- [ ] Required UI states are implemented.
- [ ] Relevant automated tests pass.
- [ ] Important failure cases are covered.
- [ ] Observability is sufficient.
- [ ] Security/privacy implications are addressed.
- [ ] Migrations and rollout steps are ready if required.
- [ ] Documentation affected by the feature is current.
- [ ] Known limitations are recorded.

---

## 19. Change Log

| Version | Date | Change | Author |
|---|---|---|---|
| 0.1 | `<YYYY-MM-DD>` | Initial draft | `<AUTHOR>` |
