# AI Design and Prompts

## Overview

The Project Resource Replacement AI Agent uses LLMs as orchestration components within Oracle AI Agent Studio — responsible for details extraction, data transformation, payload generation, and human-readable summarization.

---

## AI Capability Matrix

| Capability | Purpose |
| ---------------------- | ---------------------------------------- |
| Details Extraction | Identify outgoing and incoming resources |
| Context Interpretation | Determine replacement direction |
| Data Transformation | Convert report output to JSON |
| Payload Construction | Generate API payloads |
| Date Reasoning | Calculate start and finish dates |
| Summary Generation | Produce user-friendly updates |

---

## Prompt 1 – Understand User Context

**Objective:** Extract outgoing and incoming resources from natural language.

**Supported Patterns:** `replace [A] with [B]`, `swap out [A] for [B]`, `change PM from [A] to [B]`, etc.

**Output:**
```json
{
  "status":"success",
  "outgoing_resource_name":"John Smith",
  "outgoing_resource_formatted":"%John%Smith%",
  "incoming_resource_name":"Sarah Johnson",
  "incoming_resource_formatted":"%Sarah%Johnson%"
}
```

---

## Prompt 2 – Parse Report To Array

**Objective:** Convert BI Publisher XML → Base64 → CSV → JSON array.

**Output:**
```json
[
  { "PROJECT_ID":"300000111111", "PROJECT_NAME":"ERP Program" },
  { "PROJECT_ID":"300000222222", "PROJECT_NAME":"Finance Program" }
]
```

---

## Prompt 3 – Create Swap Payload

**Objective:** Generate Oracle Fusion API payloads dynamically.

**Outgoing Payload:**
```json
{ "ProjectId":"300000111", "TeamMemberId":"300000222", "FinishDate":"2026-06-13" }
```

**Incoming Payload:**
```json
{ "PersonEmail":"sarah.johnson@company.com", "ProjectRole":"Project Manager", "StartDate":"2026-06-13" }
```

---

## Prompt 4 – Generate Summary

**Output:** `On ERP Program, John Smith was end-dated on 13-Jun-2026 and replaced by Sarah Johnson starting on 13-Jun-2026.`

---

## Prompt 5 – Final Message

**Output:** Consolidated execution results across all projects.

---

## AI Design Principles

- **Structured Outputs** — All prompts return machine-readable JSON
- **Explicit Instructions** — Expected format, required fields, error handling specified
- **JSON First Design** — Every downstream process relies on structured JSON
- **Deterministic Prompting** — Reduces hallucinations by explicitly defining input interpretation and response format

---

## AI Patterns Demonstrated

| Pattern | Usage |
| ---------------------- | ----- |
| Details Extraction | Yes |
| Data Transformation | Yes |
| JSON Generation | Yes |
| Payload Generation | Yes |
| Date Reasoning | Yes |
| Narrative Generation | Yes |
