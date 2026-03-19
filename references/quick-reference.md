# Spec Vibe Coding quick reference

## Commands the user might say

| User says | What to do |
|---|---|
| "I want to build..." / "help me make..." | Start Phase 0 (kickoff) |
| "specflow" / "let's plan this" | Start Phase 0 or resume from last state |
| "requirements" / "PRD" / "what should it do" | Jump to Phase 1 |
| "architecture" / "tech stack" / "system design" | Jump to Phase 2 |
| "UI" / "design" / "what should it look like" | Jump to Phase 3 |
| "tasks" / "let's start coding" / "dev plan" | Jump to Phase 4 |
| "quality check" / "review everything" | Jump to Phase 5 |
| "skip this" / "next phase" | Move to the next phase |
| "show progress" / "where are we" | Print the progress summary |
| "update the feature list" / "add X to PRD" | Edit the relevant document, note downstream impacts |

## Progress display format

```
Spec Vibe Coding progress: {Project name}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Blueprint    ✅ complete
Requirements ✅ 6/6 sections
System design 🔵 3/6 sections
UI/UX design  ⬜ not started
Dev tasks     🔒 needs system design
Quality check 🔒 needs all phases
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Example: completed blueprint

For a project called "InvoiceFlow — Invoice management for freelancers":

```markdown
# Project blueprint: InvoiceFlow

## One-line description
A desktop tool that helps freelancers create, send, and track invoices without leaving their workflow.

## Problem statement
Freelancers waste 2-3 hours per week on invoicing — switching between spreadsheets, email, and payment platforms. They need a single tool that handles the full invoice lifecycle: create → send → track payment → remind.

## Target users
- **Solo freelancer** — Designer/developer, 5-15 clients, wants speed and simplicity
- **Small agency owner** — 2-5 team members, needs team-level invoice tracking
- **Part-time contractor** — Side gig alongside full-time job, invoices monthly

## Core features (initial)
1. Create invoices from templates (with line items, tax, discounts)
2. Send invoices via email (PDF attachment)
3. Payment status tracking (sent → viewed → paid → overdue)
4. Client management (contact info, payment terms, history)
5. Recurring invoices (auto-generate on schedule)
6. Dashboard with outstanding amount and monthly summary
7. Export to CSV/PDF for accounting

## Technical direction
- Platform: macOS desktop (Tauri + React + TypeScript)
- Local-first with optional cloud sync later
- SQLite for data storage
- PDF generation for invoice output

## Estimated complexity
Medium — Core CRUD is straightforward, but PDF generation, email sending, and recurring schedule logic add real complexity.

## Next steps
Start with Phase 1 (Requirements) — the feature list needs acceptance criteria and the user flows need error case coverage.
```

## Example: task prompt (from Phase 4)

```markdown
## Task 3: Invoice CRUD API

**Priority:** P0
**Type:** Backend
**Estimated time:** ~1.5h
**Dependencies:** Task 1 (project scaffold), Task 2 (DB schema)
**Files involved:** src/api/invoices.ts, src/models/invoice.ts, src/services/pdf.ts

### Prompt

You are working on InvoiceFlow, a Tauri + React + TypeScript desktop app
for freelance invoice management. The project scaffold (Task 1) and
database schema (Task 2) are already complete.

Implement the invoice CRUD API with these endpoints:

POST /api/invoices — Create a new invoice
  Request: { client_id, line_items: [{description, quantity, unit_price}],
             tax_rate?, discount?, due_date, notes? }
  Response: 201 { invoice: InvoiceObject }
  Validation: client_id must exist, at least 1 line_item required,
              due_date must be in the future

GET /api/invoices — List all invoices
  Query params: ?status=draft|sent|paid|overdue&client_id=X&sort=date|amount
  Response: 200 { invoices: InvoiceObject[], total: number }

GET /api/invoices/:id — Get single invoice with line items
PUT /api/invoices/:id — Update invoice (only if status is "draft")
DELETE /api/invoices/:id — Soft delete (only if status is "draft")

Data model (from Task 2):
  invoices: id, client_id(FK), invoice_number(auto), status(enum),
            subtotal, tax_rate, tax_amount, discount, total,
            due_date, notes, created_at, updated_at
  line_items: id, invoice_id(FK), description, quantity, unit_price, amount

Technical notes:
- invoice_number auto-generates as "INV-{YYYYMM}-{sequential}"
- total = subtotal + tax_amount - discount (compute on save)
- Use existing db connection from src/lib/database.ts

### Acceptance criteria
- [ ] POST creates invoice with auto-generated invoice_number
- [ ] POST validates required fields, returns 400 with clear errors
- [ ] GET list supports filtering by status and client
- [ ] PUT rejects updates to non-draft invoices with 409
- [ ] DELETE is soft-delete (sets deleted_at, doesn't remove row)
- [ ] All endpoints return proper error codes and messages
```
