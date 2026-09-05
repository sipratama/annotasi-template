# Project Initialization — Annotasi Template

> **Peran dokumen:** Guided bootstrap workflow untuk mengubah repository template menjadi project nyata tanpa harus mengedit seluruh file secara manual.
>
> Dokumen ini dibaca saat initialization. Setelah project stabil, AI tidak perlu membacanya untuk task normal kecuali diminta.

---

## 1. Prinsip Initialization

Initialization harus:

- menggunakan context yang diberikan user dan evidence yang sudah ada di repository;
- **tidak mengarang** product facts, requirement, architecture decision, atau metric;
- memilih document profile yang proporsional terhadap project;
- mengisi dokumen yang benar-benar aktif;
- menghapus section yang tidak relevan daripada mengisinya dengan filler;
- mempertahankan engineering standards sebagai reusable guidance;
- membuat contract/source/infrastructure folder hanya jika project membutuhkannya.

Unknown decision ditulis sebagai `TBD` atau Open Question, bukan ditebak.

---

## 2. Kapan Workflow Ini Aktif?

Gunakan workflow ini ketika:

- repository baru dibuat dari Annotasi Template;
- dokumen masih berisi `<PROJECT_NAME>` atau placeholder bootstrap;
- user meminta "initialize", "start project", "adapt template", atau setara.

Jangan jalankan ulang seluruh initialization hanya untuk feature development biasa.

---

## 3. Input Minimum

Idealnya AI mengetahui:

| Input | Contoh |
|---|---|
| Project name | `DirakitPro` |
| Problem / product idea | outcome-first learning platform |
| Primary user | beginner learner |
| Base profile | `fullstack` |
| Stack jika sudah dipilih | Next.js + Spring Boot |
| Deployment target jika diketahui | VPS / cloud |
| Modifiers | `saas`, `event-driven`, dll. |

Jika sebagian belum diketahui, gunakan evidence yang tersedia dan tandai sisanya `TBD`.

---

## 4. Pilih Base Profile

Pilih **satu** base profile.

### `fullstack`

Untuk product dengan frontend + backend.

Aktifkan secara default:
- Product Brief;
- PRD;
- Feature Specs;
- System Architecture;
- Data Model jika ada persistence;
- NFR;
- UX Flows;
- Design System;
- Test Strategy;
- Threat Model untuk internet/user-data system;
- Developer Setup;
- Configuration.

Deployment/Runbook/Release docs aktif ketika menuju production.

### `backend-service`

Aktifkan:
- Product Brief;
- PRD bila service mempunyai product/business behavior;
- Feature Specs;
- System Architecture;
- Data Model bila persistent;
- NFR;
- Test Strategy;
- Threat Model bila network/sensitive;
- Developer Setup;
- Configuration;
- operations/delivery sesuai deployment maturity.

UX/Design docs biasanya tidak aktif.

### `frontend-app`

Aktifkan:
- Product Brief;
- PRD;
- Feature Specs;
- System Architecture;
- UX Flows;
- Design System;
- NFR untuk performance/accessibility;
- Test Strategy;
- Threat Model bila auth/session/sensitive data relevan;
- Developer Setup;
- Configuration.

Data Model/persistence docs hanya aktif bila client mempunyai meaningful local persistence.

### `prototype`

Minimum:

```text
PRODUCT_BRIEF.md
PRD.md
FEATURE_TEMPLATE.md + feature specs
SYSTEM_ARCHITECTURE.md
AGENTS.md
```

Tambahkan NFR/security/test/ops docs hanya jika risk membutuhkan.

Prototype tetap tidak boleh:
- commit secrets;
- invent requirement;
- silently break contract;
- melakukan destructive data change tanpa deliberation.

---

## 5. Optional Modifiers

Modifier dapat dikombinasikan dengan base profile.

### `saas`

Pastikan perhatian pada:
- tenancy;
- identity/authorization;
- billing jika ada;
- data isolation;
- configuration;
- deployment/operations;
- security and retention.

