# API and Integration Reference

## Overview

The Project Resource Replacement AI Agent integrates Oracle Fusion HCM, Oracle Fusion Project Management, Oracle BI Publisher, and Oracle AI Agent Studio.

---

## HCM Integration

**Business Object:** `ORA_HCM_EMPINFO_SEARCHWORKER`  
**Function:** `getall_workers`  
**REST:** `GET /hcmRestApi/resources/11.13.18.05/workers?q=DisplayName LIKE '{personname}'`  
**Returns:** PersonId, PersonNumber, EmailAddress

---

## Project Team Search

**Business Object:** `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERSEARCH`  
**Function:** `getall_ProjectTeamMembers`  
**Endpoint:** `GET /fscmRestApi/resources/11.13.18.05/projects/{ProjectId}/child/ProjectTeamMembers`  
**Filter:** `FinishDate is null`

---

## Project Search

**Business Object:** `ORA_PRJ_ORAPRJCOMM_SEARCHPROJECT`  
**Function:** `getall_projects`  
**Endpoint:** `GET /fscmRestApi/resources/11.13.18.05/projects/{ProjectId}`

---

## Project Team Member Update

**Business Object:** `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERUPDATE`  
**Operation:** `PATCH /projects/{ProjectId}/child/ProjectTeamMembers/{TeamMemberId}`  
**Payload:** `{ "FinishDate":"2026-06-13" }`

---

## Project Team Member Create

**Business Object:** `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERCREATE`  
**Operation:** `POST /projects/{ProjectId}/child/ProjectTeamMembers`  
**Payload:** `{ "PersonEmail":"sarah.johnson@company.com", "ProjectRole":"Project Manager", "StartDate":"2026-06-13" }`

---

## External Integration (BI Publisher)

**Tool:** `PROJECT_RESOURCE_REPORT`  
**Type:** EXTERNAL_REST / SOAP  
**Endpoint:** `/xmlpserver/services/ExternalReportWSSService`  
**Report:** `/Custom/Financials/Project Reporting.xdo`  
**Input:** `P_EMAIL_ADDRESS`

---

## Oracle AI Agent Studio Integration Patterns

| Pattern | Usage |
| -------------------------- | ----- |
| Business Object Invocation | Yes |
| External REST Integration | Yes |
| SOAP Integration | Yes |
| Dynamic Payload Generation | Yes |
| Parallel Processing | Yes |
