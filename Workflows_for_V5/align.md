---
description: "Phase 6: Align & Judge — Tactical Global Alignment Playbook"
---

# Phase 6: Align & Judge [PLAYBOOK: GLOBAL ALIGNMENT]

This playbook governs system-wide alignment checks once all subtask threads have been completed and verified.

---

## 🛠️ Step-by-Step Alignment Checklist

### Step 1: Execute the Cross-Domain Integrity Audit
*   Audit all modified files, configuration settings, and documentation modules.
*   Verify that edits in one domain (e.g. source code changes) have not broken rules or constraints in adjacent domains (e.g. test files, environment manifests, user guides).

### Step 2: Run Supervisory Verification
*   Re-read the original user request and the Phase 3 `[Supervisory]` objective.
*   Confirm that the final state on disk satisfies the stated goals.
*   Verify every item in the **[Definition of Done Checklist]** has a corresponding physical check on disk.

### Step 3: Run Architectural Drift Audit
*   Compare the final code architecture against the `[Design]` strategy formulated in Phase 3.
*   Detect any scope creep or structural modifications.
*   *Drift Evaluation*: If drift is found, determine if it is beneficial (needs documentation) or harmful (requires rollback or correction before completing).

---

## 📝 Deliverable Schema: `[Alignment Verdict]`

Once the checklist is complete, output the verdict exactly as formatted below:

```markdown
### ⚖️ Alignment Verdict

*   **Verdict**: [ALIGNED / DRIFTED / FAILED]
*   **Supervisory Check**: [Verification summary of original user request requirements]
*   **Cross-Domain Integrity Status**: [Clear/Inconsistent - details of validation checks]
*   **Architectural Drift Audit**: [No Drift / Beneficial (justification) / Harmful (remediation plan)]
*   **Next Steps Action**: [Macro completion declaration OR corrective actions mapping]
```

---

## 🚦 Alignment Verdict Decision Logic

*   **ALIGNED**
    *   *Condition*: All requirements satisfied, no harmful drift, cross-domain check passed.
    *   *Action*: Unilaterally declare macro completion. Transition to Phase 7 if the user requests crystallization.
*   **DRIFTED**
    *   *Condition*: Non-harmful architectural changes were made or minor corrections are needed.
    *   *Action*: Document the drift. Loop back to Phase 3 (`/plan`) to apply corrections or present drift justifications to the user.
*   **FAILED**
    *   *Condition*: Major requirements missed or harmful regressions/inconsistencies introduced.
    *   *Action*: Trigger **Gated Halting**. Anchor the state and request direct user guidance.
