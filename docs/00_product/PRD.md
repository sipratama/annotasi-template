# Product Requirements Document (PRD) — <PROJECT_NAME>

> **Peran dokumen:** Source of truth untuk **apa yang harus disediakan oleh produk pada level product capability, scope, user journey, dan outcome**.
>
> Masalah, target user, value proposition, dan product principles berasal dari `PRODUCT_BRIEF.md`. Detail perilaku satu feature berada di `docs/01_features/<feature>.md`. Detail teknis berada di dokumen architecture, ADR, dan machine-readable contracts.

---

## Metadata Dokumen

| Field | Value |
|---|---|
| Product | `<PROJECT_NAME>` |
| Status | Draft / Review / Locked |
| Version | `0.1` |
| Owner | `<OWNER>` |
| Last Updated | `<YYYY-MM-DD>` |
| Target Release / Phase | `<MILESTONE>` |

---

## 1. Ringkasan Produk

### Product Summary

<Jelaskan produk dalam 2–4 kalimat. Fokus pada apa yang pengguna dapat lakukan dan outcome yang ingin dicapai.>

### Product Goal

Produk ini bertujuan untuk:

1. `<GOAL>`
2. `<GOAL>`
3. `<GOAL>`

### Referensi Product Brief

Dokumen ini harus konsisten dengan:

`./PRODUCT_BRIEF.md`

Jika product intent berubah secara material, update `PRODUCT_BRIEF.md` terlebih dahulu atau bersamaan dengan PRD.

---

## 2. Target User dan Actors

Jangan mengulang persona panjang dari Product Brief. Hanya catat actor yang relevan dengan product behavior.

| Actor | Tujuan Utama | Akses / Responsibility |
|---|---|---|
| `<ACTOR>` | `<GOAL>` | `<SCOPE>` |
| `<ACTOR>` | `<GOAL>` | `<SCOPE>` |

---

## 3. Product Scope

### In Scope

Product capability yang termasuk dalam fase ini:

- `<CAPABILITY>`
- `<CAPABILITY>`
- `<CAPABILITY>`

### Out of Scope

Hal-hal berikut tidak termasuk dalam fase ini:

- `<OUT_OF_SCOPE>`
- `<OUT_OF_SCOPE>`
- `<OUT_OF_SCOPE>`

Out-of-scope item tidak boleh diimplementasikan secara opportunistic tanpa perubahan product scope.

---

## 4. Product Capabilities

Gunakan stable capability ID.

Format yang disarankan:

```text
CAP-<DOMAIN>-<NUMBER>
```

Contoh:

```text
CAP-AUTH-001
CAP-LEARNING-002
CAP-COMMERCE-003
```

### CAP-<DOMAIN>-001 — <CAPABILITY_NAME>

**Deskripsi**  
<Jelaskan capability dari sudut pandang produk.>

**User Outcome**  
<Outcome yang diterima pengguna.>

**Primary Actors**
- `<ACTOR>`

**Priority**  
P0 / P1 / P2

**Related Feature Specs**
- `../01_features/<feature>.md`

---

### CAP-<DOMAIN>-002 — <CAPABILITY_NAME>

**Deskripsi**  
<Deskripsi>

**User Outcome**  
<Outcome>

**Priority**  
P0 / P1 / P2

**Related Feature Specs**
- `../01_features/<feature>.md`

---

## 5. Primary User Journeys

PRD menjelaskan journey lintas-feature. Detail behavior per feature tetap berada di feature specification.

### Journey J-01 — <JOURNEY_NAME>

**Actor:** `<ACTOR>`

**Goal:** `<GOAL>`

```text
<ENTRY>
   ↓
<STEP>
   ↓
<STEP>
   ↓
<OUTCOME>
```

**Success Condition**
- `<CONDITION>`

**Related Capabilities**
- `CAP-...`
- `CAP-...`

---

### Journey J-02 — <JOURNEY_NAME>

**Actor:** `<ACTOR>`

**Goal:** `<GOAL>`

**Success Condition**
- `<CONDITION>`

---

## 6. Product Rules

Gunakan bagian ini hanya untuk aturan lintas-feature atau product-wide.

| ID | Rule |
|---|---|
| PR-001 | `<PRODUCT-WIDE RULE>` |
| PR-002 | `<PRODUCT-WIDE RULE>` |

Aturan yang hanya berlaku pada satu feature harus berada di feature spec.

---

## 7. Roles and Permissions Overview

Ini adalah overview product-level, bukan security implementation.

| Capability / Action | `<ROLE_A>` | `<ROLE_B>` | `<ROLE_C>` |
|---|---:|---:|---:|
| `<ACTION>` | Yes | No | Yes |
| `<ACTION>` | Own only | All | No |

Detailed authorization rules tetap berada di feature spec dan security/architecture documentation.

---

## 8. UX Requirements

### Experience Principles

- `<PRINCIPLE>`
- `<PRINCIPLE>`

### Required Cross-Product States

Aplikasi harus menangani state yang relevan secara konsisten:

- loading;
- empty;
- success;
- validation error;
- server/dependency error;
- unauthorized/forbidden;
- offline/degraded state jika applicable.

### Responsive and Accessibility Expectations

- `<REQUIREMENT>`
- `<REQUIREMENT>`

