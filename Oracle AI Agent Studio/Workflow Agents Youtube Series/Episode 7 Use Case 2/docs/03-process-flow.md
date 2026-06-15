# Process Flow

## Overview

The Project Resource Replacement AI Agent follows a multi-stage orchestration pattern combining Oracle Fusion HCM, Oracle Fusion Projects, BI Publisher, External REST integrations, and LLM-based processing.

The workflow identifies an outgoing resource, discovers impacted projects, performs resource replacement activities, and generates a consolidated execution summary.

---

## Key Steps

1. **Understand User Context** — Natural language entity extraction to identify outgoing and incoming resources
2. **Set Initial Variables** — Store extracted resources as workflow variables (`OldProjectMember`, `NewProjectMember`)
3. **Fetch Outgoing Worker** — Resolve worker info from HCM using `ORA_HCM_EMPINFO_SEARCHWORKER`
4. **Fetch Incoming Worker** — Validate incoming worker and retrieve email
5. **Call Project Resource Report** — BI Publisher SOAP service to identify all impacted projects
6. **Parse Report Output** — Base64 decode → CSV → JSON array of projects
7. **Project Loop (Parallel)** — Process all projects simultaneously for speed and scalability
8. **Fetch Project Members** — Get active team members using `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERSEARCH`
9. **Fetch Project Details** — Retrieve metadata using `ORA_PRJ_ORAPRJCOMM_SEARCHPROJECT`
10. **Create Swap Payload** — Identify resource, determine role, calculate dates, generate payloads
11. **End-Date Existing Resource** — PATCH `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERUPDATE`
12. **Create Replacement Resource** — POST `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERCREATE`
13. **Generate Project Summary** — Per-project audit summary via LLM
14. **Generate Final Message** — Aggregate consolidated execution summary

---

## Oracle AI Agent Studio Patterns Used

| Pattern | Usage |
| -------------------------- | ----- |
| Entity Extraction | Yes |
| Variable Management | Yes |
| Business Object Invocation | Yes |
| External REST Integration | Yes |
| LLM Data Transformation | Yes |
| Dynamic Payload Generation | Yes |
| Parallel Loop Processing | Yes |
| Human Readable Summaries | Yes |
