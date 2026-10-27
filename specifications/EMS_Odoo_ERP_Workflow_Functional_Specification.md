# EMS Odoo ERP Workflow Functional Specification

## Overview

**EMS project lifecycle in Odoo**

Functional requirements, workflow specification, data structure and demonstration acceptance criteria

**Pilot project:** Sheikh Zayed Road Tower, Plot 3350144 (B+G+59+R) and car park | **Client:** SOL Properties Development LLC

**Purpose:** Configure one continuous, auditable process from prospect/client registration through proposal, negotiation, contract/PO, resource planning, execution, timesheets, vendor costs, invoicing, collections and project profitability.

---

## 1. Executive Implementation Requirements

Odoo should treat the CRM opportunity as the originating commercial record, but treat the signed award as the controlling scope and price. The project must be created from an approved contract/PO, with linked analytic account, baseline budget, work breakdown structure (WBS), timesheets, vendor commitments, delivery evidence, invoice milestones and cash receipts. Every revision, approval and variation must retain an audit trail.

**Pilot commercial baseline:** Client PO is AED 125,000 excluding VAT for review services. This is narrower than the AED 245,000 excluding VAT package in the submitted proposal. Optional or excluded services must NOT become contracted revenue or approved tasks automatically.

---

## 2. Primary Workflow / Status Gates

| Stage | Odoo record / status | Required entry and approval | Output / automated action |
|-------|---------------------|----------------------------|---------------------------|
| 01 Lead registration | CRM lead → Qualified | Client company, contacts, source, developer, project, authority, expected scope | Unique client/opportunity; duplicate check |
| 02 Opportunity and RFP | Opportunity → RFP received | RFP, location, plot, BUA, due dates, service types, expected fee, probability | Opportunity number; RFP checklist and documents |
| 03 Bid / no-bid | Bid evaluation → Approved to quote | Capacity, conflict-of-interest, expected hours, margin, risk | Bid approval; commercial/technical owner assigned |
| 04 Proposal | Quotation / proposal → Sent | Revision, technical scope, exclusions, options, prices, VAT, validity, schedule | Locked PDF revision and approval history |
| 05 Negotiation | Opportunity → Negotiating | Client comments, BAFO versions, discounts, offered versus awarded scope | Version comparison and approval for change |
| 06 Award / contract | PO/LOA/contract → Verified | Signed acceptance/PO, amount, billing schedule, scope reconciliation, NTP | Sales order + contract baseline; no unsupported items |
| 07 Project initiation | Project → Planned | PM/technical lead, WBS, deliverables, resource hours, cost rates, vendor budget | Analytic account, budget, project code, schedule |
| 08 Mobilization | Project → Authorized to start | NTP/authority to proceed per contract and prerequisites | Release timesheets and delivery tasks |
| 09 Technical delivery | Tasks → In progress → Internal QA → Issued | Document receipt, review assignment, CRS, VEMS, reports, revisions | Approval stamps, actual hours, progress %, client transmittals |
| 10 Variation | Change request → Approved / Rejected | Trigger, reason, impact on fees, hours, programme, signed client approval | Separate sales order line/budget version |
| 11 Billing | Milestone → Eligible → Invoice posted | Evidence of payment trigger; accounting approval | Invoice, VAT, aging, payable milestone balance |
| 12 Collection / closure | Paid; Deliverables closed; Project closed | Payment reconciliation, client approval, open comments, final cost | Actual margin, write-offs, lessons learned, locked closeout |

---

## 3. Pilot Source Reconciliation — Mandatory Before Configuration

| Item | Source information | Odoo treatment |
|------|-------------------|----------------|
| **Project** | Sheikh Zayed Road Tower + car park; plot 3350144; DM; proposal BUA tower 72,000 m² + car park 22,616 m² | Project master data; precise BUA appears to differ from rounded fee table (~94,000 m²). |
| **Proposal** | 20 Aug 2025 revised proposal; AED 245,000 ex VAT (125k peer review + 45k VE + 35k connection + 40k PT). Optional PBSD 195k and geotechnical 60k. | Maintain proposal as historical offered scope, not contract baseline. |
| **Client PO / award** | Signed PO extract dated 09 Sep 2025; AED 125,000 for review items 1–7 only. | Awarded sales order: review AED 125,000, subject to full PO/contract verification. |
| **Payment terms** | 25% at acceptance/NTP; 50% upon completion of scope/deliverables; 25% at authority approval / design completion. Invoice payment 15 days. | Milestones: 31,250 / 62,500 / 31,250 AED, excluding VAT; triggers not simply elapsed dates. |
| **Schedule** | Proposal: initial review 2 weeks; enabling/piling 1 week; final review/certificate 3 weeks (6 weeks stated). | Versioned project baseline; working-day dependencies and wait states. |
| **Tracker actual fields** | Sheet1: RFP, proposal revisions R00/R01, client response, official document, fee, stages, personnel/rates/engagement, weeks, conclusion. | Import crosswalk; preserve original spreadsheet as attachment. |
| **Data quality conflicts** | Tracker RFP date 01 Aug 2026 after Sep 2025 PO; R00 submission 02 Aug 2025, R01 20 Aug 2025; allocated 120% to one staff member; tracker 10 weeks. | Flag for validation, do not silently correct. 120% may mean over-allocation or nonstandard measurement. |
| **Unverified full contract** | Only one-page signed PO extract available; no full document set, cost payroll ledger or actual timesheet entries provided. | Mark source-document completeness pending; profit remains estimated until cost master and actuals validated. |

