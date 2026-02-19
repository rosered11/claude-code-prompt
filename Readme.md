# Readme

### Insight ที่ Architect ต้องรู้ (จากบทความนี้)

เขาพูดชัดมากว่า:

- ตอนแรกเขาใช้ Claude แบบ Dev:

`generate a REST controller for the Todo class`

ผลคือ:

`ได้ generic code ที่เสียเวลาปรับมากกว่าเขียนเอง`

💥 Breakthrough Moment ของ Architect

เขาบอกว่า:

```
ความต่างระหว่าง
❌ Code Generator
กับ
✅ Architecture Assistant
```

อยู่ที่:

```sql
Initial Project Analysis
```
และ command ที่สำคัญที่สุดคือ:

```bash
/init
```

เพราะมันจะ:

- Analyze entire codebase
- Generate CLAUDE.md
- สร้าง project contextual memory

📌 Key Lesson (สำคัญมาก)

เขาแนะนำว่า:
```
อย่าหยุดแค่ auto-generated CLAUDE.md
ให้ customize ด้วย architecture conventions ของทีม
```

แปลว่า:

Software Architect ต้อง:

- Inject:
    - Layering Rules
    - Aggregate Boundary
    - Naming Convention
    - Domain Rules

เข้าไปใน Claude ก่อน generate code

### Medium Profile ของเขา (รวม AI + Architecture)

มีบทความเกี่ยวกับ [link](https://medium.com/%40giuseppetrisciuoglio):

- AI Help Desk Architecture
- Multi-Agent System
- RAG System Design
- Prompt Strategy for Enterprise

### Bonus (ของจริง)

Claude Code Developer Kit:

👉 ใช้สอน Claude ให้มี skill เช่น:

- general-software-architect
- code-reviewer
- refactor-expert
- aws-solution-architect

ติดตั้งได้ใน Claude CLI:
```bash
/plugin marketplace add giuseppe-trisciuoglio/developer-kit
```

🎯 แนะนำ Learning Order

1️⃣ อ่าน:
- Claude Code: One Month...

2️⃣ สร้าง:
- CLAUDE.md (Architecture Rule)

3️⃣ Install:
- developer-kit plugin

4️⃣ ใช้:
```bash
/devkit.refactor
/devkit.feature-development
/devkit.github.review-pr
```


## Example

นี่คือ CLAUDE.md (Architecture Rule Template) สำหรับ:

✅ .NET

✅ DDD

✅ Clean Architecture

✅ SAP FTP Sync

✅ ETL (Staging → Warehouse)

✅ Outbox Pattern

✅ BU Cronjob

✅ EFCore + PostgreSQL

เอาไปวางไว้ที่:

```
root/
 └── CLAUDE.md
```

📄 CLAUDE.md (Software Architect Version)

```md
# 🧠 Architecture Governance Rules
This project follows Domain-Driven Design (DDD) and Clean Architecture.

You must strictly follow:

- Layered Architecture
- Aggregate Root consistency
- Separation of Concerns
- Transaction Boundary enforcement
- Domain Event Driven design

---

# 🏗️ Architecture Layers

Domain Layer:
- Entities
- Value Objects
- Aggregates
- Domain Events
- Domain Services
- Business Rules

Application Layer:
- Application Services
- Command / Query Handlers
- DTOs
- Validators
- MediatR Pipeline

Infrastructure Layer:
- EFCore Repositories
- FTP Clients
- PostgreSQL
- Bulk Insert
- Outbox Table
- File Storage
- External APIs

---

# 🚫 Forbidden Dependencies

Domain Layer MUST NOT depend on:

- EFCore
- Infrastructure
- FTP
- PostgreSQL
- DTOs
- MediatR

Application Layer MUST NOT contain:

- Business Logic
- Domain Validation
- Aggregate Rules

Infrastructure MUST NOT contain:

- Domain Logic
- Mapping Logic

---

# 📦 SAP Product Sync Domain Rules

Source:

SAP FTP File

Pipeline:

FTP → Staging DB → Validation
→ Transformation → Domain Event
→ Activity Generator
→ Warehouse DB

Constraints:

- Large files
- Overlapping records
- No reliable timestamp
- Row-level change detection required
- Support Add / Update / Delete
- Multi Business Unit (BU)
- Retryable processing
- Idempotency required

---

# 🧬 Aggregate Rules

Product Aggregate:

- Represents a product per BU
- Defines transactional boundary
- Contains:
  - ProductId
  - BusinessUnitId
  - Version
  - Status
  - ActivityTrigger

All business rules MUST reside inside Aggregate.

Avoid:

❌ Anemic Domain Model

---

# 🔄 Change Detection Strategy

Compare:

- Staging Table
- Warehouse Table

Use:

- Hash-based comparison
- Version tracking

Determine:

- Add
- Update
- Delete

Soft Delete MUST trigger:

ProductDeactivatedEvent

---

# 📣 Domain Events

Examples:

- ProductCreatedEvent
- ProductUpdatedEvent
- ProductDeletedEvent
- ProductDeactivatedEvent

Domain Events MUST NOT:

- Call Infrastructure directly

---

# 📤 Outbox Pattern

Integration Events:

- Must be stored in Outbox Table
- Must be transactionally safe
- Must be published asynchronously

---

# 🏭 Activity Generator

Trigger:

On Product Domain Event

Requirements:

- BU-aware
- Retryable
- Idempotent
- Async

---

# ⏱️ Background Worker

Must support:

- BU-based cronjob
- Checkpoint resume
- Retry Policy
- Serilog Logging
- Bulk Insert/Update

---

# 🧪 Testing Rules

- Domain Layer must be unit testable
- Use xUnit
- Use EFCore InMemory for Application tests

---

# 🎯 Design Principles

Prefer:

- Rich Domain Model
- Explicit Boundaries
- Transactional Consistency

Avoid:

- Fat Application Services
- Infrastructure Leakage
- Domain Logic in DTO
```

🚀 หลังจากสร้างเสร็จให้รัน:

```bash
/init
```

Claude จะ:
- อ่าน CLAUDE.md
- เข้าใจ Architecture Rule
- Generate contextual memory

ตอนนี้ Claude จะ:

❌ ไม่ generate EFCore ใน Domain

❌ ไม่ทำ Anemic Model

❌ ไม่ใส่ business logic ใน Application

✅ Respect Aggregate

✅ Use Domain Event

✅ Follow Outbox Pattern

✅ Separate Infra


🏁 ต่อไปสั่งได้เลย:

```bash
/refactor ProductSyncHandler 
according to CLAUDE.md

```

หรือ:

```bash
/design ProductActivityGenerator 
following architecture rules
```

# Reference

- [Claude code on month](https://medium.com/%40giuseppetrisciuoglio/claude-code-one-month-of-practical-experience-a-guide-for-software-architects-and-developers-e52b74236d1a)

- [Giuseppe Trisciuoglio](https://medium.com/%40giuseppetrisciuoglio)