# Scaffold: project_brief.md

## Purpose
Describe the overall project goals and organization.

## Required structure

```md
# Project Brief

## Problem
What problem is the project trying to solve, and why does it matter?

## Objectives
What outcomes should exist when the project succeeds?

## Organization
Use this section if the project can be decomposed into phases or major subdivisions.
If not, this section may be omitted.
Typical phases may be features, user stories, or subsystems.
List phases here in order, for example:
- Phase 1
- Phase 2
- Phase N

## Phase <N>: <Phase name>
<...> are placeholders for this header
Describe the phase at a high level.
If the project is a single phase, this header can be omitted.

### Objectives
What are the phase objectives?

### Key Elements
What are the main user flows, capabilities, or solution outputs?

### Out of Scope, No Gos, and Open Questions
What is intentionally excluded for now?
Which edge cases will not be handled yet?
Which open questions remain unresolved?

```

## Example
The following is an example of how a `project_brief.md` file may look.

```md
# Project Brief

## Problem
Users cannot easily unify and query their personal health records across providers.

## Objectives
Create a system that ingests health documents, normalizes data, and presents a longitudinal patient view.

## Organization
- Phase 1: Document ingestion
- Phase 2: Data normalization
- Phase 3: Search and retrieval

## Phase 1: Document ingestion

### Objectives
Allow users to upload medical files from multiple providers.

### Key Elements
- PDF upload flow
- DICOM upload flow
- File validation pipeline

### Out of Scope, No Gos, and Open Questions
- No handwritten document support yet
- No real-time syncing in this phase
- Open question: should uploads be processed synchronously or asynchronously?

```

# Scaffold: scope_context.md

## Purpose
A project is composed by one or more scopes.
This section explains in more detail the scope under development on the project right now.

## Required structure

```md
# Scope Context

## Scope Name
- What is the scope under development on the project right now?
- Short, unique identifier for the current scope (e.g., "WhatsApp Intake")

## Scope objective
- Actual piece or "slice" of work being built.
- One sentence describing the expected outcome (clear and verifiable).

## Scope Description
- Why this scope exists (problem or gap it addresses)
- How it connects to previously delivered scopes
- How it enables or unblocks future scopes

## Key elements
- Core components, flows, or artifacts that must exist
- Critical constraints or decisions shaping the solution

## Out of scope and No-Gos
- Explicitly excluded features, edge cases, or approaches
- Known trade-offs or postponed decisions
```

## Example
The following is an example of how a `scope_context.md` file may look.

```md
# Scope Context

## Scope Name
- WhatsApp PDF Intake v1

## Scope Objective
- Enable users to upload PDF medical reports via WhatsApp and persist them as Source records in the system

## Scope Description
- Users currently cannot easily ingest medical documents into the platform
- This scope introduces a simple ingestion channel using WhatsApp, building on the existing Source model
- It will serve as the foundation for future scopes involving OCR extraction and structured data parsing

## Key Elements
- WhatsApp webhook endpoint to receive user messages
- Media retrieval logic (download PDF from provider)
- Source record creation with attached file (ActiveStorage / S3)
- Basic validation (file type, size)
- Logging and error handling for failed downloads

## Out of Scope and No-Gos
- No OCR or data extraction from the PDF
- No classification of document type (e.g., blood test vs imaging)
- No retry queue or background job system (synchronous processing only)
- No user-facing UI for uploads (WhatsApp only)
```


# Scaffold: system_patterns.md

## Purpose
This document captures the recurring architectural patterns and design decisions used across the project.
Each pattern explains:
- the context in which it applies
- the decision made
- the rationale behind it

These patterns should guide consistent implementation across scopes.

## Required Structure

```md
# System Patterns

##  <Pattern name>
- <...> are placeholders for this header
- Short, descriptive name for the pattern (e.g., "Source as Polymorphic Ingestion Layer")

### Key Context
- What problem or constraint led to this pattern?
- When should this pattern be applied?
- Make a briefly description.

### Decision
- What architectural choice was made?
- Why this approach was chosen over alternatives?
- Make a briefly description.

### Implementation Shape
- How this pattern is implemented in the codebase
- Key models, modules, or flows involved
- Bring most relevant cases to explain the pattern. It should not be an exaustive approach.

### Trade-offs
- Downsides or limitations of this pattern
- When it might not be appropriate

### Pattern Key Words
What are the key words related to this pattern.
Write up to 3 key words. From the most to the last relevant.

```

