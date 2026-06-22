---
description: "Phase 4: Write & Execute — Tactical State Modification Playbook"
---

# Phase 4: Write & Execute [PLAYBOOK: ADM-V]

This playbook governs state modification checks. It implements the Active Delta-Matrix Verification (ADM-V) process to prevent data destruction or regression.

---

## 🛠️ Step-by-Step State Modification Checklist

### Step 1: Execute the Pre-Audit
*   Before running any file modifications, perform a fresh audit of the target file using `view_file`.
*   Confirm there are no local/remote changes or formatting corruption. Reject any outdated or conflicting source data.

### Step 2: Formulate the State-Delta Matrix
Categorize and map the target changes before executing them. Output the matrix explicitly.

*   **Operation Types (Vocabulary Segregation)**:
    *   **Text content changes**:
        *   `[TXT_ADD]`: Adding new variables, functions, sections, or documentation logic.
        *   `[TXT_MOD]`: Editing/modifying existing text or code logic.
        *   `[TXT_DEL]`: Deleting specific lines or paragraphs of text/code.
        *   `[TXT_MERGE]`: Combing blocks of text or logic.
    *   **Physical file changes**:
        *   `[FILE_ADD]`: Creating a new file on disk.
        *   `[FILE_MOD]`: Modifying a file's location or configuration parameters.
        *   `[FILE_TRASH]`: Deprecating a file and moving it to the `.trash/` folder.
        *   🚫 **`[FILE_DEL]` IS STRICTLY FORBIDDEN**. File deletion is not supported in this vocabulary. Deprecated files must be safely trashed.

### Step 3: Run Delta-Only Modifications
*   Use targeted edits (like `replace_file_content` or `multi_replace_file_content`) to apply changes to the exact line ranges.
*   Avoid full-file overwrites unless writing a brand-new file (`[FILE_ADD]`).

---

## 📝 Deliverable Schema: `[Delta Matrix]`

Output the State-Delta Matrix table using the format below:

```markdown
### 📝 State-Delta Matrix

| Target Element | Operation | Delta | Causal Proof |
| :--- | :--- | :--- | :--- |
| `path/to/target_file` | `[TXT_MOD]` | Update config parser logic | Tracing reveals key parser fails when key is null. |
| `path/to/target_file` | `[TXT_ADD]` | Add null validation checks | Prevents null payload exceptions at runtime. |
```
*(Omit unchanged nodes to conserve tokens.)*

---

## 🚦 Safety Constraints & Post-Audit

*   **The Non-Destruction Invariant**
    *   *Proof Check*: If an operation is marked `[TXT_DEL]` or `[FILE_TRASH]`, you must provide a rigorous, logical Causal Proof showing that the deleted data is provably incorrect, fully subsumed, or violates strategic constraints.
*   **Post-Execution Audit**
    *   Immediately after executing the tool call, check the modified file to confirm the edits were correctly applied without side-effects or formatting problems.
    *   Proceed directly to **Phase 5: Verify & Debug** (`/verify`).