---

## 4. Odoo Modules and Record Relationships

| Odoo module / component | Mandatory configuration and link |
|------------------------|----------------------------------|
| **Contacts + CRM** | Client legal entity, role-based contacts, developer/end client/consultant, opportunity history and activities. |
| **Sales / quotations** | Multi-revision commercial proposal, line-by-line scope/options, discount authority, VAT, contract acceptance. |
| **Documents + Sign (if licensed)** | RFP, proposal revisions, PO/LOA, NTP, vendor contracts, issue transmittals, certificates, approval records. |
| **Project + Planning** | Project template by service; stages, dependencies, resource allocation by staff/week, capacity vs other jobs. |
| **Timesheets + Employees** | Time by employee/date/project/task/stage, description, billable/nonbillable, approval, internal cost basis. |
| **Accounting + analytic plans** | One analytic project account; invoices and receipts; expense/revenue journal allocation; cost and margin reporting. |
| **Purchase + Vendor Bills** | Subconsultant/outsourcing PO, contracted deliverables, commitments, vendor invoice/payment tracking. |
| **Expenses / payroll linkage** | Approved travel and reimbursables; cost rates from confidential internal master, not client billable rates. |
| **Studio / small custom module** | Project scope comparison, milestone eligibility, engineering deliverables, CRS tracker, VE and variation register, profitability snapshot. |

**Configuration requirement:** Maintain one immutable linked key chain: Client ID → Opportunity ID → Proposal revision → Signed award / Sales Order → Project ID → Analytic Account ID. Vendor purchase orders and invoices must explicitly reference Project ID or "Office Overhead", never attach office purchases to projects by default.

---

## 5. Data Dictionary and Relational Records

| Entity | Essential fields / relationships |
|--------|----------------------------------|
| **Client / Contact** | legal_name, TRN, billing_address, contact_name, email, role, payment_terms, currency |
| **Opportunity** | opportunity_id, client_id, project_name, location, plot_no, authority, service, RFP_date, value, probability, owner, bid_decision |
| **Proposal revision** | proposal_id, revision_no, issued_date, valid_to, service_lines, exclusions, options, VAT, file, prepared/reviewed/approved_by |
| **Award / contract** | award_id, PO_type, PO_no, client_sign_date, NTP_date, acceptance, award_amount_exVAT, payment_terms, signed_attachment, baseline_version |
| **Project / stage / task** | project_id, contract_id, stage_code, deliverable_id, assigned_staff, start/finish baseline and forecast, dependencies, QA status |
| **Resource plan** | project, employee, role, office, week, allocated_hours, available_hours, forecast_cost_hourly, allocation_percentage |
| **Timesheet** | employee, date, project, stage, task, hours, activity, internal_cost_rate_snapshot, status, approver, expense_analytic_account |
| **Vendor commitment** | vendor, project/overhead, scope, PO_value, service_dates, invoice_ids, paid_amount, accrual, remaining_commitment |
| **Milestone / invoice** | stage_trigger, contract_percent, exVAT_amount, evidence, eligible_date, invoice_id, due_date, paid_amount, residual |
| **Variation / risk / NCR** | change_id, scope_reason, quotation, approval_status, added_days, added_budget, CRS_comment_ref, technical_owner, resolution |
| **Profit snapshot** | baseline_revenue, approved_variations, planned_labor, actual_labor, third_party_cost, expenses, overhead_basis, billed, collected, margin |

---

## 6. Technical Project Template — Structural Third-Party Review

| WBS | Delivery task / acceptance | Gate / deliverable |
|-----|---------------------------|-------------------|
| **P0** | Contract / NTP check; RFP scope matrix; document register; kickoff | Project baseline accepted |
| **P1** | Receive structural/architectural plans, analysis models, geotechnical information, design criteria and supporting studies; log missing data | Review readiness checklist |
| **P2** | Initial assessment: gravity/lateral system, load path, primary model checks, drawing coordination | Initial comments / CRS |
| **P3** | Review enabling works and piling package, as applicable to PO | Piling report / letter |
| **P4** | Detailed analysis and code review; issue CRS and standard VE observations | Detailed CRS, markups, technical report |
| **P5** | Receive designer response, classify comments open/closed/accepted risk, conduct meetings and re-check | Comment close-out evidence |
| **P6** | Final internal independent check, approval and authority submission response | Certificate / stamped drawings subject to requirements |
| **P7** | Commercial closure and archive, final invoice and client/authority approval | Accepted handover, financial close |