## Example
The following is an example of how a `system_pattern.md` file may look.

```md
# System Patterns

## Source as Polymorphic Ingestion Layer

### Context
- The system needs to ingest multiple types of health data (blood exams, imaging reports, prescriptions, etc.)
- Each data type has different structures but shares a common ingestion and storage flow
- The system must remain flexible to support new data types in the future

### Decision
- Use a polymorphic `Source` model as the central ingestion layer
- Each domain entity (e.g., ImagingDiagnostic, BloodExam, Prescription) is associated with one or more Sources
- This allows all ingestion flows (upload, API, WhatsApp) to be standardized

### Implementation Shape
- `Source` model with `source_type` and polymorphic association (`sourceable`)
- `Source` has attachments via ActiveStorage (`files`)
- Domain models (e.g., ImagingDiagnostic) `has_many :sources`
- Ingestion pipelines always create a Source first, then associate downstream data
- Controllers and services operate primarily through Source

### Trade-offs
- Adds indirection when querying domain-specific data
- Requires careful handling of polymorphic associations in queries
- Some validations must be conditional based on source type

### Pattern Key Words
- polymorphism
- ingestion-layer
- abstraction

```

# Scaffold: tech_context.md

## Purpose
This document captures the key technology decisions made in the project.

Each entry explains:
- the context that led to the choice
- the selected technology
- how it is used in the system

This helps maintain consistency and supports future migrations or refactors.

## Required Structure

```md
## <Decision Name>
- <...> are placeholders for this header
- Short, descriptive name of the technology decision (e.g., "ActiveStorage for File Handling")

### Context
- What problem or constraint led to this decision?
- Keep it concise and focused

### Decision
- What technology or stack choice was made?
- Why this approach was chosen over alternatives?
- Key factors (e.g., simplicity, ecosystem, performance, integration)

### Implementation Shape
- Where this technology is used (backend, frontend, infrastructure)
- How it is integrated into the codebase (key models, services, or configs)
- Any important constraints, conventions, or workarounds
- Focus on representative examples, not exhaustive coverage

### Trade-offs
- Limitations or downsides of this choice
- Known risks or future migration considerations

```

## Example
The following is an example of how a `tech_context.md` file may look.

```md
# Tech Context

## ActiveStorage with S3 for File Storage

### Context
- The system needs to store and serve user-uploaded medical files (PDFs, images, DICOM)
- Files can be large and must be reliably accessible and scalable
- Local storage is not suitable for production environments

### Decision
- Use Rails ActiveStorage with AWS S3 as the storage backend
- Chosen due to tight Rails integration, ease of use, and native support for cloud storage
- Avoided custom upload pipelines to reduce complexity and speed up development

### Implementation Shape
- Backend: Rails (ActiveStorage)
- Infrastructure: AWS S3 bucket for file storage
- `Source` model uses `has_many_attached :files`
- Files are uploaded via controllers and stored directly in S3
- URLs are generated through ActiveStorage (signed URLs when needed)
- Environment-specific configuration in `storage.yml`
- Used alongside WebP processing pipeline for images

### Trade-offs
- Limited control compared to a fully custom file handling system
- Performance depends on S3 latency
- Requires additional configuration for secure access (signed URLs, permissions)

### Alternatives Considered
- Local disk storage (rejected due to lack of scalability)
- Direct S3 SDK usage (rejected due to higher complexity)
- Third-party services (e.g., Cloudinary) (rejected to maintain control and reduce costs)

```


# Scaffold: active_context.md

## Purpose
This document tracks the execution state of the current scope through Value Delivery Tasks (VDTs).
VDTs represent small, concrete units of work that directly contribute to delivering value within the scope.
This file should reflect:
- what is done
- what is in progress or pending
- important implementation considerations specific to this scope

## Required Structure
**Value Delivery Task Status Legend**
[ ] VDT to be done
[/] VDT in progress
[x] VDT Completed
[o] VDT Aborted / archived / merged

