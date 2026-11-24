# Project notes

[Back to profile](../README.md)

These are notes on the projects I have worked on, including prototypes and collaborative work. The descriptions are based on the linked repositories; suggested tests are not claims of completed results.

## NODUS

[Repository](https://github.com/Glassman007/NODUS)

A change to an authentication API can break a service that is not visible in the original repository. NODUS explores this by modeling dependencies and ownership in Neo4j, retrieving records within a user's scope and using Gemini to summarize findings. FastAPI coordinates the investigation and PostgreSQL persists state.

The important distinction is between a model's conclusion and evidence that actually supports it. The public demo uses synthetic enterprise records; those records do not prove live connectors exist. The README identifies strict source enforcement and verification as areas requiring validation.

**Test to run:** remove a relevant source from the allowed set, investigate a contract change and inspect the tool trace and report for unauthorized records. Record unsupported conclusions rather than accepting a fluent answer.

## A.P.E.X

[Repository](https://github.com/Glassman007/A.P.E.X)

A training schedule can become infeasible after an athlete reports fatigue or loses an available training window. A.P.E.X treats planning as a recurring state transition rather than a one-off answer. LangGraph coordinates the planning loop, OR-Tools handles schedule constraints and a verifier checks candidate plans before persistence.

**Test to run:** simulate reduced availability and compare the revised schedule with the original. Check hard constraints independently of the model, including a case where no feasible schedule exists. This is a planning prototype, not a clinically validated training prescription.

## PRAMAN

[Repository](https://github.com/Glassman007/PRAMAN)

Two departments can describe one parcel with conflicting identifiers, areas or boundary geometries. PRAMAN's documented workflow normalizes records, resolves identities, classifies discrepancies and preserves their provenance through reconciliation and review. It is designed to sit above existing data sources rather than overwrite them.

**Test to run:** create a small labeled set containing matching parcels, overlapping geometry and different coordinate systems. Measure false matches separately from missed matches and inspect the source evidence behind each recommendation. The prototype does not establish legal ownership.

## ReValue

[Repository](https://github.com/Glassman007/ReValue)

ReValue is a device-verification prototype for e-waste and reuse workflows. The public tree separates frontend, backend, ML service and Prisma components. That separation provides a useful place to define an explicit verification interface. The public overview does not establish supported device categories, model quality or production readiness.

**Test to run:** document the input and output contract for device verification, then assemble representative examples including missing or conflicting information. Evaluate the model separately from the user workflow before treating any prediction as a verified assessment.

## MINE-TRACE

[Repository](https://github.com/Glassman007/MINE-TRACE)

A recurring fault can be treated as new if repairs, observations and maintenance notes are scattered across shifts. MINE-TRACE preserves machine-level operational history, combining structured SQL records with Qdrant retrieval. The design separates a local component from fleet-level synchronization and keeps AI findings advisory.

**Test to run:** retrieve paraphrased observations for a known incident and compare against unrelated notes with similar vocabulary. Simulate a connectivity failure and confirm that original local records remain accessible. This prototype is not a substitute for equipment inspection or safety decisions.

## MRE

[Team repository](https://github.com/garvitsingh006/MRE)

Minimal Reproduction Extractor is a collaborative hackathon project. Given an issue and a buggy repository, a model can inspect files, generate a script and execute it in an isolated Docker environment. The verifier compares execution on buggy and fixed revisions of curated SWE-bench Lite instances.

The test is behavioral: a reproduction must demonstrate the reported failure, then succeed after the fix. A missing import or unrelated exception is not a successful reproduction.

**Test to run:** evaluate a held-out set, categorize unrelated failures and report verified reproduction success with its denominator. A curated demonstration alone is not benchmark-wide accuracy.

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

[Back to profile](../README.md) · [Study notes](engineering-notebook.md)
