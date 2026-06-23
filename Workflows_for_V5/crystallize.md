---
title: "Phase 7: Crystallize Playbook"
abstract: "Playbook governing post-task knowledge extraction and empirical local heuristics generation."
date: 2026-06-22
keywords: ["crystallize", "heuristics", "wisdom", "extraction", "playbook"]
status: "active"
---

# Phase 7: Crystallize [PLAYBOOK: WISDOM EXTRACTION]

This playbook governs post-task knowledge extraction, transforming context-specific actions into general, reusable guidelines.

---

## 🚦 The Truth Gate Safety Invariant

> [!CRITICAL]
> **NEVER** extract heuristics during active troubleshooting, speculative design, or incomplete task loops. You must only perform crystallization when the absolute root cause is confirmed, a true answer is found, and a feature/subtask is 100% completed and verified on disk.

---

## 🛠️ Step-by-Step Wisdom Extraction Checklist

### Step 1: Format the State Export
*   Strip transient debugging comments or noise.
*   Retain the macro-structure, primary state transitions, and logic decision paths.
*   Produce a clean, structured summary block of the session.

### Step 2: Update Variance Referencing (`references.md`)
*   Document errors, missteps, or suboptimal paths (the "Delta").
*   Frame failures as historical navigation references (e.g. "Lessons from failed attempts/variances"), not as rigid laws.

### Step 3: Extract Protocol Abstraction (`local-rules.md`)
*   Extract successful vectors and generalize them to be domain-independent.
*   **The Heuristic Framing Rule**: Write all entries in `local-rules.md` as **Empirical Heuristics and Local Guidelines** rather than rigid "Rules and Laws".
    *   Avoid dogmatic imperatives ("never", "always", "must", "law").
    *   Use advisory recommendations and empirical observations (e.g., "we found that...", "it is recommended to...", "guidelines suggest...").

### Step 4: Integrity Cross-Check
Before writing any files to the `.ai/` directory, perform this verification:
1.  **Segregate Failure**: Ensure failed trajectories are logged strictly in `references.md`, never in `local-rules.md`.
2.  **Verify Candidates**: Confirm every proposed heuristic in `local-rules.md` matches the actual concluded solution.
3.  **Active Purge**: If a previously saved guideline is contradicted by new findings, update or deprecate it immediately.

---

## 📝 Deliverable Schema: `[Strategic Entry]`

Output the crystallization entry using the schema below:

```markdown
### 💎 Strategic Entry

#### 1. Goal-Means Gap (Context & Problem)
*   **Context**: [Summary of initial task constraints]
*   **Problem**: [What went wrong or caused friction]
*   **Solution**: [The final verified fix]

#### 2. Local Guidelines (Heuristics & Guidance)
*   **Guideline X.Y - [Title]**: We found that [empirical observation]. When [condition], it is recommended to [action description] to avoid [pitfall].
*   **Guideline A.B - [Title]**: Past experience suggests [empirical observation]. It is recommended to [action description] in order to [desired outcome].
```
