# Engineering notebook

[← Back to profile](../README.md) · [Project casebook](project-casebook.md)

This is a working record of the engineering questions I want to understand in depth. It separates design principles used in my projects from proposed experiments and learning objectives. It is not a list of completed research papers or claims of mastery.

## 01 / Model reasoning is not system verification

**Question.** When should an LLM be allowed to propose a decision, and when must a non-model component accept or reject it?

NODUS, APEX and MRE provide three useful versions of this problem. NODUS asks whether records support an investigation claim; APEX asks whether a proposed schedule satisfies explicit constraints; MRE asks whether a script exhibits the expected behavior on two code versions.

A useful design pattern is:

```text
Inputs → candidate generation → structured candidate → explicit check
                                                   ├─ accept
                                                   ├─ reject / retry
                                                   └─ insufficient evidence
```

**Experiment to run.** Create candidates that are plausible but invalid: an unsupported dependency claim, an impossible schedule and a reproduction that fails because of a missing import. Record whether the verifier rejects each candidate for the right reason. Compare candidate acceptance against a known reference rather than relying on an LLM's confidence.

## 02 / Authoritative records and retrieval indexes

**Question.** What should a system trust when a retrieval result and the underlying data disagree?

A relational store can represent canonical entities and their state. A graph can express paths between entities, and a vector index can discover related descriptions. These mechanisms have different responsibilities. For example, semantic similarity between two maintenance notes does not prove that they refer to the same fault.

**Experiment to run.** Start with structured incident records, generate paraphrased descriptions and retrieve similar notes. Measure retrieval relevance separately from record identity, and confirm conclusions against the canonical identifiers. Include an outdated index entry as a failure case.

## 03 / Stateful software and recoverability

**Question.** How can a system preserve intent and history across failures?

APEX needs state across replanning cycles, MINE-TRACE needs incident history across shifts, PRAMAN needs record versions and MindMap needs persistent coordinates. These are different domains, but each needs explicit state transitions and recoverable storage.

**Experiment to run.** Define valid transitions for a small incident state machine; test duplicate inputs, out-of-order events and interrupted persistence. Then verify the state after restart. Document the invariants and distinguish state reconstruction from simply restoring the last displayed screen.

## 04 / Systems and model engineering study plan

| Study area | Practical exercise | Evidence of learning |
| :--- | :--- | :--- |
| Programming execution & debugging | Trace recursive calls and object references in Python and C++; inspect memory and stack frames. | Explain failures from a debugger trace, not just a working patch. |
| Data structures & algorithms | Implement trees, graph search and dynamic programming; compare complexity. | Working implementations and tests against edge cases. |
| Operating systems & concurrency | Implement a small producer-consumer program and inspect synchronization behavior. | Reproducible tests for race conditions and correct shutdown. |
| Data systems | Design a normalized schema, inspect query plans and compare relational joins with graph traversal. | Explain indexing, access patterns and trade-offs with measured examples. |
| Classical ML | Build train/validation/test workflows and analyze baseline errors. | Reproducible evaluation, leakage checks and error analysis. |
| Deep learning & transformers | Implement a small neural network and progressively build a compact language model. | Training curves, held-out metrics, documented architecture and ablations. |
| Agent harnesses | Construct a tool-use evaluation set with deterministic acceptance criteria. | Trace logs, failure categories, and comparison of orchestration strategies. |

## 05 / How I want to work

- Start with an explicit problem and the simplest testable solution.
- Write down assumptions, architecture decisions and acceptance conditions.
- Use AI assistance to accelerate exploration, while understanding the code and verifying results myself.
- Prefer reproducible tests and honest boundaries over unsupported performance claims.
- Maintain concise engineering notes so that previous discoveries can inform future projects.

These notes are intended to evolve as experiments are completed. Future results should include the exact setup, inputs, observed outcomes and limitations, rather than retroactively presenting the proposed work above as completed.

---

[← Back to profile](../README.md)
