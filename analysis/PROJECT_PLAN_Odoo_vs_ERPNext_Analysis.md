# Project Management ERP Analysis & Implementation Plan

## Overview

This document provides a comprehensive evaluation of **Odoo** vs **ERPNext** as the ERP platform of choice for EMS (Engineering Management Services), along with a complete implementation roadmap based on the pilot project data (Sheikh Zayed Road Tower, SOL Properties).

**Source Documents:**

- `EMS_Odoo_Pilot_Data_and_Import_Templates.md` - Pilot data, resource plans, timesheet templates, milestones, vendor costs, data issues
- `EMS - Project Proposal & Delivery Tracker.md` - Project proposal & delivery tracking
- `EMS_Odoo_ERP_Workflow_Functional_Specification.md` - Detailed functional specification for Odoo implementation

---

## Part 1: Odoo vs ERPNext - Comprehensive Evaluation

### 1.1 Executive Summary

| Criterion | Odoo | ERPNext | Winner |
|-----------|------|---------|--------|
| **Project/Service Industry Fit** | Excellent (Project, Timesheet, Field Service modules) | Good (Project, Timesheet, but weaker service workflows) | **Odoo** |
| **CRM-to-Project Pipeline** | Native, seamless (CRM → Sales → Project → Analytic) | Requires customization (Lead → Opportunity → Project) | **Odoo** |
| **Multi-Company/Multi-Currency** | Strong (built-in) | Strong (built-in) | Tie |
| **Developer Experience** | Good (Python/XML, Studio, OWL) | Good (Python/JS, Frappe Framework) | Tie |
| **Total Cost of Ownership** | Higher (Enterprise license + hosting) | Lower (Open source, self-hosted) | **ERPNext** |
| **Customization Flexibility** | Studio (no-code) + Custom modules | Custom apps + Server/Client scripts | Tie |
| **Arabic/RTL Support** | Excellent (native) | Good (community supported) | **Odoo** |
| **UAE VAT Compliance** | Native (Odoo 17+) | Native (ERPNext 14+) | Tie |
| **Community/Ecosystem** | Large (1500+ partners, 40k+ apps) | Growing (active community, fewer apps) | **Odoo** |
| **Implementation Speed (Pilot)** | Faster (pre-built project workflows) | Slower (more configuration needed) | **Odoo** |

**Recommendation: Odoo** - Better fit for engineering/services project workflow, native CRM-to-project pipeline, superior Arabic/RTL, faster pilot delivery.

---

### 1.2 Detailed Feature Comparison

#### Core Project Management Features

| Feature | Odoo (Project + Timesheets + Field Service) | ERPNext (Project + Timesheet) |
|---------|---------------------------------------------|-------------------------------|
| **WBS / Task Hierarchy** | Multi-level tasks, sub-tasks, milestones | Basic task tree, limited hierarchy |
| **Resource Planning** | Gantt, workload view, role-based planning | Basic resource allocation |
| **Timesheet Integration** | Native (Project × Employee × Task × Date) | Native (Timesheet doctype) |
| **Timesheet Approval Flow** | Multi-level (Team Lead → PM → Manager) | Basic submit/approve |
| **Billable vs Non-Billable** | Native per task/project | Native per timesheet |
| **Milestone Billing** | Sale Order → Invoice milestones | Sales Invoice → Payment Schedule |
| **Revenue Recognition** | Native (IFRS 15, percentage of completion) | Limited (manual journal entries) |
| **Project Profitability** | Real-time (Analytic accounting) | Project Profitability report |
| **Variation/Change Orders** | Native (Sale Order amendments) | Custom (Quotation → Sales Order) |
| **Document Management** | Attachments, versions, shared folders | Attachments, File manager |
| **Client Portal** | Native (Project, Invoice, Timesheet visibility) | Native (Customer Portal) |

#### CRM & Sales Pipeline

