# Study notes

[Back to profile](../README.md) · [Project notes](project-casebook.md)

These are questions and exercises I want to explore, not completed research results. I prefer reading first, implementing a small example and checking the behavior myself.

## Algorithms and computational methods

- Implement a binary search tree with deletion, then compare its behavior on sorted and randomly ordered input. Inspect how height affects lookup cost.
- Implement breadth-first and depth-first graph traversal, including cycles and disconnected components. Compare the traversal order and memory requirements.
- Use Monte Carlo sampling to estimate a quantity with a known analytical solution, repeat with increasing sample sizes and measure variation across seeds.
- Compare a greedy scheduling heuristic with a constraint-based solver on the same small set of feasible and infeasible schedules.

## Software architecture and computing internals

- Trace object references and recursive calls in Python and C++ with a debugger. Explain the difference between stack frames and dynamically allocated objects.
- Build a bounded producer-consumer queue and exercise contention, synchronization and shutdown. Check whether every produced item is accounted for.
- Model a small state machine, persist transitions and test duplicate events, out-of-order inputs and restart after an interrupted write.
- Design a small service with explicit API contracts, then simulate a timeout and a failed downstream dependency. Compare retry and failure behavior.

## Databases and data engineering

Use the same incident dataset in a relational store, a relationship graph and a retrieval index. Compare a join with a graph traversal for a known dependency question. Keep canonical identifiers as the source of truth; semantic similarity alone does not establish record identity. Inspect query plans and add an intentionally stale index entry to test consistency.

## Machine learning and deep learning

I have completed the Machine Learning Specialization and want to strengthen the implementation side. Build a reproducible classical ML baseline with separated training and validation data, inspect errors and test for leakage. Then implement a small neural network, attention and a compact language model. Record the training configuration, loss curves and evaluation limitations instead of claiming results before running the experiments.

## Agent and harness engineering

NODUS, A.P.E.X and MRE raise a shared question: when may an agent propose something, and when should a separate component reject it? Construct a small set of plausible but invalid outputs: a dependency claim with no supporting record, an impossible schedule and a reproduction script that fails for an irrelevant reason. Define expected outcomes before running the agent, log tool calls, and categorize failures. Compare changes using the same evaluation set.

## Reading list

- [Think Python](https://allendowney.github.io/ThinkPython/) — Allen B. Downey
- [Understanding Deep Learning](https://udlbook.github.io/udlbook/) — Simon J. D. Prince
- [Problem Solving with Algorithms and Data Structures](https://runestone.academy/ns/books/published/pythonds3/index.html) — Bradley N. Miller and David L. Ranum

## Open-source interests

Developer tooling, database systems, ML infrastructure and agent frameworks. A practical starting point is to reproduce an issue, read the surrounding implementation and write a regression test before proposing a patch. These are contribution interests, not a claim of existing upstream contributions.

[Back to profile](../README.md)
