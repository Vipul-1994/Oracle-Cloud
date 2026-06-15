# Prompt Engineering Strategy

A major portion of this workflow agent relies on carefully engineered LLM prompts to ensure deterministic ERP transaction processing. The workflow uses structured enterprise prompts optimized for JSON extraction, Oracle Fusion payload generation, PO matching, supplier validation, and ERP-safe response formatting.

---

## Key Prompt Design Principles

### 1. Strict JSON Enforcement
All payload-generation prompts explicitly enforce valid JSON output — no markdown fences, no conversational text, JSON-only response.

### 2. Invoice Extraction Prompt
Extracts: Invoice Number, Date, Due Date, Supplier Info, PO Number, Invoice Lines, Quantities, Unit Prices, Total. Also includes currency normalization, date standardization, and mathematical sanity validation (line totals vs header totals).

### 3. Supplier Site Validation Prompt
AI evaluates supplier site and procurement BU combinations — detects single vs multiple sites, structures recommendations, prepares data for Human-in-the-Loop approval.

### 4. Human Approval Interpretation Prompt
Interprets free-text user feedback (e.g., "Use US1", "First option", "Use Vision BU") and maps back to Supplier Site + Procurement BU — creating a conversational approval experience.

### 5. PO Invoice Payload Generation Prompt
Combines extracted invoice data, PO header, and PO lines. Performs description/unit price/PO line number matching and generates a fully structured Oracle Fusion AP Invoice payload.

### 6. Non-PO Payload Generation Prompt
Uses validated supplier site info, maps procurement BUs, builds invoice lines dynamically, constructs Oracle Fusion invoice payload JSON.

### 7. Confirmation Message Prompt
Converts raw API responses into business-friendly summaries — formats line details, highlights invoice numbers and amounts, improves operational readability.

---

## Enterprise AI Design Pattern

Input → Extraction → Validation → Reasoning → Human Approval → Payload Generation → ERP Transaction Creation

LLM nodes serve as: Intelligent parsers, Validation engines, Decision support systems, and Structured payload generators — not simple chatbots.