| Feature | Odoo | ERPNext |
|---------|------|---------|
| **Lead → Opportunity** | Native Kanban, stages, activities | Native Kanban, stages |
| **Proposal/Quotation Versioning** | Native (revisions, electronic signature) | Basic (version field) |
| **Proposal → Contract/PO** | One-click create SO/Contract | Manual conversion |
| **Contract Management** | Contracts app (recurring, amendments) | Basic (Sales Order) |
| **Pipeline Forecasting** | Weighted, expected revenue, probability | Weighted pipeline |
| **Lost Reason Tracking** | Native | Native |

#### Resource & HR Integration

| Feature | Odoo | ERPNext |
|---------|------|---------|
| **Employee Directory** | Native (HR app) | Native (HR module) |
| **Timesheet → Payroll** | Native integration | Native integration |
| **Leave/Attendance** | Native | Native |
| **Expense Claims** | Native (linked to project) | Native (linked to project) |
| **Multi-Office/Location** | Native (company/warehouse) | Native (company/territory) |
| **Freelancer/Contractor Support** | Vendor bills + analytic | Supplier + project allocation |

#### Financial & Accounting

| Feature | Odoo | ERPNext |
|---------|------|---------|
| **Analytic Accounting** | Native, multi-dimensional | Cost Centers + Projects |
| **Multi-Currency** | Native, daily rates, auto-revaluation | Native, manual/exchange rate tools |
| **VAT/GST (UAE)** | Native (Odoo 17+), FTA audit file | Native (ERPNext 14+), FTA audit file |
| **Invoice Milestones** | Native (Sale Order → Invoice plan) | Payment Schedule on Sales Invoice |
| **Vendor Bill Matching** | 3-way match (PO, Receipt, Bill) | 3-way match (PO, Receipt, Purchase Invoice) |
| **Cash Flow Forecasting** | Native | Basic |
| **Fixed Assets** | Native | Native |

#### Technical & Developer Experience

| Aspect | Odoo | ERPNext |
|--------|------|---------|
| **Framework** | Odoo ORM (Python), OWL (JS), XML views | Frappe Framework (Python), JS/React-like |
| **Customization - No Code** | **Studio** (drag-drop, very powerful) | **Customize Form**, Client/Server Scripts |
| **Customization - Code** | Custom modules (Python/XML) | Custom Apps (Python/JS) |
| **API** | REST (JSON/XML-RPC), GraphQL (community) | REST (Frappe), GraphQL |
| **Deployment** | Odoo.sh, On-premise, Docker, Kubernetes | Frappe Cloud, On-premise, Docker, Kubernetes |
| **Upgrades** | Major version migration needed | Major version migration needed |
| **Testing** | Odoo test framework (YAML/Python) | Frappe test framework (Python) |
| **Debugging** | Good (log, debug mode, shell) | Good (bench console, logs) |
| **Documentation** | Excellent (official + community) | Good (official + community) |
| **Learning Curve** | Moderate (ORM, XML, OWL) | Moderate (Frappe, DocTypes) |

---

### 1.3 Missing Features / Gaps Analysis

#### Odoo Gaps for EMS Requirements

| Requirement (from Spec) | Odoo Standard | Gap | Workaround |
|-------------------------|---------------|-----|------------|
| **Immutable key chain: Client → Opportunity → Proposal Rev → Award → Project → Analytic** | Partial | No enforced immutable chain | Custom module with constraints + audit log |
| **Vendor PO must reference Project or "Office Overhead" (never default to project)** | Partial | Default behavior attaches to project | Domain restriction + onchange validation |
| **Distinct INTERNAL COST RATE / CLIENT BILLING RATE / PLANNING RATE** | Partial | Only cost price & sale price on product/employee | Custom fields on hr.employee + project.task |
| **Approval freeze preserves cost-rate snapshot** | No | Timesheet uses current rate | Custom timesheet model with frozen rate field |
| **Engagement % = planned hours / available hours** | No | Only allocation % on project | Custom compute field on resource plan |
| **Multi-office (Dubai, Cairo, remote) with exchange rate policy** | Partial | Multi-company handles this | Multi-company setup per office |
| **Audit: who changed prices, rates, milestones, WBS baseline, task closure** | Partial (audit log) | Not granular enough for all fields | Auditlog module + custom tracked fields |
| **Revenue recognition per IFRS 15 (percentage of completion)** | Yes (Enterprise) | Only in Enterprise edition | Requires Enterprise license |

