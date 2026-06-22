---
description: "Phase 5: Verify & Debug — Tactical Verification & Gated Loop Playbook"
---

# Phase 5: Verify & Debug [PLAYBOOK: GATED LOOP]

This playbook governs the verification of Applied modifications, execution of diagnostic or test suites, and control of the state machine loops.

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

## 🚦 Loop Control Decision logic

Categorize the verification state into one of four conditions to determine the next workflow transition:

### Condition A: Execution Blocked / Contradictory Constraints
*   *Definition*: The execution failed, dependencies are missing, or constraints are contradictory.
*   *Action*: Trigger **Gated Halting**. Stop execution, do not attempt speculative fixes.
*   *Deliverable*: Output a clearly marked State Anchoring block:
    ```markdown
    ### 🛑 Gated Halting State
    *   **[Completed]**: [What is verified on disk]
    *   **[In-Progress]**: [What was being edited when blocked]
    *   **[Next]**: [Planned trajectory after unblocking]
    *   **[Decision Points]**: [The exact question(s) for the user]
    ```

### Condition B: Subtask Successful, Macro Goal Incomplete
*   *Definition*: The atomic subtask is verified, but the `[Definition of Done Checklist]` is not 100% complete.
*   *Action*: Loop back to **Phase 3: Plan & Log** (`/plan`) to outline the next subtask.

### Condition C: Macro Goal 100% Completed
*   *Definition*: Every checklist item on the `[Definition of Done Checklist]` is verified on disk.
*   *Action*: Proceed to **Phase 6: Align & Judge** (`/align`).

### Condition D: Thread Blocked, Parallel Thread Available
*   *Definition*: The current subtask thread is blocked, but the Task Registry contains other independent, unblocked threads.
*   *Action*: Pivot. Mark current thread as `BLOCKED` in the Task Registry. Mark the target independent thread as `ACTIVE`. Transition to Phase 3 for the new thread. Return to the blocked thread once user input is received.

---

## 🛑 Recursion Limit Protection

*   **Subtask Iteration Limit**: A subtask is permitted to loop between Phases 3–5 a **maximum of 5 times**.
*   If the subtask does not converge (Condition B or C) within 5 loops, the state machine triggers **Gated Halting** (Condition A). Halt and escalate to the user to prevent infinite debugging spirals.
