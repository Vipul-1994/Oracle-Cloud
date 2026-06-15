# Oracle Fusion AP Invoice Processor – Architecture

## Solution Overview

This solution demonstrates an AI-powered Accounts Payable Invoice Processing Workflow Agent built using Oracle AI Agent Studio, Oracle Fusion Financials, REST APIs, Workflow Agents, LLM-based reasoning, and Human-in-the-Loop approvals.

---

## Core Architecture Pattern

Invoice Input → AI Extraction → Validation → Decision Routing → Human Review → Payload Generation → Oracle Fusion Transaction Creation

---

## Workflow Stages

### Stage 1 – Invoice Intake
- **Node:** Tool Node (Chat Attachment Reader) — accepts invoice PDF, extracts raw text

### Stage 2 – Invoice Parsing
- **Node:** LLM Node — extracts Invoice Number, Date, Due Date, Supplier Name, Amount, PO Number, Invoice Lines → structured JSON

### Stage 3 – Workflow Decision Routing
- **Node:** Condition Node — checks if PO Number exists
  - PO Exists → PO Invoice Flow
  - PO Missing → Non-PO Invoice Flow

---

## PO Invoice Flow

1. **Fetch PO Details** — `purchaseOrders` REST API (PO Header, Supplier Site, Procurement BU)
2. **Fetch PO Lines** — retrieve lines for matching
3. **PO Line Matching** — LLM compares Description, Unit Price, Quantity between invoice and PO lines
4. **Build PO Invoice Payload** — LLM generates Oracle Fusion AP Invoice JSON
5. **Create Invoice** — `POST /invoices`

---

## Non-PO Invoice Flow

1. **Fetch Supplier Details** — retrieve supplier info
2. **Fetch Supplier Sites** — retrieve sites and Procurement BUs
3. **AI Supplier Site Validation** — LLM evaluates supplier site and BU combinations
4. **Human Approval** — user confirms supplier site and business unit
5. **Build Non-PO Payload** — LLM generates payload
6. **Create Invoice** — `POST /invoices`

---

## Oracle Fusion APIs Used

| API | Purpose |
| ------------------------------- | ------------------ |
| suppliers | Supplier retrieval |
| suppliers/{id}/child/sites | Supplier sites |
| purchaseOrders | PO retrieval |
| purchaseOrders/{id}/child/lines | PO line retrieval |
| invoices | Invoice creation |

---

## Future Enhancements

- Confidence scoring, Duplicate invoice detection, Autonomous approvals
- AI anomaly detection, Invoice hold automation, Multi-agent orchestration