Timesheets must be attributable to P0–P7 and to the named employee. Work outside the signed scope, such as independent premium modeling, PBSD or full VE redesign, should create a proposed variation, not quietly consume the base fee.

---

## 7. Resource Plan and Time-Entry Rules

| Named team member | Tracker rate (AED/h) | Tracker engagement | Pilot classification |
|------------------|---------------------|-------------------|---------------------|
| Mehdi Esmaeili | 500 | 10% | Provisional planned allocation |
| Abraam Emil | 400 | 5% | Provisional planned allocation |
| Zahra Aynedar | 150 | 120% | Exception: exceeds ordinary single-person capacity |
| Behairy Ahmed | 200 | 40% | Provisional planned allocation |
| Suzanne Alboudi | 150 | 2% | Provisional planned allocation |
| Michellyn Abaquin | 100 | 2% | Provisional planned allocation |

The supplied tracker lists these role-based planning figures; they are NOT verified payroll cost rates and the percentages are not actual recorded time. Odoo should import them as provisional planning assumptions pending staff rate/availability confirmation.

Resource planning should be in HOURS by employee per week; engagement % is calculated as planned project hours ÷ available productive hours. Multiple-project allocation must respect shared capacity.

Enter actual hours each day against a WBS task; project manager approves weekly. Reject or flag negative hours, missing descriptions and overlapping capacity.

Maintain distinct confidential **INTERNAL COST RATE**, **CLIENT BILLING RATE** and **PLANNING RATE** (source tracker). Do not treat 500 AED/h as payroll expense without verification.

Approval freeze preserves the cost-rate snapshot on the timesheet to avoid changing historical project margin after a staff salary/rate update.

Permit Dubai, Cairo, remote and external freelancer resources with reporting by office and company currency; apply exchange rate policy where needed.

---

## 8. Budget, Costing and Profit Calculations

| Metric | Definition / calculation |
|--------|-------------------------|
| **Contracted revenue** | Signed award ex VAT + approved signed variations ex VAT; unaccepted proposal options excluded. |
| **Planned labour cost** | Σ (planned hours × internally approved forecast cost per hour). |
| **Actual labour cost** | Σ (approved actual hours × historical internal cost rate). |
| **Committed external cost** | Open approved vendor PO amounts not yet posted as bill costs; avoid double counting. |
| **Actual direct cost** | Labour actual + posted vendor bills + approved direct project expenses + other allocated actual costs. |
| **Estimate at completion (EAC)** | Actual direct costs + estimate to complete (remaining labour, vendor commitments and forecast expenses). |
| **Forecast gross margin** | (Contracted revenue − EAC) / contracted revenue × 100. |
| **Realized gross margin** | (Recognized revenue − costs matched to that recognition) / recognized revenue; accounting policy to confirm. |
| **Cash collection** | Customer receipts reconciled to posted invoices; outstanding = posted invoices − applied receipts/credits. |
| **Budget deviation** | Actual hours − approved baseline hours; cost variance = actual + forecast remaining − approved budget. |
| **Overhead** | Separate optional allocation under approved methodology; show margin before and after overhead rather than mixing them. |

**Pilot billing illustration:** AED 125,000 ex VAT; milestones AED 31,250 + AED 62,500 + AED 31,250. For a 5% VAT scenario, total VAT AED 6,250, total invoiced incl VAT AED 131,250. VAT is a tax liability and must not be counted as project revenue/profit. These are contract-value illustrations, NOT evidence invoices were issued or paid.

Project cost/profit cannot be credibly calculated from the submitted Excel because it contains engagement percentages/rates, not actual dated timesheets, validated cost rates, vendor bills or a cost allocation policy.

---

## 9. Controls, Permissions and Approval Matrix

| Action | Responsible / authorizing role | Enforced control |
|--------|-------------------------------|------------------|
| Create opportunity / contacts | Business development or PM | Deduplicate client / contacts |
| Approve proposal / discounts | Commercial director / authorized management | Signed approval and controlled revision history |
| Approve signed contract baseline | Management + Finance | PO matching and reconciliation of awarded scope |
| Approve resource plan/budget | Project manager + Finance/management | Capacity and margin review before mobilization |
| Submit timesheets | Assigned employee | Task, hours, date mandatory |
| Approve timesheets / delivery | PM; technical lead for technical outputs | No self-approval for designated control gates |
| Approve vendor PO / variation | Authorized commercial approver | Limits of authority; client approval evidence for variation |
| Approve invoice posting | Finance | Milestone eligibility and approved sales amount check |
| Close project | PM + Finance + management | Technical issues, open PO, unbilled WIP, AR and costs reviewed |

