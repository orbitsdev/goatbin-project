# Halal GOAT Bin

**Geographically-Oriented Application and Traceability System**

A comprehensive traceability and halal certification management system for goat farming and meat distribution in the Philippines.

---

## Project Status

```
        LEVEL 1              LEVEL 2              LEVEL 3              LEVEL 4
      (Overview)            (Detail)            (Build)             (Release)
          |                    |                   |                    |
          v                    v                   v                    v
    +----------+        +----------+        +----------+        +----------+
    |          |        |          |        |          |        |          |
    |   PLAN   |------->|  DESIGN  |------->|   CODE   |------->|  DEPLOY  |
    |          |        |          |        |          |        |          |
    +----------+        +----------+        +----------+        +----------+
          |                    |                   |                    |
          v                    v                   v                    v
     Documents            Wireframes            Working              Live
     (10 docs)            + Specs               Code                System

   [COMPLETE]             NEXT                 LATER               LATER
```

**Current Phase:** Level 1 - High-Level Overview (Complete)
**Date:** February 1, 2026
**Next Step:** Clarification meeting, then Level 2 (Detailed Design)

---

## Documentation Guide

### Core Documents (Read in Order)

| # | Document | Purpose |
|---|----------|---------|
| 1 | [STEP_01_STAKEHOLDERS.md](STEP_01_STAKEHOLDERS.md) | WHO is involved |
| 2 | [STEP_02_USER_ROLES_PERMISSIONS.md](STEP_02_USER_ROLES_PERMISSIONS.md) | WHO can do WHAT |
| 3 | [STEP_03_BUSINESS_PROCESS_FLOW.md](STEP_03_BUSINESS_PROCESS_FLOW.md) | HOW it works |
| 4 | [STEP_04_MODULES_FEATURES.md](STEP_04_MODULES_FEATURES.md) | WHAT to build |
| 5 | [STEP_05_DATABASE_DESIGN.md](STEP_05_DATABASE_DESIGN.md) | WHERE to store data (overview) |
| 6 | [STEP_06_TECHNICAL_ARCHITECTURE.md](STEP_06_TECHNICAL_ARCHITECTURE.md) | HOW to build it (overview) |

### Updates & Action Items

| # | Document | Purpose |
|---|----------|---------|
| 7 | [ADDENDUM_FORM_TERMINOLOGY_CHANGES.md](ADDENDUM_FORM_TERMINOLOGY_CHANGES.md) | Changes based on existing goat farm forms |
| 8 | [MEETING_AGENDA_CLARIFICATION.md](MEETING_AGENDA_CLARIFICATION.md) | Questions that need team discussion |

### Reference / Educational (Optional Reading)

| # | Document | Purpose |
|---|----------|---------|
| 9 | [GIS_EXPLANATION_AND_USAGE.md](GIS_EXPLANATION_AND_USAGE.md) | What is GIS and how we use it |
| 10 | [BLOCKCHAIN_EXPLANATION_AND_USAGE.md](BLOCKCHAIN_EXPLANATION_AND_USAGE.md) | What is blockchain and how we use it |

### Reference Forms (Images)

Existing goat farm forms used as reference for system design. Located in [`/reference`](reference/) folder.

| # | Image | Description |
|---|-------|-------------|
| 1 | [01_baseline_survey_personal_farm_info.jpg](reference/01_baseline_survey_personal_farm_info.jpg) | Baseline Survey - Personal & Farm Information |
| 2 | [02_stock_inventory_breeding.jpg](reference/02_stock_inventory_breeding.jpg) | Stock Information - Inventory & Breeding |
| 3 | [03_feeds_feeding_system.jpg](reference/03_feeds_feeding_system.jpg) | Feeds and Feeding System |
| 4 | [04_health_management_husbandry.jpg](reference/04_health_management_husbandry.jpg) | Health Management & Husbandry Practices |
| 5 | [05_housing_marketing_support.jpg](reference/05_housing_marketing_support.jpg) | Housing, Marketing & Support Services |
| 6 | [06_problems_checklist.jpg](reference/06_problems_checklist.jpg) | Problems Checklist & Marketing Issues |
| 7 | [07_form1_livestock_inventory.jpg](reference/07_form1_livestock_inventory.jpg) | Form 1 - Livestock Inventory Record |
| 8 | [08_form2_production_reproduction.jpg](reference/08_form2_production_reproduction.jpg) | Form 2 - Production & Reproduction Record |
| 9 | [09_form3_disease_parasite_control.jpg](reference/09_form3_disease_parasite_control.jpg) | Form 3 - Disease & Parasite Control |
| 10 | [10_financial_report_sales.jpg](reference/10_financial_report_sales.jpg) | Financial Report - Cash Inflow/Sales |

