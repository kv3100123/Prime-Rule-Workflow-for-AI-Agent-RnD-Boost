---
title: "Project Knowledge Consolidation Playbook"
abstract: "A playbook to summarize, consolidate, and register all local knowledge, scripts, skills, and heuristics into a central project summary for future reuse."
date: 2026-06-23
keywords: ["consolidation", "manifest", "local", "reusable-skills", "knowledge"]
status: "active"
---

# Playbook: Consolidate & Localize Knowledge [PLAYBOOK: CONSOLIDATE]

This playbook governs the consolidation of local workspace state, packaging knowledge, custom scripts, local skills, and lessons learned into a single summary document (`CONSOLIDATION.md`). This enables any future AI agent or developer to instantly acquire context and avoid rebuilding wheels when resuming or migrating elements of the project.

---

## 🚦 Trigger Criteria

Execute this playbook manually when:
*   A major phase of a project concludes.
*   Preparing to pause or archive the workspace.
*   Packaging self-contained skills/scripts to be moved or reused in another project.

---

## 🛠️ Step-by-Step Consolidation Checklist

### Step 1: Scan & Inventory
Scan the workspace root and local metadata directories (e.g. `.ai/` and custom skill directories) to register:
1.  **Skills**: Directory-bound rules, manuals, and templates (e.g. `render_mermaid/`).
2.  **Scripts & Utilities**: Executable code files, testing scripts, scratch helper tools.
3.  **Core Heuristics**: Guidelines extracted from `.ai/local-heuristics.md` or `.ai/STRATEGIC_LOG.md`.

### Step 2: Document Context & Findings
Explain the state of the project:
*   What has been solved and verified on disk.
*   The stack and system dependencies.
*   Important architectural decisions and why they were made.

### Step 3: Write the Consolidation Summary (`CONSOLIDATION.md`)
Create a single markdown file `CONSOLIDATION.md` at the project root using the schema below. This file serves as the landing page for future reference.

---

## 📝 Deliverable Schema: `[Consolidation Summary]`

Create/update `CONSOLIDATION.md` with the following structure:

```markdown
# 📦 Project Knowledge Consolidation & Summary

> This document registers the localized context, scripts, custom skills, and lessons learned in this workspace.

---

## 🎯 Project Overview & Status
*   **Mission**: [Brief summary of the project's goal]
*   **Tech Stack**: [Core languages, libraries, APIs used]
*   **Current State**: [What works, what has been verified]

---

## 🛠️ Local Skills Registry

| Skill Name | Path | Purpose | How to Invoke / Reuse |
| :--- | :--- | :--- | :--- |
| `name` | `[link](path)` | [Brief description] | [Instructions or command] |

---

## 📜 Local Scripts & Utilities

| Script File | Path | Purpose | Execution Command |
| :--- | :--- | :--- | :--- |
| `script.py` | `[link](path)` | [Brief description] | `python path` |

---

## 💡 Lessons & Custom Heuristics

### Key Architectural Decisions
*   **Decision X**: We chose [strategy] because [reason].
*   **Decision Y**: We chose [strategy] because [reason].

### Core Development Guidelines
*   *Guideline 1*: Past experience suggests [observation]. It is recommended to [action] to avoid [pitfall].
*   *Guideline 2*: We found that [observation]. When [condition], it is recommended to [action].
```