### `event-driven`

Aktifkan:
- AsyncAPI/schema bila external/cross-module events menjadi contract;
- event ownership;
- idempotency;
- retry;
- ordering;
- DLQ;
- observability.

### `ai-enabled`

Tambahkan project-specific decisions untuk:
- model/provider;
- prompt/versioning bila material;
- evaluation;
- cost;
- privacy;
- unsafe/untrusted model output;
- fallback/degradation.

Buat ADR bila model/provider architecture menjadi strategic decision.

### `open-source`

Pertimbangkan:
- `CONTRIBUTING.md`;
- license;
- changelog/release notes;
- compatibility policy;
- public setup docs.

### `regulated`

Perkuat:
- traceability;
- security;
- audit;
- retention;
- compliance;
- release evidence;
- approval.

Jangan mengklaim compliance hanya karena template berisi control.

---

## 6. Activation Matrix

Legenda:

- **R** — Required/default for profile
- **C** — Conditional
- **—** — Usually inactive

| Document | Fullstack | Backend | Frontend | Prototype |
|---|:---:|:---:|:---:|:---:|
| Product Brief | R | R | R | R |
| PRD | R | C/R | R | R |
| Roadmap | C | C | C | — |
| Feature Specs | R | R | R | R |
| System Architecture | R | R | R | R |
| Data Model | R/C | R/C | C | — |
| NFR | R/C | R/C | R/C | C |
| UX Flows | R | — | R | C |
| Design System | R | — | R | C |
| Test Strategy | R | R | R | C |
| Threat Model | R/C | R/C | C | C |
| Developer Setup | R | R | R | C |
| Configuration | R/C | R/C | R/C | C |
| Deployment | C | C | C | — |
| Runbook | C | C | C | — |
| Risks | C | C | C | — |
| Release Checklist | C | C | C | — |
| Known Limitations | C | C | C | C |

Engineering standards tetap berada di repo dan dibaca selektif.

---

## 7. Initialization Steps

### Step 1 — Inspect Before Editing

AI harus membaca:

```text
AGENTS.md
README.md
docs/PROJECT_INITIALIZATION.md
```

Lalu inspect:
- existing code;
- package/build files;
- existing documentation;
- current repository structure;
- user-provided context.

Jangan memilih stack hanya berdasarkan template.

### Step 2 — Declare Profile

Catat:

```text
Base profile:
Modifiers:
Known stack:
Deployment maturity:
Active project docs:
Inactive/conditional docs:
Open decisions:
```

Tidak perlu membuat file profile tambahan kecuali project memang membutuhkannya.

### Step 3 — Initialize Product Context

Isi:

```text
docs/00_product/PRODUCT_BRIEF.md
```

Prioritas:
- problem;
- target user;
- value;
- goals;
- non-goals;
- product principles;
- MVP boundary;
- assumptions/open questions.

Jangan mengarang evidence atau metric.

### Step 4 — Initialize PRD

Isi PRD hanya sampai level capability/journey/product rules yang benar-benar diketahui.

Jangan menyalin semua Product Brief ke PRD.

Product Brief tetap owner untuk:
- product purpose;
- target user context;
- strategic outcome;
- product-level assumptions.

PRD owner untuk:
- product capability;
- cross-feature behavior/scope;
- user journeys;
- release product acceptance.

### Step 5 — Create Feature Specs

Jangan isi `FEATURE_TEMPLATE.md` sebagai satu giant FRD.

Copy per feature:

```text
docs/01_features/authentication.md
docs/01_features/checkout.md
```

Gunakan stable IDs:

```text
FR-AUTH-001
FR-CHECKOUT-001
```

### Step 6 — Initialize Architecture

Isi `SYSTEM_ARCHITECTURE.md` berdasarkan architecture yang diketahui.

Minimum:
- system purpose;
- runtime components;
- boundaries;
- dependency direction;
- auth boundary;
- data/integration ownership;
- architecture invariants.

