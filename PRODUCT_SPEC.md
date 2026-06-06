# VendorBridge AI — Complete Product Specification

## Executive Summary

VendorBridge AI is an AI-powered procurement platform that reduces RFQ-to-PO cycle time from 45+ days to 7 days through intelligent vendor selection, real-time quotation analysis, and automated approval workflows.

**Core Value Proposition:** Every other procurement tool gives you a database. VendorBridge AI gives you an AI Procurement Officer that works 24/7.

---

## Key Features

### 1. AI Procurement Copilot
- Natural language interface to create RFQs
- Smart vendor recommendations based on category and trust score
- Answer questions about procurement data
- Generate procurement reports in seconds

### 2. Vendor Trust Score Algorithm
Dynamic 0–100 scoring based on:
- **Price Competitiveness (25%)** — How competitively priced vs market average
- **Delivery Performance (30%)** — On-time delivery percentage
- **Response Speed (15%)** — How quickly vendor responds to RFQs
- **Quote Win Rate (15%)** — Percentage of quotes that won contracts
- **Dispute-Free Rate (15%)** — Percentage of invoices without disputes

### 3. AI Quotation Analyzer
Automatic analysis of all received quotations:
- Best Price winner
- Fastest Delivery winner
- Best Overall Value winner
- Risk flags for each quotation
- Market context and recommendations

### 4. Risk Detection Engine
Real-time monitoring for 7 risk signals:
- Price spike detection (25%+ above average)
- Overbudget quotations
- Vendor reliability risks
- Approval bottlenecks
- Single-vendor dependency
- RFQ deadline misses
- Invoice 3-way match failures

### 5. Real-Time Procurement Dashboard
- Live KPI cards (Active RFQs, Pending Approvals, Month Spend, Risk Score)
- RFQ tracking with quotation progress
- Approval queue with AI recommendations
- Spend analytics by category
- Vendor risk alerts

### 6. One-Click PO & Invoice Pipeline
- Auto-generate Purchase Orders from approved quotations
- Automatic 3-way invoice matching (PO ↔ Receipt ↔ Invoice)
- PDF generation and email delivery via Resend

---

## User Roles & Access

| Role | Can Create RFQ | Can Approve | Can Submit Quote | Can View Analytics |
|------|---|---|---|---|
| **Admin** | ✅ | ✅ | ❌ | ✅ Full |
| **Manager** | ✅ | ✅ | ❌ | ✅ Dept |
| **Officer** | ✅ | ❌ | ❌ | ✅ Limited |
| **Vendor** | ❌ | ❌ | ✅ | ✅ Own only |

---

## Complete User Flow

### Internal User (Procurement Officer)
1. Login
2. View Dashboard (AI briefing, KPIs, alerts)
3. Use AI Copilot: "Create RFQ for 100 laptops, $80k budget"
4. AI auto-fills RFQ form, recommends vendors
5. Publish RFQ (emails sent to vendors via Resend)
6. Wait for quotations
7. Review AI Quotation Analysis (winner cards, AI recommendation)
8. Click "Award to Vendor"
9. Manager approves
10. PO auto-generated and emailed to vendor
11. Vendor submits invoice
12. AI runs 3-way match (auto-approved if matched)
13. View analytics report on dashboard

### Vendor User
1. Receive RFQ invitation email with magic link
2. Click link → vendor portal opens (no login required)
3. Review RFQ specs
4. Fill in quotation (prices, delivery date, terms)
5. Submit quotation
6. Receive notification when awarded
7. Get PO via email
8. Submit invoice through portal
9. Track payment status

---

## API Architecture (40+ endpoints)

### Authentication
- `POST /api/auth/login` — Login with email/password
- `POST /api/auth/logout` — Logout
- `GET /api/auth/session` — Get current session

### Vendors
- `GET /api/vendors` — List vendors (paginated, filterable)
- `POST /api/vendors` — Create vendor
- `GET /api/vendors/[id]` — Get vendor details
- `PUT /api/vendors/[id]` — Update vendor
- `GET /api/vendors/[id]/analytics` — Get vendor trust score breakdown

### RFQs
- `GET /api/rfqs` — List RFQs
- `POST /api/rfqs` — Create RFQ + send vendor invites
- `GET /api/rfqs/[id]` — Get RFQ details
- `PUT /api/rfqs/[id]` — Update RFQ

### Quotations
- `GET /api/quotations` — List quotations
- `POST /api/quotations` — Vendor submits quotation
- `GET /api/rfqs/[id]/quotations` — Get all quotes for RFQ
- `POST /api/ai/analyze-quotes` — Trigger AI analysis

### Approvals
- `GET /api/approvals` — Get pending approvals
- `POST /api/approvals/[id]/decide` — Approve/reject with comments

### Purchase Orders
- `POST /api/purchase-orders/generate` — Generate PO from quotation
- `GET /api/purchase-orders` — List POs
- `GET /api/purchase-orders/[id]` — Get PO details
- `GET /api/purchase-orders/[id]/pdf` — Download PO PDF

### Invoices
- `GET /api/invoices` — List invoices
- `POST /api/invoices` — Vendor submits invoice
- `POST /api/invoices/[id]/match` — Run 3-way match

### AI
- `POST /api/ai/copilot` — Chat with AI Copilot
- `POST /api/ai/analyze-quotes` — Analyze quotations
- `POST /api/vendors/trust-score` — Calculate trust score

### Analytics
- `GET /api/analytics/dashboard` — Dashboard KPIs
- `GET /api/analytics/spend` — Spend by category
- `GET /api/analytics/vendor-performance` — Vendor metrics

---

## Technology Stack

**Frontend:**
- Next.js 15 (React 19, TypeScript)
- Tailwind CSS + Shadcn UI components
- Framer Motion (animations)
- Recharts (data visualization)
- Zustand (state management)

**Backend:**
- Next.js API routes (Node.js)
- Supabase (PostgreSQL)
- Google Gemini 2.5 Flash (AI)
- Resend (email delivery)

**Deployment:**
- Vercel (frontend + backend)
- Supabase (database)

---

## Success Metrics

- **Cycle Time:** RFQ to PO in 7 days (vs 45+ days baseline)
- **Cost Savings:** 12–18% reduction through better vendor selection
- **Accuracy:** 99%+ 3-way match accuracy
- **Adoption:** 80%+ user adoption within 30 days
- **Satisfaction:** 4.5+/5 user satisfaction score

---

For complete implementation details, see `HACKATHON_PLAN.md`.
