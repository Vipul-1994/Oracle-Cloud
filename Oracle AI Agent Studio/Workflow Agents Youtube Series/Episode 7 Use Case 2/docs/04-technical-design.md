# Technical Design

## Workflow Metadata

| Property | Value |
| -------------- | ------------------------------ |
| Workflow Name | PROJECT_TEAM_REPLACEMENT_AGENT |
| Architecture | Data Pipeline |
| Trigger Type | REST |
| Human Approval | Disabled |
| Loop Type | Parallel |

---

## Node Design

### UNDERSTAND_USER_CONTEXT
- **Type:** LLM — Extract resources from natural language
- **Output:** `{ "status":"success", "outgoing_resource_name":"", "incoming_resource_name":"" }`

### SET_INITIAL_VARIABLES
- **Type:** SET_FIELDS
- **Variables:** `OldProjectMember`, `NewProjectMember`

### FETCH_OUTGOING_WORKER / FETCH_INCOMING_WORKER
- **Type:** BO_FUNCTION — `ORA_HCM_EMPINFO_SEARCHWORKER` → `getall_workers`
- **REST:** `GET /hcmRestApi/resources/11.13.18.05/workers`

### CALL_PROJECT_REPORT
- **Type:** EXTERNAL_REST — `PROJECT_RESOURCE_REPORT` via SOAP (BI Publisher)

### PARSE_REPORT_TO_ARRAY
- **Type:** LLM — Base64 decode → CSV → JSON array of `{ PROJECT_ID, PROJECT_NAME }`

### PROJECT_LOOP (PARALLEL)
Nested pipeline per project:
1. **FETCH_PROJECT_MEMBERS** — `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERSEARCH` (filter: FinishDate is null)
2. **FETCH_PROJECT_DETAILS** — `ORA_PRJ_ORAPRJCOMM_SEARCHPROJECT`
3. **CREATE_SWAP_PAYLOAD** — LLM: locate resource, identify role, calculate dates, generate payloads
4. **END_DATE_OLD_MEMBER** — `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERUPDATE` (PATCH)
5. **CREATE_NEW_PROJECT_TEAM_MEMBER** — `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERCREATE` (POST)
6. **GENERATE_SUMMARY** — LLM: project-level audit summary

### FINAL_MESSAGE
- **Type:** LLM — Aggregate all summaries into human-readable response

---

## Date Calculation Logic

| Scenario | Rule |
|---|---|
| Project End Date = NULL | Use Current Date |
| Current Date < Project End Date | Use Current Date |
| Current Date >= Project End Date | Use Project End Date - 1 Day |

---

## Oracle AI Agent Studio Patterns

| Pattern | Used |
| -------------------------- | ---- |
| Details Extraction | Yes |
| Data Transformation | Yes |
| External REST Integration | Yes |
| Nested Workflow | Yes |
| Parallel Looping | Yes |
| Dynamic Payload Generation | Yes |
| Summary Generation | Yes |