#### ERPNext Gaps for EMS Requirements

| Requirement (from Spec) | ERPNext Standard | Gap | Workaround |
|-------------------------|------------------|-----|------------|
| **CRM Opportunity → Proposal Revision → Signed Award → Project** | Partial | No native proposal revision control | Custom DocType for Proposal Version |
| **Immutable key chain enforcement** | No | No referential integrity enforcement | Custom validation hooks |
| **Vendor PO default to "Office Overhead" not Project** | No | Defaults to project if linked | Custom script to set default |
| **Three distinct rate types (Internal/Client/Planning)** | No | Only billing rate on Employee | Custom fields + client scripts |
| **Approval freeze with rate snapshot** | No | Timesheet uses current rate | Custom Timesheet with frozen rate |
| **Engagement % calculation** | No | Manual field | Custom compute |
| **Multi-office with currency per office** | Yes (Multi-company) | Complex setup | Multi-company per office |
| **Audit trail for all spec fields** | Partial (Versioning) | Not all fields tracked by default | Enable versioning on all custom fields |
| **Revenue recognition (IFRS 15)** | Limited | Manual process | Custom implementation |
| **Gantt/Workload view for resource planning** | Basic | No visual resource planning | Custom dashboard / external tool |

---

### 1.4 Developer Experience Comparison

#### Odoo Developer Experience

**Strengths:**

- **Studio**: Drag-drop UI builder for 80% of customizations without code
- **OWL Framework**: Modern reactive JS framework (Vue-like)
- **ORM**: Powerful, expressive, handles complexity well
- **XML Views**: Declarative UI definition, inheritance via XPath
- **Pre-built Modules**: 40,000+ apps on Odoo Apps store
- **Odoo.sh**: Integrated CI/CD, staging, production deployment
- **Documentation**: Comprehensive official docs + massive community

**Challenges:**

- **Version Upgrades**: Major versions (16→17→18) require code migration
- **Enterprise Lock-in**: Key features (Studio, Accounting, Helpdesk, Field Service) require Enterprise license
- **XML Verbosity**: Views can become large and complex
- **Performance**: Large databases need optimization (indexing, read_group)

**Typical Stack:**

```text
Backend:  Python 3.10+, PostgreSQL 14+
Frontend: OWL (JS), SCSS, QWeb templates
Dev Tools: VS Code + Odoo extension, pgAdmin, Odoo.sh
Testing:  pytest + Odoo test runner (YAML/Python)
```

#### ERPNext Developer Experience

**Strengths:**

- **Frappe Framework**: Full-stack, batteries-included (auth, permissions, desk, reports)
- **DocType-Driven**: Metadata-driven, less boilerplate
- **Client/Server Scripts**: Easy event-driven customization
- **100% Open Source**: No feature gating
- **Frappe Cloud**: Managed hosting with CI/CD
- **Bench CLI**: Excellent developer tooling (migrate, backup, restore, shell)
- **REST/GraphQL API**: First-class, auto-generated

**Challenges:**

- **Less Pre-built**: Fewer ready-made industry modules
- **JS Framework**: Custom (frappe.ui), not standard React/Vue
- **Report Builder**: Less mature than Odoo's
- **Community Apps**: Fewer than Odoo Apps store
- **Upgrade Path**: Can be complex with heavy customization

**Typical Stack:**

```text
Backend:  Python 3.10+, MariaDB 10.6+ / PostgreSQL 14+
Frontend: Frappe UI (custom), Vue.js (newer), SCSS
Dev Tools: VS Code + Frappe extension, bench CLI
Testing:  pytest + Frappe test utilities
```

