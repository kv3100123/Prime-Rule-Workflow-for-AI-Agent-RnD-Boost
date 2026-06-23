---
title: "Phase 5: Verify & Debug Playbook"
abstract: "Playbook governing verification, diagnostics execution, and control of the state machine loops."
date: 2026-06-22
keywords: ["verify", "debug", "loop", "gated", "diagnostics"]
status: "active"
---

# Phase 5: Verify & Debug [PLAYBOOK: GATED LOOP]

This playbook governs the verification of applied modifications, execution of diagnostic or test suites, and control of the state machine loops.

---

## 🛠️ Step-by-Step Verification Checklist

### Step 1: Read the Freshly Modified Disk State
*   Immediately read the modified files from disk (do not rely on working memory of what was written).
*   Verify the syntax structure and logic accuracy.

### Step 2: Run Verification Checks
*   Execute tests, compile code, run static analysis, or visually inspect changes.
*   Compare outcomes strictly against the evaluation criteria set in Phase 3's `[Design]` plane.

### Step 3: Persistence of State and Findings
*   **Update Session Tracker**: Append current execution outcomes and updated Task Registry state to `.ai/session.md` in the nearest `.ai/` directory (searching recursively upwards from active subproject files).
*   **Log Findings**: If you encounter specific quirks, API behaviors, library requirements, or error solutions, append them to `.ai/findings.md` in the nearest `.ai/` directory.

---

## 🚦 Loop Control Decision Logic

Categorize the verification state into one of six conditions to determine the next workflow transition:

### Condition A: Diagnostic Failure
*   *Definition*: There are linter warnings, compiler errors, or test failures.
*   *Action*: The agent **must** log the exact error messages to `.ai/findings.md` in the nearest `.ai/` directory, and transition directly back to **Phase 3: Plan & Log** (`/plan`) to re-evaluate the technical strategy. Do not attempt blind fixes without updating the plan.

### Condition B: Execution Blocked / Contradictory Constraints
*   *Definition*: The execution is physically blocked by configuration errors, missing APIs/environment variables, or user constraints are contradictory.
*   *Action*: Trigger **Gated Halting**. Stop execution, do not attempt speculative fixes.
*   *Deliverable*: Output a clearly marked State Anchoring block:
    ```markdown
    ### 🛑 Gated Halting State
    *   **[Completed]**: [What is verified on disk]
    *   **[In-Progress]**: [What was being edited when blocked]
    *   **[Next]**: [Planned trajectory after unblocking]
    *   **[Decision Points]**: [The exact question(s) for the user]
    ```

### Condition C: Subtask Successful, Macro Goal Incomplete
*   *Definition*: The atomic subtask is verified, but the `[Definition of Done Checklist]` is not 100% complete.
*   *Action*: Loop back to **Phase 3: Plan & Log** (`/plan`) to outline the next subtask.

### Condition D: Macro Goal 100% Completed
*   *Definition*: Every checklist item on the `[Definition of Done Checklist]` is verified on disk.
*   *Action*: Proceed to **Phase 6: Align & Judge** (`/align`).

### Condition E: Thread Blocked, Parallel Thread Available
*   *Definition*: The current subtask thread is blocked, but the Task Registry contains other independent, unblocked threads.
*   *Action*: Pivot. Mark current thread as `BLOCKED` in the Task Registry. Mark the target independent thread as `ACTIVE`. Transition to Phase 3 for the new thread. Return to the blocked thread once user input is received.

### Condition F: Max Loop Iterations Reached
*   *Definition*: The subtask iteration count reaches 3 without converging.
*   *Action*: Transition immediately to **Phase: Triad Resolution** (`/debate`) to run a dialectic review of the design and assumptions before halting.

---

## 🛑 Recursion Limit Protection

*   **Subtask Iteration Limit**: A subtask is permitted to loop between Phases 3–5 a **maximum of 3 times**.
*   If the subtask does not converge (Condition C or D) within 3 loops, the state machine triggers **Condition F** (Transition to Triad Debate). If the Triad Debate cannot resolve the design issue within 3 rounds, it then triggers **Gated Halting** (Condition B) to prevent infinite debugging spirals.
