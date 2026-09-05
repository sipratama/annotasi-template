# Annotasi Template

> 🇮🇩 Bahasa Indonesia · [🇬🇧 English](./README.en.md)

Template pengembangan software yang **AI-ready, opinionated, dan production-oriented** untuk product development fullstack, backend, maupun frontend.

Annotasi Template membantu manusia dan AI coding agent seperti **Codex** dan **Claude Code** bekerja dari source of truth yang sama—mulai dari product intent, feature behavior, architecture, contract, engineering standards, sampai release evidence.

> Tujuannya bukan membuat dokumentasi sebanyak mungkin. Tujuannya adalah menjaga **shared understanding dengan duplikasi seminimal mungkin**.

---

## Apa yang diselesaikan template ini?

AI-assisted development bisa mempercepat coding, tetapi mudah menimbulkan masalah ketika:

- requirement hanya hidup di chat;
- architecture berubah tanpa keputusan eksplisit;
- API contract tertinggal dari implementation;
- AI membaca terlalu banyak context yang tidak relevan;
- business rule tersebar di frontend, backend, dan test;
- project punya banyak dokumen tetapi tidak jelas mana yang authoritative.

Annotasi Template menggunakan alur:

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

## Prinsip utama

### One Concern, One Source of Truth

Satu concern harus mempunyai satu authoritative source.

| Pertanyaan | Source of Truth |
|---|---|
| Kenapa product dibuat dan untuk siapa? | `docs/00_product/PRODUCT_BRIEF.md` |
| Capability apa yang harus tersedia? | `docs/00_product/PRD.md` |
| Bagaimana satu feature harus berperilaku? | `docs/01_features/<feature>.md` |
| Bagaimana sistem disusun? | `docs/02_architecture/SYSTEM_ARCHITECTURE.md` |
| Kenapa keputusan architecture dibuat? | `docs/02_architecture/adr/` |
| Seberapa baik sistem harus bekerja? | `docs/02_architecture/NON_FUNCTIONAL_REQUIREMENTS.md` |
| Apa persistent data model-nya? | migrations/schema + `DATA_MODEL.md` |
| Apa REST/event contract-nya? | `contracts/` bila digunakan |
| Bagaimana engineering dilakukan? | `docs/standards/` |
| Bagaimana testing direncanakan? | `docs/04_engineering/TEST_STRATEGY.md` |
| Bagaimana system dirilis/dioperasikan? | `docs/05_operations/` + `docs/06_delivery/` |

### AI membaca secara selektif

Jangan meminta AI membaca seluruh repository untuk setiap task.

Default flow:

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

### Contract sebelum implementation drift

Perubahan terhadap API, event, schema, atau persistent format harus memperbarui contract/migration sebelum atau bersamaan dengan implementation.

### Architecture decision harus eksplisit

Material architecture change tidak boleh hanya muncul di code atau chat. Gunakan ADR.

---

## Quick Start

### 1. Buat repository dari template

Rekomendasi: aktifkan **Template repository** pada repository GitHub ini, lalu gunakan tombol **Use this template** untuk membuat project baru.

Alternatif: clone/copy repository secara manual.

### 2. Gunakan guided initialization

Buka project baru menggunakan Codex atau Claude Code lalu gunakan prompt:

```text
Initialize this repository as a new project using AGENTS.md and
docs/PROJECT_INITIALIZATION.md.

Use existing repository evidence and the context I provide.
Do not invent missing product decisions.

Project: <nama project>
Profile: <fullstack | backend-service | frontend-app | prototype>
Modifiers: <saas | event-driven | ai-enabled | open-source | regulated | none>

After initialization:
- summarize the selected document profile,
- report unresolved product/architecture decisions,
- report files created/removed/updated,
- run the template/project validation checks where possible.
```

AI akan menggunakan workflow di [`docs/PROJECT_INITIALIZATION.md`](./docs/PROJECT_INITIALIZATION.md).

### 3. Mulai feature development

Untuk feature baru:

1. copy `docs/01_features/FEATURE_TEMPLATE.md`;
2. beri nama berdasarkan domain/feature;
3. definisikan stable requirement IDs seperti `FR-PAYMENT-001`;
4. implementasikan dengan context routing dari `AGENTS.md`.

---

## Struktur repository template

Struktur yang **benar-benar disediakan oleh template**:

```text
.
├── README.md
├── README.en.md
├── AGENTS.md
├── CLAUDE.md
│
├── docs/
│   ├── PROJECT_INITIALIZATION.md
│   │
│   ├── 00_product/
│   │   ├── PRODUCT_BRIEF.md
│   │   ├── PRD.md
│   │   └── ROADMAP.md
│   │
│   ├── 01_features/
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
└── scripts/
    └── validate_template.py
```

Folder seperti `src/`, `backend/`, `frontend/`, `contracts/openapi/`, `contracts/asyncapi/`, migrations, atau deployment manifests **dibuat sesuai kebutuhan project**, bukan dipaksakan oleh template.

---

## Dokumen wajib vs kondisional

Tidak semua project harus mengisi semua dokumen.

### Core — hampir selalu aktif

| Dokumen | Status |
|---|---|
| `README.md` | Wajib |
| `AGENTS.md` | Wajib untuk AI-assisted project |
| `PRODUCT_BRIEF.md` | Wajib |
| `PRD.md` | Wajib untuk product dengan behavior non-trivial |
| `SYSTEM_ARCHITECTURE.md` | Wajib untuk software non-trivial |
| `FEATURE_TEMPLATE.md` | Dipertahankan sebagai template |
| `ADR_TEMPLATE.md` | Dipertahankan sebagai template |
| `docs/standards/` | Dipertahankan; dibaca selektif |

