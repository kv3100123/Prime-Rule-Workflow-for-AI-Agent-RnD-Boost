---
title: "Phase 2: Parse & Decompose Playbook"
abstract: "Playbook governing task parsing, complexity classification, and MPC trace vector formulation."
date: 2026-06-22
keywords: ["parse", "decompose", "mpc", "trace", "registry", "tasks"]
status: "active"
---

# Phase 2: Parse & Decompose [PLAYBOOK: MPC TRACE]

This playbook governs the parsing of incoming requests and the decomposition of missions into structured, traceable task graphs.

---

## 🛠️ Step-by-Step Decomposition Checklist

### Step 1: Enforce Complexity Classification
Silently classify the mission depth using Law 0:
*   **Trivial Tasks**: A single-step, obvious modification (e.g., formatting alignment, adding a minor comment, fixing a syntax typo).
    *   *Action*: Skip planning and execute directly.
*   **Standard Tasks**: Multi-step edits of moderate complexity with no severe architectural shifts.
    *   *Action*: Proceed to write the 3-Node MPC Trace and the State Tracker.
*   **Complex Tasks**: Multi-domain architectures, high ambiguity, API modifications, or major feature designs.
    *   *Action*: Engages full State Machine loop, including the 5-Node MPC Trace, Task Registry, and active State Tracker.

### Step 2: Formulate the MPC Trace
Define the logical boundary of the task using Model Predictive Control (MPC) formatting. All descriptors must be short (≤ 5 words) keyword phrases.

*   **Standard Trace (3-Node Vector)**:
    ```markdown
    ### 🧩 MPC Trace
    `[Prev: <keyword>] → [Task: <keyword>] → [Next: <keyword>]`
    ```
*   **Complex Trace (5-Node Vector)**:
    ```markdown
    ### 🧩 MPC Trace
    `[t-2: <keyword>] → [t-1: <keyword>] → [Task: <keyword>] → [t+1: <keyword>] → [t+2: <keyword>]`
    *(Note: For brand-new greenfield implementations where historical or future nodes do not logically exist yet, you may gracefully fall back to a 3-Node Vector.)*
    ```

### Step 3: Map Parallel Threads & Dependencies
If the mission contains multiple coupled subtasks, decompose them into separate execution threads:
1.  Output one MPC trace vector per thread.
2.  Draw a dependency map showing the joining points.
    *   *Example*:
        ```
        Thread A: [Prev: Setup] → [Task: Write Engine] → [Next: Integration]
        Thread B: [Prev: Setup] → [Task: Write GUI] → [Next: Integration]
        Dependencies: A.Next ∧ B.Next → Integration (both must verify first)
        ```

### Step 4: Initialize the Task Registry
For **Complex Tasks**, output the initial Task Registry table. Keep this updated at every phase:

```markdown
### 📋 Task Registry

| Task ID | Thread | Supervisory Goal / Deliverable | Status | Dependencies |
| :--- | :--- | :--- | :--- | :--- |
| **T1** | A | [Atomic deliverable description] | `PENDING` | None |
| **T2** | B | [Atomic deliverable description] | `PENDING` | T1 |
```
*(Registry status values: `PENDING`, `ACTIVE`, `VERIFIED`, `DONE`, `BLOCKED`)*

---

## 🚦 Ambiguity Gate & Exception Handler

*   **The Unknown Origin Boundary**
    *   *Condition*: If the preceding state (`Prev` or `t-1`) cannot be verified on disk or logically determined from the Context Snapshot.
    *   *Action*: STOP. Do not speculate or guess.
    *   *Format*: Output: `[Prev: UNKNOWN] → [Task: TRIAD RESOLUTION]`
    *   *Route*: Force transition immediately to **Interstitial: Triad Resolution** (`/debate`) to resolve the context before continuing.