---

### 1.5 Cost Analysis (3-Year TCO Estimate for EMS)

| Cost Component | Odoo (Enterprise) | ERPNext (Self-Hosted) | ERPNext (Frappe Cloud) |
|----------------|-------------------|----------------------|------------------------|
| **License (25 users)** | ~$75,000/yr ($30/user/mo) | $0 | Included |
| **Hosting (Production)** | $5,000-15,000/yr | $3,000-8,000/yr | $2,400-6,000/yr |
| **Implementation (Pilot)** | $50,000-80,000 | $60,000-100,000 | $60,000-100,000 |
| **Customization (Year 1)** | $30,000-50,000 | $40,000-70,000 | $40,000-70,000 |
| **Support/Maintenance (Yr 2-3)** | $40,000-60,000/yr | $20,000-40,000/yr | $30,000-50,000/yr |
| **Training/Change Mgmt** | $20,000-30,000 | $25,000-35,000 | $25,000-35,000 |
| **3-Year Total (Est.)** | **$350,000-500,000** | **$250,000-400,000** | **$280,000-430,000** |

*Note: Estimates vary significantly by region, partner rates, and scope.*

---

### 1.6 Final Recommendation: Odoo

**Why Odoo for EMS:**

1. **Project/Service Workflow Fit**: Native project → timesheet → invoicing → profitability flow matches EMS requirements exactly
2. **CRM-to-Project Pipeline**: Seamless opportunity → quotation → sales order → project → analytic account chain
3. **Studio**: Enables EMS to iterate on forms/workflows without developer dependency
4. **Arabic/RTL**: Native support critical for UAE operations
5. **UAE VAT**: Native FTA audit file generation
6. **Faster Pilot Delivery**: Pre-built workflows reduce configuration time
7. **Ecosystem**: Larger partner network in UAE/Middle East for support

**Risk Mitigation:**

- Budget for Enterprise license (~$75k/yr for 25 users)
- Plan for version upgrade every 2 years
- Use Studio for 80% customizations, custom modules only for complex logic
- Engage certified Odoo partner for implementation

---

## Part 2: Implementation Roadmap

### 2.1 Phase 0: Foundation & Preparation (Weeks 1-2)

| Task | Description | Owner | Deliverable |
|------|-------------|-------|-------------|
| 0.1 | **Data Reconciliation Workshop** - Resolve all 7 critical data issues from pilot tracker | EMS + Implementation Team | Signed-off data dictionary |
| 0.2 | **Odoo Edition Decision** - Confirm Enterprise vs Community + required apps | EMS Management | License purchase / subscription |
| 0.3 | **Environment Setup** - Odoo.sh or on-premise dev/staging/prod | DevOps | 3 environments ready |
| 0.4 | **Project Charter** - Scope, timeline, roles, communication plan | PM | Signed charter |
| 0.5 | **Gap Analysis Workshop** - Map each spec requirement to Odoo standard/custom | Functional Consultant | Gap analysis document |

**Key Decisions Required (from Spec Section 13):**

- [ ] Actual RFP/proposal dates confirmation
- [ ] Engagement % definition (capacity vs allocation)
- [ ] Hourly rate validation (internal cost vs billing vs planning)
- [ ] Project calendar (6 vs 10 weeks)
- [ ] Client legal entity, NTP, deliverable scope, exclusions
- [ ] Overhead/partner profit share reporting level
- [ ] Project numbering, budget authorities, document naming
- [ ] Phase 1 scope: review projects only vs all EMS services

---

### 2.2 Phase 1: Core Configuration - CRM, Sales, Project (Weeks 3-6)

