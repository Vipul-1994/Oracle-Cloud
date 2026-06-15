# Limitations and Lessons Learned

## Overview

This document captures current limitations, architectural trade-offs, and lessons learned during the development of the Project Resource Replacement AI Agent.

---

## Limitations Summary

| # | Limitation | Impact | Recommendation |
|---|---|---|---|
| 1 | Duplicate Worker Names | High | Use Person Number or Email instead of display name |
| 2 | No Resource Availability Validation | Medium | Add capacity check before assignment |
| 3 | No Approval Workflow | High | Add Manager/PMO approval before execution |
| 4 | No Rollback Strategy | High | Implement error logic + rollback workflow |
| 5 | LLM-Based CSV Parsing | Medium | Risk of parsing errors; consider deterministic parser |
| 6 | Large Volume Processing | Medium | Introduce batch processing to avoid API throttling |
| 7 | Project Discovery Dependency | Medium | Create alternate discovery options if report unavailable |

---

## Lessons Learned

1. **Natural Language Improves Adoption** — Users prefer `Replace John Smith with Sarah Johnson` over navigating multiple screens
2. **AI Works Best as an Orchestrator** — Generating payloads and transformations, not replacing business systems
3. **Oracle Fusion APIs Enable Strong Automation** — Using supported APIs ensures maintainability and upgrade compatibility
4. **Role Inheritance Reduces Errors** — Automatically inheriting the outgoing role simplifies transitions
5. **BI Publisher as a Discovery Layer** — Reports expose business relationships not easily accessible via a single API call
6. **Parallel Processing Improves Scalability** — Significantly reduces execution time for multi-project scenarios
7. **Structured Prompting Improves Reliability** — Explicit JSON-only outputs reduce variability and hallucinations

---

## Recommended Production Enhancements

| Enhancement | Priority |
| ---------------------------- | -------- |
| Approval Workflow | High |
| Rollback Capability | High |
| Resource Capacity Validation | High |
| Dry Run Mode | High |
| Batch Processing | Medium |
| Audit Dashboard | Medium |
