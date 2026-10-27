# ERP Evaluation Repository: Odoo vs ERPNext

This repository contains the analysis and evaluation artifacts for selecting an ERP system (Odoo vs ERPNext) for EMS (Engineering Management Services), centered on a pilot implementation for the **Sheikh Zayed Road Tower** project (Plot 3350144, Client: SOL Properties Development LLC).

## Repository Structure

```
project-management-erp-analysis/
├── analysis/                           # Evaluation analysis and decision-making documents
│   └── PROJECT_PLAN_Odoo_vs_ERPNext_Analysis.md
├── specifications/                     # Functional specifications and pilot data
│   ├── EMS_Odoo_ERP_Workflow_Functional_Specification.md
│   ├── EMS_Odoo_Pilot_Data_and_Import_Templates.md
│   └── EMS - Project Proposal & Delivery Tracker.md
├── AGENTS.md                          # Agent instructions and project context
├── opencode.json                        # OpenCode configuration
└── skills-lock.json                     # Locked skill versions
```

## Key Documents

### Analysis
- **Project Plan & Comparison**: [analysis/PROJECT_PLAN_Odoo_vs_ERPNext_Analysis.md](analysis/PROJECT_PLAN_Odoo_vs_ERPNext_Analysis.md) - Comprehensive evaluation of Odoo vs ERPNext, implementation roadmaps for both options, risk register, team structure, and success criteria

### Specifications
- **Odoo Functional Specification**: [specifications/EMS_Odoo_ERP_Workflow_Functional_Specification.md](specifications/EMS_Odoo_ERP_Workflow_Functional_Specification.md) - Detailed functional specification for Odoo implementation (workflow stages, data dictionary, UAT scripts, controls)
- **Odoo Pilot Data**: [specifications/EMS_Odoo_Pilot_Data_and_Import_Templates.md](specifications/EMS_Odoo_Pilot_Data_and_Import_Templates.md) - Pilot data: resource plans, timesheet templates, milestones, vendor costs, and 7 critical data issues
- **Source Tracker Data**: [specifications/EMS - Project Proposal & Delivery Tracker.md](specifications/EMS%20-%20Project%20Proposal%20%26%20Delivery%20Tracker.md) - Source tracker data (project info, proposal history, client agreement, team rates/engagement)

## Project Context

- **Pilot Project**: Sheikh Zayed Road Tower + Car Park (B+G+59+R), Plot 3350144
- **Client**: SOL Properties Development LLC
- **Award Value**: AED 125,000 ex VAT (review services only, not full AED 245,000 proposal)
- **Payment Milestones**: 25% NTP, 50% deliverables, 25% authority approval
- **Team**: 6 named resources with provisional rates/engagements (Zahra at 120% flagged)
- **Data Issues**: 7 critical conflicts (dates, rates, scope, engagement >100%, missing timesheets)

## Evaluation Status

**No decision has been made yet** between Odoo and ERPNext. This repository contains the artifacts to support that decision.

### Odoo Advantages (from analysis)
- Better project/service workflow fit
- Native CRM-to-project pipeline
- Studio for no-code customization
- Superior Arabic/RTL support
- Faster pilot delivery

### ERPNext Advantages (to be evaluated)
- Open source (no license costs)
- Python-based (similar tech stack)
- Strong community
- Built-in project management

## Critical Decisions Required (Blocking Evaluation Completion)

From the Project Plan:
- [ ] Actual RFP/proposal dates confirmation (tracker shows RFP 2026-08-01 after PO 2025-09-09)
- [ ] Engagement % definition (capacity vs allocation vs other measure)
- [ ] Hourly rate validation (internal cost vs billing vs planning)
- [ ] Project calendar (6 vs 10 weeks)
- [ ] Client legal entity, NTP, deliverable scope, exclusions
- [ ] Overhead/partner profit share reporting level
- [ ] Project numbering, budget authorities, document naming
- [ ] Phase 1 scope: review projects only vs all EMS services

## Next Steps

1. Complete ERPNext functional specification (parallel to Odoo spec)
2. Create side-by-side comparison matrix in `comparison/` directory (to be created)
3. Conduct Phase 0 decision workshop with stakeholders
4. Make final ERP selection decision
5. Proceed with implementation planning for chosen ERP

## Notes for Evaluators

- The `PROJECT_PLAN_Odoo_vs_ERPNext_Analysis.md` is the single source of truth for evaluation approach
- Pilot data has **7 critical issues** that must be resolved regardless of ERP choice
- Odoo **Enterprise license** would be ~$75k/yr for 25 users (if chosen)
- ERPNext would require more custom development but no license fees
- Both options would use similar tech stacks (Python, PostgreSQL)