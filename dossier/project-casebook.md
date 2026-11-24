# Project notes

[← Back to profile](../README.md)

Notes on the projects I have worked on, including the problems they address, how they are put together, and what I would test next. Some are prototypes or team projects; the notes distinguish demonstrated features from proposed work.

## NODUS

**Enterprise change-impact investigation** · [Source repository](https://github.com/Glassman007/NODUS)

**Problem.** A service change can affect consumers and teams that are invisible when looking only at the changed repository. Searching individual documents does not necessarily expose the dependency chain or establish whether a particular source supports a conclusion.

**Approach.** Model services, contracts, records and ownership as relationships. Use graph navigation alongside scoped retrieval, then allow a model to organize the findings into an investigation report.

```text
Investigation objective → authorized records → relationship traversal
                      → model-assisted analysis → report
```

**Architecture.** React/TypeScript provides the investigation UI, FastAPI coordinates requests, Neo4j represents relationships, and PostgreSQL stores application state. Gemini supports interpretation and report synthesis.

**Design decision.** A model should not determine permissions or establish evidence merely by asserting a claim. Authorization belongs in the backend; conclusions require inspectable supporting records.

**Current scope.** The repository describes graph-based investigation and Gemini reporting using the synthetic NEXUS organization. Strict evidence verification, selected-source enforcement and automated ownership/task delivery still require end-to-end validation. A live connector or delivered notification should not be inferred from a synthetic record.

**What to test next.** Test a contract-change scenario in which a relevant source is excluded, and verify that no unauthorized information appears in the report or tool trace.

## A.P.E.X

**Adaptive athlete planning** · [Source repository](https://github.com/Glassman007/A.P.E.X)

**Problem.** A fixed training schedule can become infeasible when fatigue, recovery or available time changes. A one-shot chatbot does not provide persistent planning state or reliable scheduling constraints.

**Approach.** Represent the athlete's current observations as state, interpret changes, decide whether to replan, solve a constrained scheduling problem and verify the proposed schedule before saving it.

```text
Observe → interpret → plan → optimize → verify → persist
            ↑                                 │
            └──────────── next observation ───┘
```

**Architecture.** The documented design uses FastAPI, LangGraph for orchestration, OR-Tools for optimization, SQLAlchemy and PostgreSQL for persistence, with test and simulation components.

**Design decision.** Keep scheduling constraints outside the language model. The model can interpret a goal, but the constraint engine and verifier determine whether a proposal is acceptable.

**Boundary.** This is a software planning project, not a clinically validated or professionally prescribed training system.

**What to test next.** Simulate a sudden reduction in available training windows, compare the original and revised schedules, and test both feasible and infeasible constraint combinations.

## PRAMAN

**Parcel data reconciliation and verification** · [Source repository](https://github.com/Glassman007/PRAMAN)

**Problem.** Records about the same land parcel may disagree across departments in identifiers, owner names, area, boundaries or historical versions.

**Approach.** Normalize incoming datasets, resolve parcel identities, detect and classify conflicts, and retain source evidence. A proposed resolution can then go through human review before it becomes part of a versioned parcel record.

```text
Source datasets → normalization → matching → conflict detection
                → proposed reconciliation → review → version history
```

**Architecture.** The repository organizes work around source/schema mapping, unified spatial views, conflicts and reconciliation, evidence, parcel history and shared datasets.

**Design decision.** Reconciliation is not simply overwriting one record with another. The system should retain the source disagreement and make the basis for the proposed resolution visible.

**Boundary.** The application is a reconciliation prototype, not an authority for legal land ownership or a replacement for official cadastral records.

**What to test next.** Construct a test set with conflicting parcel identifiers and geometry, then measure matching precision and inspect false matches before accepting a reconciliation rule.

## MINE-TRACE

**Operational memory for mining equipment** · [Source repository](https://github.com/Glassman007/MINE-TRACE)

**Problem.** Equipment observations, repairs and technician notes can become disconnected when operators change shifts or connectivity is unreliable. A recorded repair does not establish that a recurring fault has been resolved.

**Approach.** Associate observations and maintenance evidence with a machine and incident history. Use structured queries for exact records and semantic retrieval for differently worded observations that may describe similar symptoms.

```text
Equipment observation → local history → SQL records + semantic index
                      → evidence reconstruction → optional AI analysis
```

**Architecture.** The documented design separates local and global components. SQL holds authoritative records, Qdrant supports semantic recall, and hosted model inference is an optional analysis dependency.

**Design decision.** Distinguish a repair from a verified resolution, and keep the original record available when semantic retrieval or AI is unavailable.

**Boundary.** Demonstration data is not real mine telemetry. This decision-support prototype does not replace trained maintenance staff, inspection, or safety authorization.

**What to test next.** Evaluate retrieval on paraphrased incident notes and test whether history remains available during a simulated provider or connectivity failure.

## Minimal Reproduction Extractor (MRE)

**Automated software bug reproduction · HackCBS team project** · [Team repository](https://github.com/garvitsingh006/MRE_Hackcbs9.0)

**Problem.** An issue report may describe a bug without providing a compact executable example. An LLM can generate a plausible script that fails for unrelated reasons.

**Approach.** Give the model the issue and buggy codebase, allow bounded exploration and script execution, and then validate the candidate script against known buggy and fixed versions.

```text
Issue + buggy checkout → search/read/write/run → candidate repro
                       → buggy version fails + fixed version passes
```

**Architecture.** Python, isolated Docker execution, curated SWE-bench Lite instances, provider abstraction and a deterministic verifier. The repository includes repro scripts, orchestration code and verification tests.

**Design decision.** The acceptance criterion is observable program behavior, not whether a model's explanation seems reasonable. Reject irrelevant failure modes such as a broken import.

**Boundary.** A curated demonstration does not establish benchmark-wide reproduction accuracy. This is collaborative hackathon work.

**What to test next.** Evaluate a larger held-out set, categorize failure causes and report actual reproduction success against the deterministic acceptance criteria.

## ReValue

**Electronic device verification** · [Source repository](https://github.com/Glassman007/ReValue)

**Problem.** E-waste and device reuse workflows need a way to assess a device and organize evidence relevant to its verification.

**Approach.** Separate user-facing interactions, application logic and machine-learning functionality. The project direction is to make the verification process easier to inspect and improve independently of the interface.

**Architecture.** The public repository contains frontend, backend, ML-service and Prisma components. The detailed model evaluation, supported device categories and production verification accuracy are not established by the public repository overview.

**Design decision.** Keep the ML service separate from the user workflow so that its behavior can be evaluated without treating a prediction as an authoritative device assessment.

**What to test next.** Document the verification input/output contract and assemble representative validation examples before claiming any accuracy figure.

## Pipeline Explorer

**Transaction observability and fraud-rule inspection** · [Source repository](https://github.com/Glassman007/Pipeline-Explorer)

**Problem.** Transaction-scoring logic is difficult to understand when rule execution and data flow are opaque.

**Approach.** Bring event processing, scoring logic and a visualization interface into one prototype so a developer can inspect transactions and the rules applied to them.

**Architecture.** The repository includes a JavaScript Kafka consumer, fraud engine, SQL schema, sample transactions, a dashboard and Docker Compose configuration.

**Design decision.** A transaction flag is an analytical signal, not proof that fraud occurred. Rule behavior needs to be inspected against known examples.

**What to test next.** Add labeled test cases for ordinary and suspicious transactions, then compare rule coverage and false positives. No detection accuracy or production throughput is claimed here.

## MindMap

**Local-first visual thinking canvas** · [Source repository](https://github.com/Glassman007/MindMap)

**Problem.** Automatic layout and connector adjustment can interrupt manual exploration when the goal is free-form thinking rather than a structured diagram.

**Approach.** Let the user place shapes, edit text and draw arrows without automatic rearrangement. Store the board locally and provide export and editing controls.

**Architecture.** A browser interface and a local Node.js server; the repository documents local JSON autosave, pan/zoom, undo/redo, object editing and PNG export. The local server is designed to bind to loopback.

**Design decision.** Preserve user intent rather than imposing an algorithmic layout. Persistence should not corrupt the board if a write is interrupted.

**What to test next.** Verify that object coordinates and connector geometry remain stable across edit, save, reload and undo/redo operations.

---

[← Back to profile](../README.md) · [Study notes →](engineering-notebook.md)