Detailed UI patterns dan design tokens berada di `DESIGN_SYSTEM.md`.

---

## 9. Notifications and User Communication

Gunakan jika produk memiliki notification, email, push, in-app alert, atau transactional communication.

| Trigger | Audience | Channel | Purpose |
|---|---|---|---|
| `<TRIGGER>` | `<ACTOR>` | Email / Push / In-app | `<PURPOSE>` |

Copy final tidak harus disimpan di PRD bila sudah memiliki dedicated content source.

---

## 10. Search, Filter, Sort, and Discovery

Gunakan bila relevan.

### Search

- `<EXPECTED PRODUCT BEHAVIOR>`

### Filter

- `<EXPECTED PRODUCT BEHAVIOR>`

### Sort

- `<EXPECTED PRODUCT BEHAVIOR>`

### Discovery / Recommendation

- `<EXPECTED PRODUCT BEHAVIOR OR N/A>`

Detail query/index/search architecture tidak berada di PRD.

---

## 11. Analytics and Product Events

Catat event yang dibutuhkan untuk memahami product outcome, bukan seluruh telemetry engineering.

| Event | Trigger | Key Properties | Purpose |
|---|---|---|---|
| `<EVENT_NAME>` | `<WHEN>` | `<PROPERTIES>` | `<WHY>` |

Jangan memasukkan sensitive data ke analytics tanpa kebutuhan dan review yang jelas.

---

## 12. Data and Privacy Expectations

Product-level expectation:

- `<WHAT USER DATA IS REQUIRED>`
- `<WHAT USER CAN VIEW / EDIT / DELETE>`
- `<RETENTION OR CONSENT EXPECTATION>`
- `<DATA EXPORT / ACCOUNT DELETION EXPECTATION>`

Physical data model berada di `DATA_MODEL.md` dan migrations/schema.

---

## 13. Integrations

Product-level dependency pada external systems.

| Integration | Product Purpose | Critical? | Related Feature |
|---|---|---:|---|
| `<SERVICE>` | `<PURPOSE>` | Yes / No | `<FEATURE>` |

Protocol, retry, timeout, dan technical integration behavior berada di architecture/contract/standards.

---

## 14. Success Metrics

Metric authoritative sebaiknya konsisten dengan Product Brief.

### Primary Metric

| Metric | Definition | Target / Direction |
|---|---|---|
| `<METRIC>` | `<CALCULATION>` | `<TARGET>` |

### Supporting Metrics

| Metric | Purpose |
|---|---|
| `<METRIC>` | `<WHY>` |

### Guardrails

| Metric | Guardrail |
|---|---|
| `<METRIC>` | `<LIMIT>` |

---

## 15. Release Scope

### Required for Release

- `CAP-...`
- `CAP-...`

### Can Be Deferred

- `CAP-...`

### Release Blockers

Release tidak boleh dianggap product-complete jika:

- `<BLOCKER CONDITION>`
- `<BLOCKER CONDITION>`

Technical release gates berada di `RELEASE_CHECKLIST.md` dan CI/CD standard.

---

## 16. Dependencies and Assumptions

### Dependencies

| Dependency | Needed For | Risk |
|---|---|---|
| `<DEPENDENCY>` | `<CAPABILITY>` | Low / Medium / High |

### Assumptions

| ID | Assumption | Status |
|---|---|---|
| A-01 | `<ASSUMPTION>` | Open / Validated / Rejected |

---

## 17. Open Product Decisions

| ID | Decision / Question | Owner | Blocking? | Target |
|---|---|---|---:|---|
| PD-01 | `<QUESTION>` | `<OWNER>` | Yes / No | `<MILESTONE>` |

Jika keputusan menghasilkan architecture change, buat ADR. Jika menghasilkan behavior change, update feature spec.

---

## 18. Feature Specification Index

| Feature | Spec | Status | Related Capability |
|---|---|---|---|
| `<FEATURE>` | `../01_features/<feature>.md` | Draft / Locked | `CAP-...` |

PRD tidak boleh menduplikasi seluruh functional requirements dari feature specs.

---

## 19. Product Acceptance

Product scope untuk fase ini dianggap terpenuhi ketika:

- [ ] seluruh P0 capabilities tersedia;
- [ ] primary user journeys dapat diselesaikan;
- [ ] relevant feature acceptance criteria terpenuhi;
- [ ] product metrics/event instrumentation yang diwajibkan tersedia;
- [ ] tidak ada product blocker yang unresolved;
- [ ] out-of-scope behavior tidak masuk tanpa keputusan eksplisit.

Engineering Definition of Done berada di `AGENTS.md` dan engineering standards.

---

## 20. Related Documents

- Product Brief: `./PRODUCT_BRIEF.md`
- Roadmap: `./ROADMAP.md`
- Feature Specs: `../01_features/`
- System Architecture: `../02_architecture/SYSTEM_ARCHITECTURE.md`
- NFR: `../02_architecture/NON_FUNCTIONAL_REQUIREMENTS.md`
- Data Model: `../02_architecture/DATA_MODEL.md`

---

## 21. Change Log

| Version | Date | Change | Author |
|---|---|---|---|
| 0.1 | `<YYYY-MM-DD>` | Initial draft | `<AUTHOR>` |