| Task | Description | Odoo Components | Deliverable |
|------|-------------|-----------------|-------------|
| 1.1 | **CRM Pipeline Setup** - Stages: Lead → Qualified → RFP → Proposed → Negotiating → Won/Lost | `crm.lead`, `crm.stage`, activities | Configured pipeline with weighted forecasting |
| 1.2 | **Proposal Versioning** - Quotation revisions with electronic signature | `sale.order` (quotation), portal, sign | Revision-controlled proposals |
| 1.3 | **Sales Order → Project Auto-Create** - On SO confirm, create project + analytic account | `sale.order`, `project.project`, `account.analytic.account` | Automated project creation |
| 1.4 | **Immutable Key Chain Enforcement** - Client → Opportunity → Proposal Rev → SO → Project → Analytic | Custom module: `ems_project_chain` | Constraints + audit trail on all links |
| 1.5 | **Pilot Data Import** - SOL Client, Opportunity, Proposal R00/R01, PO, Project | Import templates from `EMS_Odoo_Pilot_Data_and_Import_Templates.md` | Seeded pilot data in dev |

**Custom Development (Task 1.4):**

```python
# ems_project_chain/models/project_chain.py
class ProjectChain(models.Model):
    _name = 'ems.project.chain'
    _description = 'Immutable Project Key Chain'
    
    client_id = fields.Many2one('res.partner', required=True, ondelete='restrict')
    opportunity_id = fields.Many2one('crm.lead', required=True, ondelete='restrict')
    proposal_revision_ids = fields.One2many('sale.order', 'ems_proposal_rev_id')
    signed_award_id = fields.Many2one('sale.order', domain=[('state','=','sale')], ondelete='restrict')
    project_id = fields.Many2one('project.project', required=True, ondelete='restrict')
    analytic_account_id = fields.Many2one('account.analytic.account', required=True, ondelete='restrict')
    
    _sql_constraints = [
        ('unique_chain', 'UNIQUE(client_id, opportunity_id, signed_award_id, project_id)', 
         'Project chain must be unique and immutable')
    ]
```

---

### 2.3 Phase 2: Resource Planning & Timesheets (Weeks 7-10)

| Task | Description | Odoo Components | Deliverable |
|------|-------------|-----------------|-------------|
| 2.1 | **Employee Rate Structure** - Three rate fields: Internal Cost, Client Billing, Planning | `hr.employee` + custom fields | Rate master data |
| 2.2 | **Resource Planning Model** - Weekly hours by employee per project, engagement % compute | Custom model `ems.resource.plan` | Planning board (Gantt/workload) |
| 2.3 | **Timesheet Enhancement** - Frozen cost rate snapshot on approval, WBS task link | `account.analytic.line` + custom fields | Compliant timesheet entry |
| 2.4 | **Timesheet Approval Flow** - Daily entry → Weekly PM approval → Lock | `hr.timesheet.sheet` + custom states | Approval workflow |
| 2.5 | **Multi-Office Support** - Dubai, Cairo, Remote, Freelancer with currency | `res.company` (multi-company) + `res.currency.rate` | Multi-office reporting |
| 2.6 | **Pilot Resource Import** - 6 employees from tracker with rates/engagements | Import template | Resource data loaded |

**Custom Development (Task 2.1, 2.2, 2.3):**

```python
# ems_resource/models/employee_rate.py
class HrEmployee(models.Model):
    _inherit = 'hr.employee'
    
    # Three distinct rates per spec
    internal_cost_rate = fields.Monetary('Internal Cost Rate (AED/h)', 
        currency_field='currency_id', groups='ems.group_project_manager')
    client_billing_rate = fields.Monetary('Client Billing Rate (AED/h)',
        currency_field='currency_id')
    planning_rate = fields.Monetary('Planning Rate (AED/h) - From Tracker',
        currency_field='currency_id', help='Provisional rate from Excel tracker')

# ems_resource/models/resource_plan.py
class EmsResourcePlan(models.Model):
    _name = 'ems.resource.plan'
    _description = 'Weekly Resource Plan by Employee per Project'
    
    employee_id = fields.Many2one('hr.employee', required=True)
    project_id = fields.Many2one('project.project', required=True)
    week_start = fields.Date(required=True)
    planned_hours = fields.Float('Planned Hours', required=True)
    engagement_pct = fields.Float('Engagement %', compute='_compute_engagement', store=True)
    # Engagement % = planned_hours / available_hours (40h default)

# ems_timesheet/models/analytic_line.py
class AccountAnalyticLine(models.Model):
    _inherit = 'account.analytic.line'
    
    frozen_cost_rate = fields.Monetary('Frozen Cost Rate (AED/h)', 
        currency_field='currency_id', readonly=True,
        help='Snapshot of internal_cost_rate at approval time')
    wbs_task_id = fields.Many2one('project.task', 'WBS Task', 
        domain="[('project_id', '=', project_id)]")
    
    def action_approve(self):
        # Snapshot rate before approval
        self.frozen_cost_rate = self.employee_id.internal_cost_rate
        super().action_approve()
```

