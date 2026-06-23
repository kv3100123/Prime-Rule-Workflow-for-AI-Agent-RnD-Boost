---
title: "Phase 1: Explore & Research Playbook"
abstract: "Playbook governing context gathering and research at the start of any engineering task."
date: 2026-06-23
keywords: ["explore", "research", "context", "playbook"]
status: "active"
---

# Phase 1: Explore & Research [PLAYBOOK: CONTEXT ACQUISITION]

This playbook governs context gathering at the start of any task or subtask. Follow these steps to systematically transition from an unknown workspace state to a fully mapped, high-confidence context.

---

## 🚀 Bootstrap Protocol (How to Initiate)
Whenever a new user task/prompt is received, the agent must bootstrap the workflow engine:
1. **Complexity Gate Check**: Silently classify the task complexity (Trivial, Standard, Complex).
2. **Phase 1 Initiation**: For Standard or Complex tasks, the agent **must** initiate Phase 1 (Explore) in its very first response block. The response must immediately begin with the `### 🔍 Context Snapshot` block and run context-acquisition tools. Proposing plans or modifying files in this first response block before context is established is strictly prohibited.

---

## 🛠️ Step-by-Step Research Checklist

### Step 1: Read Explicitly Mentioned Files
*   Identify all files, directories, or code symbols mentioned by the user or within active session documents.
*   Audit them completely using the `view_file` tool to understand their structure and internal logic. Do not guess what lies inside.
*   Check the YAML front-matter header of markdown documents first to assess relevance before reading the entire file.

### Step 2: Traverse Adjacent Files & Configurations
*   List contents of active subproject folders using `list_dir`.
*   Scan for system configuration manifests (e.g., `package.json`, `setup_config.yaml`, `.env.example`, `CMakeLists.txt`).
*   Identify tests or test scripts that verify code within the component you are modifying.

### Step 3: Audit Deployed Rules & Historic Records
*   Read and verify the version of the active deployed global rules (`GEMINI.md` on your system).
*   Audit the nearest `.ai/STRATEGIC_LOG.md` and `.ai/local-heuristics.md` (searching recursively upwards from active subproject directories).
*   Extract reference weights, past troubleshooting findings, and design principles established by previous sessions.

### Step 4: Map Upstream and Downstream Dependencies
*   Use the `grep_search` tool to trace where modified functions, variables, or files are imported, called, or referenced.
*   Identify side effects or breaking changes that your edits could introduce elsewhere in the project.

### Step 5: Visual and Minor Cue Audit
*   Actively review the user prompt for any dropped files, screenshots, or console output snippets.
*   Open and examine visual assets in full (analyzing code lines in images, error messages, and UI mock layouts) to extract all implicit requirements.
*   Audit every single word or brief comment in the prompt to ensure no subtle constraints are missed.

---

## 📝 Deliverable Schema: `[Context Snapshot]`

After completing the research checklist, output your findings using the following schema. This block must be clearly visible in the chat response.

```markdown
### 🔍 Context Snapshot

#### 1. [Known]
*   **Global Rules**: [Must explicitly validate rules read, e.g. "Global Rule: Ingested V5 Architecture"]
*   **Workspace Paths**: [List absolute directories and files analyzed]
*   **Active Configurations**: [Key settings, dependencies, or versions detected]
*   **Historical Context**: [Critical learnings extracted from .ai/ logs or design docs]
*   **System Dependencies**: [Mappable upstream/downstream connection points]

#### 2. [Unknown]
*   [List missing files, unverified assumptions, undocumented behaviors, or ambiguous parameters]

#### 3. [Assumptions]
*   **Assumption A**: [Description] | *Confidence*: [High/Medium/Low] | *Causal Rationale*: [Why this assumption is likely true]
*   **Assumption B**: [Description] | *Confidence*: [High/Medium/Low] | *Causal Rationale*: [Why this assumption is likely true]
```

---

## 🚦 Transition Gates & Error Handlers

*   **Gate A: Sufficiency Check**
    *   *Condition*: All critical context parameters are resolved (no High/Medium confidence gaps in `[Unknown]`).
    *   *Action*: Proceed to **Phase 2: Parse & Decompose** (`/parse`).
*   **Gate B: Critical Gaps / Low Confidence Detected**
    *   *Condition*: Gaps exist in the `[Unknown]` block that make task planning highly speculative or risky, OR the confidence level of the proposed solution/approach is **$\le 90\%$**.
    *   *Action*: Do not guess. Trigger a `/debate` (Triad Resolution) to resolve the missing parameters or halt and request direct user input.
