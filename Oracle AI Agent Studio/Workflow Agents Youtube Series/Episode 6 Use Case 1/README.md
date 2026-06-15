# Oracle Fusion AP Invoice Processor – Workflow Agent

AI-powered Accounts Payable Invoice Processing Workflow Agent built using Oracle AI Agent Studio and Oracle Fusion Financials.

## Overview

This project demonstrates an end-to-end AP Invoice Processing Workflow Agent built inside Oracle AI Agent Studio. It automates invoice intake, parsing, PO validation, supplier validation, payload generation, and invoice creation directly within Oracle Fusion Financials using REST APIs.

Supports both **PO Matched Invoices** and **Non-PO Invoices**, with Human-in-the-Loop approval for supplier site and business unit validation.

---

## Key Capabilities

- Upload Invoice PDF directly through chat
- Extract invoice data using Chat Attachment Reader
- Parse invoice information using LLM nodes
- Detect whether PO exists and route accordingly
- Retrieve Supplier / Supplier Site / PO details from Oracle Fusion
- Match invoice lines against PO lines
- Human approval workflow for supplier site validation
- Dynamically generate invoice payloads
- Create AP invoices using Oracle Fusion REST APIs
- Send confirmation message/email after processing

---

## Node Types Used

| Node Type | Purpose |
| -------------------- | ------------------------------------------------------ |
| Tool Node | Read Invoice PDF attachment |
| LLM Node | Parse invoice details and generate payloads |
| Condition Node | Check whether PO exists |
| Business Object Node | Fetch supplier, PO, supplier site, and create invoices |
| Human Approval Node | Business unit/site validation |
| Email Node | Send final confirmation |

---

## Oracle Fusion REST APIs Used

- `GET /fscmRestApi/resources/11.13.18.05/suppliers`
- `GET /suppliers/{SupplierId}/child/sites`
- `GET /fscmRestApi/resources/11.13.18.05/purchaseOrders`
- `GET /purchaseOrders/{POHeaderId}/child/lines`
- `POST /fscmRestApi/resources/11.13.18.05/invoices`

---

## Future Enhancements

Multi-invoice batch processing, OCR confidence scoring, Duplicate invoice detection, Invoice policy validation, Autonomous approval routing, AI anomaly detection.

---

*Author: Arpit Paliwal — Oracle ACE | Oracle ERP & AI Consultant*