Jika keputusan material belum dipilih, jangan pura-pura locked.

### Step 7 — Activate Conditional Docs

Untuk setiap conditional document:

- **aktif dan isi** jika concern sudah relevan;
- **biarkan template** jika project diperkirakan segera membutuhkan dan statusnya jelas;
- **hapus dari derived project** jika benar-benar tidak relevan dan hanya menambah noise.

Jangan mengisi file dengan puluhan `N/A`.

### Step 8 — Create Contracts Only When Needed

Jika REST API benar-benar menjadi cross-component/public contract:

```text
contracts/openapi/openapi.yaml
```

Jika async events benar-benar menjadi contract:

```text
contracts/asyncapi/asyncapi.yaml
```

Jika belum ada contract, jangan membuat dummy schema hanya agar folder terlihat lengkap.

### Step 9 — Project README

Ganti README template dengan README project yang menjelaskan minimal:

- apa project-nya;
- stack;
- setup/run;
- architecture/docs entry points;
- test command;
- deployment status bila ada.

Derived project tidak wajib mempertahankan README bilingual kecuali audience membutuhkannya.

### Step 10 — Validate

Jalankan:

```bash
python scripts/validate_template.py --project-mode
```

Lalu lakukan project-specific build/test checks.

### Step 11 — Initialization Report

AI harus melaporkan:

```text
Profile
Files activated
Files removed
Files created
Known stack
Open product decisions
Open architecture decisions
Contracts created
Validation/tests executed
Risks / limitations
```

---

## 8. Placeholder Rules

Placeholder diperbolehkan pada reusable template files:

```text
docs/01_features/FEATURE_TEMPLATE.md
docs/02_architecture/adr/ADR_TEMPLATE.md
```

Pada active project docs, metadata placeholder seperti berikut harus diganti atau dinyatakan eksplisit:

```text
<PROJECT_NAME>
<OWNER>
<YYYY-MM-DD>
<AUTHOR>
```

Unknown content tidak boleh diisi dengan fakta palsu.

Gunakan:

```text
TBD
Unknown
Open Question
Not decided
```

sesuai konteks.

---

## 9. Standards Rules During Initialization

Jangan rewrite seluruh `docs/standards/` untuk setiap project.

Standards adalah reusable baseline.

Project-specific deviation harus hidup di:
- architecture;
- ADR;
- NFR;
- security/design documentation;

bukan dengan menyalin standard ke versi kedua.

---

## 10. Initialization Prompt — Recommended

```text
Initialize this repository using AGENTS.md and
docs/PROJECT_INITIALIZATION.md.

Project context:
<PASTE PROJECT CONTEXT>

Base profile:
<fullstack | backend-service | frontend-app | prototype>

Modifiers:
<saas | event-driven | ai-enabled | open-source | regulated | none>

Rules:
- inspect existing repository evidence first;
- do not invent missing product facts or architecture decisions;
- use TBD/Open Question for unresolved material decisions;
- activate only relevant project-specific documents;
- keep engineering standards as reusable references;
- create contracts only if the project needs those boundaries;
- keep feature specs modular;
- run project-mode validation when finished;
- report profile, changed files, unresolved decisions, and evidence.
```

---

## 11. Initialization Definition of Done

Initialization selesai ketika:

- [ ] base profile ditentukan;
- [ ] Product Brief menggambarkan project nyata;
- [ ] PRD mempunyai known capability/scope;
- [ ] feature specs awal dibuat bila scope diketahui;
- [ ] System Architecture menggambarkan baseline nyata, bukan template fiction;
- [ ] conditional docs diputuskan secara eksplisit;
- [ ] contract folders hanya dibuat bila dibutuhkan;
- [ ] active docs tidak memakai project metadata placeholders;
- [ ] README project sudah relevan;
- [ ] validation dijalankan bila tooling tersedia;
- [ ] open decisions dan limitations dilaporkan.

Initialization **tidak** berarti semua requirement dan architecture harus sudah final.
