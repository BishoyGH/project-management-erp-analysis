# AGENTS.md - Project Management ERP Analysis Repository

## Repository Overview

This repository contains the analysis and implementation planning for selecting and deploying an ERP system (Odoo vs ERPNext) for EMS (Engineering Management Services). The project centers on a pilot implementation for the **Sheikh Zayed Road Tower** project (Plot 3350144, Client: SOL Properties Development LLC).

## Key Files

| File | Purpose |
|------|---------|
| `PROJECT_PLAN_Odoo_vs_ERPNext_Analysis.md` | **Primary document** - Comprehensive evaluation of Odoo vs ERPNext, 22-week implementation roadmap, risk register, team structure, and success criteria |
| `EMS_Odoo_ERP_Workflow_Functional_Specification.md` | Detailed functional specification for Odoo implementation (workflow stages, data dictionary, UAT scripts, controls) |
| `EMS_Odoo_Pilot_Data_and_Import_Templates.md` | Pilot data: resource plans, timesheet templates, milestones, vendor costs, and 7 critical data issues |
| `EMS - Project Proposal & Delivery Tracker.md` | Source tracker data (project info, proposal history, client agreement, team rates/engagement) |
| `opencode.json` | OpenCode configuration with superpowers plugin and skill paths |
| `skills-lock.json` | Locked skill versions (erpnext, odoo-19, odoo-development, project-management, etc.) |

## Project Context

- **Pilot Project**: Sheikh Zayed Road Tower + Car Park (B+G+59+R), Plot 3350144
- **Client**: SOL Properties Development LLC
- **Award Value**: AED 125,000 ex VAT (review services only, not full AED 245,000 proposal)
- **Payment Milestones**: 25% NTP, 50% deliverables, 25% authority approval
- **Team**: 6 named resources with provisional rates/engagements (Zahra at 120% flagged)
- **Data Issues**: 7 critical conflicts (dates, rates, scope, engagement >100%, missing timesheets)

## Technology Decisions

- **Selected ERP**: **Odoo** (Enterprise recommended) - better project/service workflow fit, native CRM-to-project pipeline, Studio for no-code customization, superior Arabic/RTL, faster pilot delivery
- **Framework**: Odoo ORM (Python), OWL (JS), XML views, PostgreSQL
- **Custom Modules Planned**: `ems_project_chain`, `ems_resource`, `ems_timesheet`, `ems_budget`, `ems_vendor`, `ems_dashboard`
- **Deployment**: Odoo.sh or on-premise (dev/staging/prod)

## Critical Implementation Requirements (from Spec)

1. **Immutable Key Chain**: Client → Opportunity → Proposal Rev → Award → Project → Analytic Account
2. **Three Distinct Rates**: Internal Cost Rate / Client Billing Rate / Planning Rate (tracker rates are provisional)
3. **Approval Freeze**: Timesheet approval snapshots cost rate to preserve historical margin
4. **Vendor PO Default**: Must reference Project OR "Office Overhead" - never default to project
5. **Engagement %**: Planned hours ÷ available hours (40h/week default)
6. **Multi-Office**: Dubai, Cairo, Remote, Freelancer with currency per office
7. **Audit Trail**: All spec fields tracked with timestamp/user/revision
8. **No Double Counting**: Vendor PO commitment ≠ Vendor bill (separate tracking)

## Development Commands & Workflows

### Odoo Development (when implementation begins)
```bash
# Typical Odoo 17/18 development stack
# Backend: Python 3.10+, PostgreSQL 14+
# Frontend: OWL (JS), SCSS, QWeb templates
# Dev Tools: VS Code + Odoo extension, pgAdmin, Odoo.sh
# Testing: pytest + Odoo test runner (YAML/Python)
```

### Current Phase (Analysis/Planning)
No build/test commands yet - this is a planning repository. Implementation will follow the 6-phase roadmap in `PROJECT_PLAN_Odoo_vs_ERPNext_Analysis.md`.

## Key Decisions Required (Blocking Phase 0)

From `PROJECT_PLAN` Section 2.1 and `SPEC` Section 13:
- [ ] Actual RFP/proposal dates confirmation (tracker shows RFP 2026-08-01 after PO 2025-09-09)
- [ ] Engagement % definition (capacity vs allocation vs other measure)
- [ ] Hourly rate validation (internal cost vs billing vs planning)
- [ ] Project calendar (6 vs 10 weeks)
- [ ] Client legal entity, NTP, deliverable scope, exclusions
- [ ] Overhead/partner profit share reporting level
- [ ] Project numbering, budget authorities, document naming
- [ ] Phase 1 scope: review projects only vs all EMS services

## UAT Acceptance Criteria (12 Mandatory Scripts)

All must pass for go-live:
1. Lead → qualify → RFP → proposal R00 → R01 → win → PO
2. PO creates project + analytic account + baseline budget automatically
3. Resource plan → engagement % → timesheet → approval
4. Timesheet approval freezes cost rate → margin correct
5. Vendor PO for project → 3-way match → bill → payment
6. Milestone 1 eligible → invoice → pay → collection
7. Milestone 2 eligible → invoice → pay → collection
8. Milestone 3 eligible → invoice → pay → collection
9. Variation → approved → budget updated → revenue recognized
10. Profitability dashboard: Revenue - Labor - Vendor = Margin
11. Audit log shows: who changed rate, when, old/new value
12. No double-counting: vendor PO commitment ≠ vendor bill

## Risk Highlights

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Data quality issues delay pilot | High | High | Phase 0 workshop mandatory; sign-off before config |
| Engagement % definition unresolved | High | Medium | Workshop with HR/Finance; document decision |
| Rate validation (3 rate types) | High | High | HR/Finance sign-off on rate master before import |
| Scope creep beyond review projects | Medium | High | Phase 1 scope locked; Phase 2 for expansion |

## Repository Structure (Planned for Implementation)

```
ems_erp_implementation/
├── docs/
│   ├── specs/
│   ├── plans/
│   └── decisions/          # DECISION_LOG.md
├── odoo/
│   ├── custom_addons/      # ems_project_chain, ems_resource, etc.
│   ├── studio_exports/     # XML exports of Studio customizations
│   └── data/               # pilot_import_templates, demo_data
├── tests/
│   ├── unit/
│   ├── integration/
│   └── uat/                # test_scripts_1-12.py
├── deployment/
│   ├── odoo.sh/
│   ├── docker/
│   └── ansible/
└── README.md
```

## Notes for Future Agents

- This is a **planning/analysis repository** - no code yet, only specifications and data
- The `PROJECT_PLAN` document is the single source of truth for implementation approach
- All custom module code snippets in the plan are **proposed designs**, not implemented code
- Pilot data has **7 critical issues** that must be resolved in Phase 0 before any configuration
- Odoo **Enterprise license** is recommended (~$75k/yr for 25 users) for Studio, Accounting, Field Service
- Use **Studio for 80% of customizations**; custom modules only for complex logic (immutable chain, rate snapshots, engagement %)
- Engage certified Odoo partner for implementation