---

### 2.4 Phase 3: Budget, Costing, Vendor Management (Weeks 11-14)

| Task | Description | Odoo Components | Deliverable |
|------|-------------|-----------------|-------------|
| 3.1 | **Project Budget Baseline** - Labor (from resource plan) + Vendor commitments | `project.budget` (Enterprise) or custom | Baseline budget per WBS |
| 3.2 | **Vendor Cost Management** - PO → Receipt → Bill 3-way match, Project/Office Overhead | `purchase.order`, `stock.picking`, `account.move` | Vendor workflow with project linkage |
| 3.3 | **Invoice Milestones** - 3 milestones (25%/50%/25%) with eligibility rules | `sale.order` → `account.move` (invoice plan) | Automated milestone invoicing |
| 3.4 | **VAT Handling** - 5% UAE VAT, separate liability, FTA audit file | `account.tax`, `account.tax.report` | Compliant VAT |
| 3.5 | **Profitability Dashboard** - Revenue vs Labor Cost vs Vendor Cost vs Margin | Analytic reports + custom dashboard | Real-time project P&L |
| 3.6 | **Pilot Vendor/Milestone Import** - Templates from spec | Import templates | Cost & revenue data loaded |

**Custom Development (Task 3.1, 3.2):**

```python
# ems_budget/models/project_budget.py
class ProjectBudget(models.Model):
    _name = 'ems.project.budget'
    _description = 'Project Budget Baseline (Labor + Vendor)'
    
    project_id = fields.Many2one('project.project', required=True)
    wbs_task_id = fields.Many2one('project.task', 'WBS Element')
    budget_labor_hours = fields.Float('Budgeted Labor Hours')
    budget_labor_cost = fields.Monetary('Budgeted Labor Cost (AED)')
    budget_vendor_cost = fields.Monetary('Budgeted Vendor Cost (AED)')
    budget_total = fields.Monetary('Total Budget', compute='_compute_total')
    # Version control for baseline vs revisions
    version = fields.Integer(default=1)
    is_baseline = fields.Boolean('Is Baseline Version')
    parent_id = fields.Many2one('ems.project.budget', 'Previous Version')

# ems_vendor/models/purchase_order.py
class PurchaseOrder(models.Model):
    _inherit = 'purchase.order'
    
    project_id = fields.Many2one('project.project', 'Project', 
        domain="[('analytic_account_id', '!=', False)]")
    cost_allocation = fields.Selection([
        ('project', 'Project'),
        ('office_overhead', 'Office Overhead')
    ], required=True, default='office_overhead')
    
    @api.onchange('project_id')
    def _onchange_project_id(self):
        if self.project_id:
            self.analytic_account_id = self.project_id.analytic_account_id
            self.cost_allocation = 'project'
        else:
            self.cost_allocation = 'office_overhead'
```

---

### 2.5 Phase 4: Dashboards, Reporting & Audit (Weeks 15-18)

