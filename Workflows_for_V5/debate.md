---
description: "Interstitial: Triad Resolution — Tactical Triad Debate Playbook"
---

# Interstitial: Triad Resolution [PLAYBOOK: TRIAD DEBATE]

This playbook governs the structured pressure-testing of architectural models, ambiguous requests, and high-risk operations. 

---

## 🛠️ Step-by-Step Dialectic Procedure

### Step 1: Evaluate Triggers
Execute a Triad Debate immediately when any of the following conditions are met:
1.  **Mandatory Triggers**:
    *   Adding or updating third-party libraries/dependencies.
    *   Modifying database schemas, physical tables, or core API endpoints.
    *   Any debugging or repair loop (Phases 3–5) reaching iteration count $\ge 3$.
2.  **Ambiguity Triggers**:
    *   Contradictory constraints given by the user.
    *   High-risk file modifications with sparse documentation.
    *   When Bounded Operation (Law 1) cannot resolve logic vectors.

### Step 2: Conduct the Dialectic Loop
Execute the debate using three distinct, sequential roles:
1.  **`[Proposer]`**: Propose the baseline change, design concept, or API contract. Keep it clear and literal.
2.  **`[Challenger]`**: Perform a **Dual-Vector Analysis**. Analyze:
    *   **`[Vulnerabilities]`**: Negative pressure. Highlight edge cases, performance costs, regression risks, and security issues.
    *   **`[Hidden Value]`**: Positive pressure. Identify unstated design benefits, long-term architectural scalability, or reuse patterns that would be lost if rejected.
3.  **`[Judge]`**: Weigh the Challenger's findings. Issue a final, binding ruling:
    *   **Accept**: Risks are negligible compared to value.
    *   **Modify**: Specific adjustments to mitigate vulnerabilities while preserving hidden value.
    *   **Reject**: Concept fails safety or structural constraints. Trigger alternate path.

---

## 📝 Deliverable Schema: `[Triad Ruling]`

When executing the debate, output the roles and verdict exactly as shown in this schema:

```markdown
### ⚖️ Triad Debate

#### 1. [Proposer]
*   **Proposed Path**: [Detailed explanation of proposed code modification or architectural concept]

#### 2. [Challenger]
*   **[Vulnerabilities]**:
    *   *Risk 1*: [Description of potential failure/side effect]
    *   *Risk 2*: [Description of performance or structural cost]
*   **[Hidden Value]**:
    *   *Value 1*: [Description of unstated leverage or optimization]
    *   *Value 2*: [Description of scalability/reusability gains]

#### 3. [Judge]
*   **Verdict**: [ACCEPT / MODIFY / REJECT]
*   **Logical Rationale**: [Mandatory 2-3 sentence causal proof justifying the verdict]
*   **Execution Directives**: [Specific, actionable code instructions for the plan phase]
```

---

## 🚦 Scope Limit & Gated Halting

*   **Dialectic Round Limit**
    *   The debate must converge and conclude in **$\le 3$ rounds**.
    *   *Exception Gate*: If the Triad cannot resolve the ambiguity within 3 rounds, the ruling is automatically **Gated Halting**. Anchor the state immediately, output coordinates, and request direct user guidance.
*   Once resolved, return immediately to the phase that triggered the debate.
