# Readme

1. System Context Prompt (ต้องรันก่อนเสมอ)

```
/set system context:

You are a Software Architect specializing in:

- Domain-Driven Design (DDD)
- Event-Driven Architecture
- .NET Microservices
- ETL Pipelines
- SAP Integration
- FTP-based ingestion
- PostgreSQL bulk processing

Our system processes SAP product files from FTP.

Pipeline:

FTP → Staging DB → Validation → Transformation 
→ Domain Event → Activity Generator 
→ Warehouse DB (PostgreSQL)

Constraints:

- Files are large (millions of rows)
- Records may overlap between files
- No reliable file-level timestamp
- Change detection must be row-level
- Sync must support Add / Update / Delete
- Multi Business Unit (BU)
- Cronjob per BU
- Idempotency required
- Retry required
- Async processing required
- EFCore.BulkExtensions used

Architecture Requirements:

- Clean Architecture
- DDD layering
- Outbox Pattern
- Checkpointing
- Background Worker
- Domain Events
- Integration Events
- MediatR
```

👉 เพื่อให้ Claude เข้าใจ “โลกของระบบคุณ”

2. Design Product Sync Microservice

```
/design a .NET microservice for SAP Product Sync

Include:

- FTP ingestion service
- staging table strategy
- version tracking per product
- change detection per record
- domain aggregate boundary
- activity generation pipeline
- BU-based processing
- async background worker
- retry policy
- checkpointing mechanism
- idempotency handling
- outbox pattern

Target:

PostgreSQL warehouse

```

3. Detect Change Logic (หัวใจ SAP Sync)

```
/design row-level change detection strategy 
for SAP product sync

Conditions:

- No reliable modified timestamp
- overlapping files
- Add / Update / Delete detection required

Compare:

- staging table
- warehouse table

Suggest:

- hash strategy
- version strategy
- soft delete handling

```

4. Refactor Existing Sync Handler (God Service Killer)

```
/refactor this sync handler 
into DDD pipeline using:

- Application Service
- Domain Service
- Aggregate
- Domain Event
- Integration Event
- Outbox Table
- Validator
- Activity Generator
- Retry Policy
- Checkpoint

Preserve business logic
Separate infrastructure logic

```

5. Activity Generator Design

```
/design ProductActivityGenerator

Requirements:

- trigger on product change
- generate activity per BU
- async processing
- retryable
- transactional safe
- outbox compatible

```

6. Background Worker per BU

```
/create .NET background worker 
to process product sync per BU

Include:

- cronjob support
- checkpoint resume
- retry policy
- logging using Serilog
- bulk insert/update

```

7. Generate Tests (Domain First)

```
/generate xUnit tests 
for domain validation logic

Use:

EFCore InMemory provider

```

8. Architecture Drift Scan (Weekly Run)

```
/find violations against:

- DDD layering
- Clean Architecture
- Aggregate boundary
- Application vs Domain separation
- Infrastructure leakage

```

🏁 How Architect ใช้จริง (Workflow)

```
claude

1️⃣ /set system context
2️⃣ /design microservice
3️⃣ /design change detection
4️⃣ /refactor sync handler
5️⃣ /create BU worker
6️⃣ /generate domain tests
7️⃣ /find architecture violations

```

📌 Pro Tip

หลัง Dev merge PR:

```
/review this pull request 
for architecture violations

```
👉 ใช้เป็น AI Architecture Governance