| Task | Description | Odoo Components | Deliverable |
|------|-------------|-----------------|-------------|
| 4.1 | **CRM Funnel Dashboard** - Pipeline, conversion, proposal age | `crm.lead` + dashboard | Funnel dashboard |
| 4.2 | **Portfolio Dashboard** - Contracted revenue, stage, deliverables, payments | Custom dashboard + analytic | Portfolio view |
| 4.3 | **Resource Dashboard** - Planned vs actual, utilization, double-booking | `ems.resource.plan` + timesheets | Resource utilization |
| 4.4 | **Project Economics Dashboard** - Award vs variations, EAC, margin, AR aging | Analytic + custom | Project P&L |
| 4.5 | **Finance Dashboard** - Milestone eligibility, invoicing, collections, VAT | `account.move` + custom | Finance dashboard |
| 4.6 | **Audit Trail** - All spec fields tracked with timestamp/user/revision | `auditlog` module + tracked fields | Complete audit log |

**Custom Development (Task 4.6):**

```python
# Track all critical fields per spec Section 10
AUDIT_TRACKED_MODELS = {
    'sale.order': ['amount_total', 'amount_untaxed', 'order_line.price_unit'],
    'project.project': ['name', 'date_start', 'date', 'analytic_account_id'],
    'project.task': ['name', 'planned_hours', 'parent_id', 'stage_id', 'active'],
    'hr.employee': ['internal_cost_rate', 'client_billing_rate', 'planning_rate'],
    'account.analytic.line': ['unit_amount', 'frozen_cost_rate', 'wbs_task_id'],
    'account.move': ['invoice_line_ids.price_unit', 'invoice_date', 'payment_state'],
    'purchase.order': ['amount_total', 'project_id', 'cost_allocation'],
}
```

---

### 2.6 Phase 5: UAT, Training & Go-Live (Weeks 19-22)

| Task | Description | Deliverable |
|------|-------------|-------------|
| 5.1 | **UAT Script Execution** - All 12 mandatory demo scripts from Spec Section 11 | UAT sign-off |
| 5.2 | **User Training** - Role-based: PM, Accountant, Resource Manager, Leadership | Training materials + sessions |
| 5.3 | **Data Migration** - Historical projects, open POs, vendor data | Migrated data validated |
| 5.4 | **Parallel Run** - 2 weeks parallel with Excel trackers | Variance report |
| 5.5 | **Go-Live** - Cutover, hypercare support | Production live |
| 5.6 | **Documentation Handover** - User manuals, admin guide, custom code docs | Complete documentation |

**UAT Scripts (from Spec Section 11 - to be detailed):**

1. Create lead → qualify → RFP → proposal R00 → proposal R01 → win → PO
2. PO creates project + analytic account + baseline budget automatically
3. Resource plan entered → engagement % computed → timesheet entered → approved
4. Timesheet approval freezes cost rate → margin calculated correctly
5. Vendor PO created for project → 3-way match → bill → payment
6. Milestone 1 eligible → invoice issued → client pays → collection recorded
7. Milestone 2 eligible → invoice → pay → collection
8. Milestone 3 eligible → invoice → pay → collection
9. Variation requested → approved → budget updated → revenue recognized
10. Profitability dashboard shows: Revenue - Labor Cost - Vendor Cost = Margin
11. Audit log shows: who changed rate, when, old/new value
12. No double-counting: vendor PO commitment ≠ vendor bill (separate tracking)

---

### 2.7 Phase 6: Post Go-Live & Continuous Improvement (Months 6-12)

| Task | Description | Timeline |
|------|-------------|----------|
| 6.1 | **Hypercare Support** - Dedicated support for 4 weeks | Month 1-2 |
| 6.2 | **Performance Tuning** - Query optimization, indexing | Month 2-3 |
| 6.3 | **Advanced Reporting** - Custom reports per leadership requests | Month 3-6 |
| 6.4 | **Phase 2 Scope** - Expand to all EMS service lines (not just review) | Month 6-12 |
| 6.5 | **Integration** - HR/Payroll, Document Management, Email | Month 6-12 |

---