### Conditional

| Dokumen | Aktif ketika |
|---|---|
| `ROADMAP.md` | product memiliki lebih dari satu milestone/direction |
| `DATA_MODEL.md` | project memiliki persistent/domain data |
| `NON_FUNCTIONAL_REQUIREMENTS.md` | quality targets perlu eksplisit |
| `UX_FLOWS.md` | ada user journey lintas screen/feature |
| `DESIGN_SYSTEM.md` | ada user-facing UI |
| `TEST_STRATEGY.md` | testing melibatkan lebih dari unit test sederhana |
| `THREAT_MODEL.md` | ada auth, user data, network boundary, payment, upload, admin, dll. |
| `DEVELOPER_SETUP.md` | project perlu onboarding developer |
| `CONFIGURATION.md` | runtime configuration non-trivial |
| `DEPLOYMENT.md` | project dideploy |
| `RUNBOOK.md` | project dioperasikan/di-support |
| `RISKS.md` | ada material risk yang perlu ownership |
| `RELEASE_CHECKLIST.md` | ada controlled production release |
| `KNOWN_LIMITATIONS.md` | ada limitation yang perlu diketahui contributor/user |

**Engineering standards tetap disimpan**, walaupun tidak semuanya aktif untuk setiap task. `AGENTS.md` hanya merutekan AI ke standard yang relevan.

---

## Project Profiles

### Fullstack

Default untuk product dengan frontend + backend.

Umumnya mengaktifkan:
- product docs;
- feature specs;
- architecture/data/NFR;
- design;
- test strategy/threat model;
- operations saat menuju production.

### Backend Service

Design docs dapat dinonaktifkan. Backend, API/integration, persistence, security, testing, dan reliability menjadi prioritas.

### Frontend App

Backend/persistence project docs dapat dikurangi. Design, UX, API contract consumption, accessibility, testing, dan security tetap relevan.

### Prototype

Gunakan minimum:

```text
PRODUCT_BRIEF
PRD
FEATURE SPECS
SYSTEM_ARCHITECTURE
AGENTS
```

Tambahkan dokumen lain hanya ketika risk/complexity membutuhkannya.

### Modifiers

Profile dapat ditambah modifier:

- `saas`
- `event-driven`
- `ai-enabled`
- `open-source`
- `regulated`

Detail aktivasi ada di `docs/PROJECT_INITIALIZATION.md`.

---

## Codex dan Claude

### Codex

`AGENTS.md` adalah canonical repository-wide instruction source.

### Claude Code

`CLAUDE.md` sengaja sangat tipis dan mengimpor:

```text
@AGENTS.md
```

Jadi Claude dan Codex tidak memiliki dua rule set berbeda.

Detailed AI behavior berada di:

```text
docs/standards/14_AI_ASSISTED_DEVELOPMENT.md
```

---

## Kebijakan bahasa

Annotasi Template menggunakan:

### Bahasa Indonesia / hybrid

Untuk human-facing product thinking:

- `README.md`
- `PROJECT_INITIALIZATION.md`
- `PRODUCT_BRIEF.md`
- `PRD.md`
- `ROADMAP.md`
- `FEATURE_TEMPLATE.md`
- `UX_FLOWS.md`
- `DESIGN_SYSTEM.md`

Technical vocabulary seperti `Acceptance Criteria`, `Non-Goals`, `ADR`, `idempotency`, `rollback`, atau `Given/When/Then` boleh tetap English bila lebih natural.

### English

Untuk engineering dan machine-oriented artifacts:

- `AGENTS.md`
- `CLAUDE.md`
- architecture docs;
- ADR;
- engineering/test/security/operations docs;
- `docs/standards/`;
- source code;
- database/schema naming;
- OpenAPI/AsyncAPI/contracts.

Hanya README yang dimirror bilingual (`README.md` + `README.en.md`). Specification lain mempunyai **satu canonical language** agar tidak terjadi drift.

---

## Requirement IDs

Feature behavior menggunakan stable IDs:

```text
FR-<FEATURE>-<NUMBER>
```

Contoh:

```text
FR-AUTH-001
FR-CHECKOUT-004
FR-PAYMENT-012
```

Rules:
- ID tidak berubah hanya karena refactor;
- ID yang retired tidak digunakan ulang;
- test, contract, issue, dan ADR boleh mereferensikan ID;
- jangan membuat ID untuk implementation detail trivial.

---

## Versioning

Versi Annotasi Template direkomendasikan menggunakan:

- Git Tags;
- GitHub Releases.

Nama repository atau folder tidak perlu membawa nomor versi.

---

## Validasi

Jalankan:

```bash
python scripts/validate_template.py
```

Pada project yang sudah diinisialisasi:

```bash
python scripts/validate_template.py --project-mode
```

Validator melakukan structural checks dasar dan local Markdown link validation. Ini bukan pengganti review isi dokumen.

---

## Filosofi template

Annotasi Template bukan framework yang mewajibkan semua project mempunyai puluhan dokumen aktif.

Gunakan tiga aturan:

1. **Keep the source of truth clear.**
2. **Delete or ignore what does not help delivery.**
3. **Load only the context needed for the current task.**

AI mempercepat implementation; AI tidak memiliki product truth.