---

## 10. Required Management Dashboards

1. **CRM funnel:** lead → qualified → RFP → proposed → negotiating → won/lost; total weighted pipeline, conversion time and proposal age.

2. **Portfolio:** contracted revenue, project stage, revised end date, deliverable status, technical comments, payment overdue and forecast margin.

3. **Resource:** weekly planned versus actual hours, utilization by person and office, double-booked staff, projected overrun and unapproved timesheets.

4. **Project economics:** original award versus approved variations; labor cost, vendor commitments, forecast EAC, gross margin, cash collection and accounts receivable aging.

5. **Finance:** invoice milestone eligibility, amount invoiced, client receipt, unpaid balance, VAT separately, vendor PO/invoice/payment matching.

6. **Audit:** who changed prices, rates, milestone triggers, WBS baseline and task closure, with timestamp and revision.

---

## 11. Mandatory Odoo Demonstration Scripts / UAT

| Test | Acceptance result |
|------|-------------------|
| **A.** Register SOL and plot | Single client and opportunity created with contact, RFP and technical attachments. |
| **B.** Enter original proposal AED 245,000 and revised version | System tracks revisions and optional services separately. |
| **C.** Import signed PO AED 125,000 | System creates only awarded review scope; shows non-awarded AED 120,000 proposal items as excluded, without conflating with optional 255,000. |
| **D.** Build project from approved award | Project, analytic account, WBS P0–P7, schedule and billing milestones created with links. |
| **E.** Allocate six named personnel | Import indicative rates/percent; flag Zahra at 120% if interpreted as capacity utilization. |
| **F.** Enter/approve sample weekly hours | Approved timesheets update actual costs and earned progress; planned vs actual visible. |
| **G.** Add external freelancer PO and office printer purchase | Freelancer project cost tracked; office printer classified overhead, not charged to project. |
| **H.** Submit variation for PBSD | Requires signed client approval before revenue/budget increases. |
| **I.** Invoice 25% NTP milestone | AED 31,250 net plus AED 1,562.50 VAT if taxable; remaining milestone billing visible. |
| **J.** Record partial receipt and overdue payment | Invoice status, aging and collected cash reconcile to accounting. |
| **K.** Complete technical certificate, run margin report | Report reconciles contract + variations − costs; technical vs financial close separate. |
| **L.** Re-open historic proposal / amend cost rate | History, prior invoice, past timesheet costs and original approved baseline remain recoverable. |

---

## 12. Delivery, Integration and Deployment Acceptance

Deliver a working configured demonstration database, seeded with the pilot SOL client, proposal and awarded scope; provide a reproducible Excel/CSV import template and data dictionary.

Supply user-role matrix, approval workflows, automation list, security restrictions, and descriptions of any Studio/custom code with ongoing support obligations.

Demonstrate general ledger and analytic ledger reconciliation; invoice and vendor payment audit trails; role-limited staff internal cost rates.

Agree access to existing EMS Excel trackers, PO/LOA registers, invoice register and any HR/payroll masters only after mapping data ownership and confidentiality.

Document Odoo edition/version, standard versus custom features, licensing, integrations, migration process, backups, testing strategy and commercial quotation.

**UAT pass criteria:** All 12 scripts above run end-to-end, no unapproved optional revenue, budget/cost changes traceable, and no double counting of vendor PO and bill.

---

## 13. Decisions Required from EMS Before Go-Live

1. Confirm actual RFP and proposal dates, pilot award number and whether the scanned PO is complete.
2. Confirm whether resource "engagement %" in existing Excel means dedicated weekly capacity, allocation to this project or a different measure.
3. Validate the person-level hourly figures: internal cost, billing charge-out or forecast planning allowances.
4. Confirm project calendar, working hours by office, overtime policy and whether the 6-week proposal programme or 10-week tracker is operative.
5. Confirm client legal entity, award terms, NTP, approved deliverable scope, exclusions and exact payment/approval trigger evidence.
6. Choose whether overhead and partner/NCK profit share are reported at project level or only in management accounts.
7. Agree project numbering, budget approval authorities, document naming and whether the first release will cover only review projects or all EMS services.

---

*Source basis: EMS revised 20 Aug 2025 proposal, signed one-page SOL PO extract, and EMS Project Proposal & Delivery Tracker.xlsx. All implementation behavior and sample controls are proposed requirements for Odoo to confirm, not assertions that these features are already configured.*