---

## Project Levels

| Level | Name | Purpose | Output | Status |
|-------|------|---------|--------|--------|
| **1** | High-Level Overview | Understand WHAT to build | Documents | **Complete** |
| **2** | Detailed Design | Understand HOW to build in detail | Specs, wireframes, user stories | Next |
| **3** | Development | Actually BUILD the system | Working code | Later |
| **4** | Deployment | RELEASE and maintain | Live system | Later |

### Level 1 - What We Completed

- Clear understanding of the project
- All stakeholders identified
- Roles and permissions defined
- Features listed
- Database structure (overview)
- Technical architecture decided

**Depth:** Overview - enough to understand the project

### Level 2 - What Comes Next

| Document | Purpose |
|----------|---------|
| Detailed Database Schema | Exact fields, data types, indexes, constraints |
| API Specification (Swagger) | Every endpoint with request/response examples |
| UI/UX Wireframes | Screen layouts, navigation flow |
| User Stories | "As a [user], I want to [action], so that [benefit]" |
| Acceptance Criteria | Checklist for each feature |
| Business Rules | Detailed validation rules |

**Depth:** Detailed - enough to START coding

### Level 3 - Development

| Activity | Output |
|----------|--------|
| Database migrations | SQL/Laravel migration files |
| API coding | Laravel controllers, services, models |
| Frontend coding | Nuxt pages, components |
| Mobile coding | Flutter screens, widgets |
| Testing | Unit tests, integration tests |

**Depth:** Actual code

### Level 4 - Deployment

| Activity | Output |
|----------|--------|
| Server setup | Configured servers |
| CI/CD pipeline | Automated deployment |
| Documentation | User manual, admin guide |
| Training | Trained users |
| Monitoring | System health checks |

**Depth:** Live system

---

## Overview

Halal GOAT Bin is a multi-platform system designed to:

- Track goats from farm to consumer
- Manage halal certification and compliance
- Provide GIS-based mapping of farms and facilities
- Enable QR code-based product verification
- Support multiple stakeholders in the halal meat supply chain

## Technology Stack

| Layer | Technology | Version |
|-------|------------|---------|
| Frontend (Web) | Nuxt 3 (Vue 3) | Latest |
| Backend API | Laravel | 12 |
| Mobile App | Flutter | Latest |
| Database | PostgreSQL | 16+ |
| Authentication | Laravel Sanctum | Latest |
| Cache | Redis | Latest |
| Blockchain | TBD | - |
| GIS/Maps | TBD | - |
| SMS Gateway | TBD | - |

## Key Stakeholders

- Farm Owners & Workers
- Slaughterhouse Staff
- Halal Certifiers (NCMF)
- LGU Personnel
- Department of Agriculture
- Traders & Distributors
- Consumers

## Project Structure

```
goatbin-project/
│
├── CORE DOCUMENTATION
│   ├── STEP_01_STAKEHOLDERS.md
│   ├── STEP_02_USER_ROLES_PERMISSIONS.md
│   ├── STEP_03_BUSINESS_PROCESS_FLOW.md
│   ├── STEP_04_MODULES_FEATURES.md
│   ├── STEP_05_DATABASE_DESIGN.md
│   └── STEP_06_TECHNICAL_ARCHITECTURE.md
│
├── UPDATES & ACTION ITEMS
│   ├── ADDENDUM_FORM_TERMINOLOGY_CHANGES.md
│   └── MEETING_AGENDA_CLARIFICATION.md
│
├── REFERENCE / EDUCATIONAL
│   ├── GIS_EXPLANATION_AND_USAGE.md
│   └── BLOCKCHAIN_EXPLANATION_AND_USAGE.md
│
├── reference/                          <- Reference form images
│   ├── 01_baseline_survey_personal_farm_info.jpg
│   ├── 02_stock_inventory_breeding.jpg
│   ├── 03_feeds_feeding_system.jpg
│   ├── 04_health_management_husbandry.jpg
│   ├── 05_housing_marketing_support.jpg
│   ├── 06_problems_checklist.jpg
│   ├── 07_form1_livestock_inventory.jpg
│   ├── 08_form2_production_reproduction.jpg
│   ├── 09_form3_disease_parasite_control.jpg
│   └── 10_financial_report_sales.jpg
│
└── README.md
```

## License

*To be determined*

---

**Status:** Level 1 Complete
**Next:** Clarification meeting, then Level 2 (Detailed Design)