## Part 3: Risk Register

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Data quality issues (7 critical issues) delay pilot | High | High | Phase 0 workshop mandatory; sign-off before config |
| Engagement % definition not resolved | High | Medium | Workshop with HR/Finance; document decision |
| Rate validation (internal vs billing vs planning) | High | High | HR/Finance sign-off on rate master before import |
| Scope creep beyond review projects | Medium | High | Phase 1 scope locked; Phase 2 for expansion |
| Odoo version upgrade complexity | Medium | Medium | Stay on LTS (18.0); plan upgrade annually |
| Custom module maintenance burden | Medium | Medium | Maximize Studio; minimize custom code; document |
| User adoption resistance | Medium | High | Role-based training; champions; parallel run |
| Multi-company/currency complexity | Low | High | Start single-company; add Cairo/Remote later |

---

## Part 4: Team Structure & Roles

| Role | Responsibility | FTE (Peak) |
|------|----------------|------------|
| **Project Sponsor** | EMS Leadership, decisions, budget | 0.1 |
| **Project Manager** | Timeline, coordination, risk, communication | 1.0 |
| **Functional Consultant (Lead)** | Requirements, config, UAT, training | 1.0 |
| **Technical Consultant (Lead)** | Architecture, custom modules, integrations | 1.0 |
| **Odoo Developer(s)** | Custom modules, Studio, reports | 2.0 |
| **QA/Tester** | Test scripts, UAT support, automation | 0.5 |
| **DevOps** | Environments, CI/CD, backups, monitoring | 0.5 |
| **EMS Subject Matter Experts** | Business process validation, data, UAT | 2-3 (part-time) |
| **Change Manager** | Training, adoption, communication | 0.5 |

---

## Part 5: Success Criteria (KPIs)

| KPI | Target | Measurement |
|-----|--------|-------------|
| **Pilot Go-Live** | Week 22 | On-time delivery |
| **Data Accuracy** | 100% pilot data reconciled | Zero critical data issues |
| **User Adoption** | >90% active users at 30 days | Login analytics |
| **Timesheet Compliance** | >95% approved weekly | Approval rate |
| **Invoice Accuracy** | Zero milestone billing errors | Finance reconciliation |
| **Project Margin Visibility** | Real-time for all active projects | Dashboard availability |
| **Audit Trail Completeness** | 100% spec fields tracked | Audit log review |
| **UAT Pass Rate** | 12/12 scripts pass | UAT sign-off |

---

## Appendix: File Structure for Implementation

```text
ems_erp_implementation/
├── docs/
│   ├── specs/
│   │   └── 2025-08-27-ems-erp-functional-spec.md
│   ├── plans/
│   │   └── 2025-08-27-ems-erp-implementation-plan.md
│   └── decisions/
│       └── DECISION_LOG.md
├── odoo/
│   ├── custom_addons/
│   │   ├── ems_project_chain/
│   │   ├── ems_resource/
│   │   ├── ems_timesheet/
│   │   ├── ems_budget/
│   │   ├── ems_vendor/
│   │   └── ems_dashboard/
│   ├── studio_exports/
│   │   └── (XML exports of Studio customizations)
│   └── data/
│       ├── pilot_import_templates/
│       └── demo_data/
├── tests/
│   ├── unit/
│   ├── integration/
│   └── uat/
│       └── test_scripts_1-12.py
├── deployment/
│   ├── odoo.sh/
│   ├── docker/
│   └── ansible/
└── README.md
```

---

## Next Steps

1. **Review this plan** with EMS stakeholders
2. **Confirm Odoo edition** (Enterprise recommended) and license procurement
3. **Schedule Phase 0 workshop** for data reconciliation (Week 1)
4. **Assemble implementation team** (internal + partner)
5. **Kick off** with signed charter

---

*Document Version: 1.0*  
*Date: 2025-08-27*  
*Based on: EMS_Odoo_Pilot_Data_and_Import_Templates.md, EMS - Project Proposal & Delivery Tracker.md, EMS_Odoo_ERP_Workflow_Functional_Specification.md*