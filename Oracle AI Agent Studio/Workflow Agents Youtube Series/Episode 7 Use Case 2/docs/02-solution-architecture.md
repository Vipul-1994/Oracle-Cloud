# Solution Architecture

## Architecture Overview

The Project Resource Replacement AI Agent orchestrates multiple Oracle Fusion services and AI components to automate project resource replacement.

The architecture combines:

* Oracle AI Agent Studio
* Oracle Fusion HCM
* Oracle Fusion Project Management
* Oracle BI Publisher
* Oracle Fusion REST APIs
* Large Language Models

---

## Component Responsibilities

### AI Agent Studio Layer

Acts as the orchestration engine.

Responsibilities:
* Workflow execution
* Variable management
* Node orchestration
* Loop execution
* Tool invocation
* Response generation

### Oracle Fusion HCM Layer

Used to fetch worker identities. Business Object: `ORA_HCM_EMPINFO_SEARCHWORKER`

### Oracle BI Publisher Layer

Provides project discovery capability. External Tool: `PROJECT_RESOURCE_REPORT`

### Oracle Fusion Projects Layer

Used for project resourcing operations. Business Objects:
* `ORA_PRJ_ORAPRJCOMM_SEARCHPROJECT`
* `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERSEARCH`
* `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERUPDATE`
* `ORA_PRJ_ORAPRJCOMM_PROJECTMEMBERCREATE`

### LLM Processing Layer

Used for: Entity Extraction, Report Transformation, Payload Generation, and Summary Generation.

---

## Design Principles

* **Reusability**: Business logic is reusable across resource types.
* **Scalability**: Supports multiple project assignments.
* **Maintainability**: Uses standard Oracle Fusion APIs.
* **Extensibility**: Additional validations and approvals can be added.
* **Governance**: Updates occur through supported Oracle Fusion interfaces.
