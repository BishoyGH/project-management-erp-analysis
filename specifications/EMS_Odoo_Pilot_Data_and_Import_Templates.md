# EMS Odoo Pilot Data and Import Templates

## Sheet: Pilot Summary

| Metric | Value | Basis / clarification |
|--------|-------|----------------------|
| **Project** | Sheikh Zayed Road Tower + Car Park | Plot 3350144 |
| **Client** | SOL Properties Development LLC | Award PO extract |
| **Award value ex VAT (AED)** | 125,000 | Review items 1-7 only |
| **Offered proposal ex VAT (AED)** | 245,000 | Not awarded in full |
| **Proposal non-awarded (AED)** | 120,000 | VE 45k + steel connection 35k + PT 40k |
| **VAT rate** | 0.05 | Verify final tax treatment |
| **Stage 1 net (AED)** | 31,250 | 25% on acceptance + NTP |
| **Stage 2 net (AED)** | 62,500 | 50% upon deliverables |
| **Stage 3 net (AED)** | 31,250 | 25% authority approval |
| **Actual profitability** | NOT AVAILABLE | Requires cost master, timesheets and bills |
| **RFP date flag** | 2026-08-01 in tracker | Later than 2025 PO; confirm |
| **Duration conflict** | 6 weeks vs 10 weeks | Proposal vs tracker |

---

## Sheet: Resource Plan

| Project | Employee | Tracker AED per hour | Tracker engagement % | Planned weekly capacity h | Hours allocated / week | Internal cost AED per h | Planned weekly cost AED | Flag |
|---------|----------|---------------------|---------------------|---------------------------|------------------------|------------------------|------------------------|------|
| SZR-SOL | Mehdi Esmaeili | 500 | 10% | 40 | 4 | | | COST RATE MISSING |
| SZR-SOL | Abraam Emil | 400 | 5% | 40 | 2 | | | COST RATE MISSING |
| SZR-SOL | Zahra Aynedar | 150 | 120% | 40 | 48 | | | CHECK >100% |
| SZR-SOL | Behairy Ahmed | 200 | 40% | 40 | 16 | | | COST RATE MISSING |
| SZR-SOL | Suzanne Alboudi | 150 | 2% | 40 | 0.8 | | | COST RATE MISSING |
| SZR-SOL | Michellyn Abaquin | 100 | 2% | 40 | 0.8 | | | COST RATE MISSING |

---

## Sheet: Timesheet Import

| Entry ID | Date (YYYY-MM-DD) | Employee | Project Code | WBS | Task / activity | Hours | Approval Status | Cost rate snapshot AED/h | Actual cost AED | Billable? | Office |
|----------|-------------------|----------|--------------|-----|----------------|-------|----------------|------------------------|----------------|-----------|--------|
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |
| | | | SZR-SOL | | | | Draft | | | No | |

---

## Sheet: Milestones and Revenue

| Stage | Trigger evidence | Percent | Net contract AED | VAT AED | Gross invoice AED | Eligible? | Invoice issued? | Paid AED | Open balance AED |
|-------|------------------|---------|------------------|---------|-------------------|-----------|----------------|----------|------------------|
| M1 | Acceptance of offer AND NTP | 25% | 31,250 | 1,562.5 | 32,812.5 | No | No | 0 | 0 |
| M2 | Completion of scope and deliverables | 50% | 62,500 | 3,125 | 65,625 | No | No | 0 | 0 |
| M3 | Authority approval and design completion | 25% | 31,250 | 1,562.5 | 32,812.5 | No | No | 0 | 0 |

---

## Sheet: Vendor and Cost Import

| Record | Vendor | Project / Office overhead | PO no | Scope | Committed ex VAT | Billed ex VAT | Paid ex VAT | Cost owner | Status |
|--------|--------|---------------------------|-------|-------|------------------|---------------|-------------|------------|--------|
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |
| | | | | | | | | | Draft |

---

## Sheet: Data Issues

| Issue | Original source | Required resolution | Priority |
|-------|----------------|---------------------|----------|
| RFP date after signed award | Workbook RFP 2026-08-01, PO 2025-09-09 | Validate actual RFP date | Critical |
| Engagement 120% | Tracker Zahra Aynedar 120% | Confirm metric and allocation constraints | Critical |
| 6 vs 10 weeks | Proposal 6, tracker 10 | Approve baseline programme | High |
| No actual dated timesheets | Tracker has staff rate and engagements only | Populate and approve hours | Critical |
| No internal cost ledger | Rates may be charge-out rates | HR/Finance approves private costs | Critical |
| Proposal vs PO scope | Proposal 245k; PO 125k | Exclude unwon scope from baseline | Critical |
| No proof of collections | PO milestones only | Import actual invoices and receipts | High |

---

*Document Version: 1.0*  
*Date: 2025-08-27*  
*Source: EMS Project Proposal & Delivery Tracker.xlsx*