```md
# Active Context

## VDTs
Use the checklist format below to track progress.
Guidelines:
- Each VDT should be a small unit of value
- Prefer outcome-oriented descriptions (not just actions)
- Order tasks by execution priority

[ ] VDT Name – short description
[/] VDT Name – short description
[x] VDT Name – short description
[o] VDT Name – short description


## Implementation Notes
Key constraints, patterns, and considerations specific to this scope not mentioned at the project level in the `tech_context.md` or `system_pattern.md` files.

Include:
- Relevant system patterns to follow
- Dependencies (internal or external)
- Technical constraints or decisions
- References to other documentation


### Issue <N> : <Issue Name>
<...> are placeholders for this header
- Description: What is the issue?
- Impact: Why does it matter for this scope?
- Guidance: How should it be handled?

```

## Example
The following is an example of how a `active_context.md` file may look.

```md
# Active Context

## VDTs
[x] Create WhatsApp webhook endpoint
[x] Parse incoming message payload
[x] Extract media_sid from incoming message
[x] Implement media download service
[ ] Handle expired media URLs (retry or fallback strategy)
[ ] Add error handling for failed downloads


## Implementation Notes

### Issue 1: Twilio Media URL Expiration
- Description: Media URLs provided by Twilio (content_direct_temporary) expire quickly (~5 minutes)
- Impact: Delayed processing may lead to failed downloads
- Guidance: Avoid storing URLs; fetch media immediately or proxy via backend using authenticated requests


### Issue 2: Source Creation Pattern
- Description: All ingestion flows must create a Source as the entry point
- Impact: Ensures consistency across ingestion pipelines
- Guidance: Follow "Source as Polymorphic Ingestion Layer" pattern

```

# Scaffold: progress.md

## Purpose
This document tracks the evolution of the project at the scope level.

It provides:
- a high-level view of all scopes required to complete the project
- the current status of each scope
- key open decisions impacting the overall system

Notes:
- This file operates at scope granularity (not VDT level)
- It is continuously updated as scopes evolve (split, merged, discarded)
- Scopes may be grouped into phases when applicable

## Required Structure

**Scope Status Legend**
[x] Completed
[o] Aborted / archived / merged
[/] In progress
[ ] Not started

```md

# Progress

## Phase <N>: <Phase Name>
<...> are placeholders for this header
Group the scopes under the corresponding phases.
If there's only one phase this header is the project name.

### Scopes progress
[ ] Scope Name – short description
[/] Scope Name – short description
[x] Scope Name – short description
[o] Scope Name – short description


### Open Decisions & Issues

#### Decision <N>: <Decision Name>
- Description: What is the decision or issue?
- Impact: Why does it matter for the overall project?
- Options: What are the possible approaches?
- Next Step: What is needed to move forward?

```

## Example
The following is an example of how a `progress.md` file may look.

```md
# Progress

## Phase 1: Data Ingestion Foundation

### Scopes progress
[x] Source Model Foundation – Create base ingestion entity for all health data
[x] ActiveStorage Integration – Enable file upload and storage via S3
[/] WhatsApp PDF Intake v1 – Allow users to send PDFs via WhatsApp and store them
[ ] OCR Extraction Pipeline – Extract structured data from uploaded documents
[ ] Data Normalization Layer – Standardize biomarker names and units

## Phase 2: Data Structuring & Intelligence
### Scopes
[ ] Biomarker Mapping Engine – Map extracted values to known biomarkers
[ ] Longitudinal Health Timeline – Track user data evolution over time
[ ] Alerting System – Detect abnormal patterns in user data

## Open Decisions & Issues
#### Decision 1: OCR Strategy
- Description: Whether to use AWS Textract or an LLM-based OCR pipeline
- Impact: Affects accuracy, cost, and system complexity
- Options:
  - AWS Textract (structured, reliable, less flexible)
  - LLM-based OCR (flexible, potentially more accurate, higher cost)
- Next Step: Run benchmark on real user PDFs

#### Decision 2: Sync vs Async Processing
- Description: Whether ingestion should remain synchronous or move to background jobs
- Impact: Affects performance and system scalability
- Options:
  - Keep synchronous (simpler, faster to build)
  - Introduce background jobs (more scalable, more complex)
- Next Step: Evaluate average processing time and failure rate
```
