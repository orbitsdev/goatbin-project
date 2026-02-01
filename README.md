# Halal GOAT Bin

**Geographically-Oriented Application and Traceability System**

A comprehensive traceability and halal certification management system for goat farming and meat distribution in the Philippines.

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

## Project Levels Overview

| Level | Name | Purpose | Output |
|-------|------|---------|--------|
| **Level 1** | High-Level Overview | Understand WHAT to build | Documents (Done) |
| **Level 2** | Detailed Design | Understand HOW to build in detail | Specs, wireframes, user stories |
| **Level 3** | Development | Actually BUILD the system | Working code |
| **Level 4** | Deployment | RELEASE and maintain | Live system |

## Level 1 - What We Completed

| Document | Purpose |
|----------|---------|
| [Stakeholders](STEP_01_STAKEHOLDERS.md) | WHO is involved |
| [Roles & Permissions](STEP_02_USER_ROLES_PERMISSIONS.md) | WHO can do WHAT |
| [Business Process Flow](STEP_03_BUSINESS_PROCESS_FLOW.md) | HOW it works |
| [Modules & Features](STEP_04_MODULES_FEATURES.md) | WHAT to build |
| [Database Design](STEP_05_DATABASE_DESIGN.md) | WHERE to store (overview) |
| [Technical Architecture](STEP_06_TECHNICAL_ARCHITECTURE.md) | HOW to build (overview) |

**Depth:** Overview - enough to understand the project

## Level 2 - What Comes Next

| Document | Purpose |
|----------|---------|
| Detailed Database Schema | Exact fields, data types, indexes, constraints |
| API Specification (Swagger) | Every endpoint with request/response examples |
| UI/UX Wireframes | Screen layouts, navigation flow |
| User Stories | "As a [user], I want to [action], so that [benefit]" |
| Acceptance Criteria | Checklist for each feature |
| Business Rules | Detailed validation rules |

**Depth:** Detailed - enough to START coding

## Level 3 - Development

| Activity | Output |
|----------|--------|
| Database migrations | SQL/Laravel migration files |
| API coding | Laravel controllers, services, models |
| Frontend coding | Nuxt pages, components |
| Mobile coding | Flutter screens, widgets |
| Testing | Unit tests, integration tests |

**Depth:** Actual code

## Level 4 - Deployment

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

| Layer | Technology |
|-------|------------|
| Frontend (Web) | Nuxt 3 (Vue 3) |
| Backend API | Laravel 12 |
| Mobile App | Flutter |
| Database | PostgreSQL 16+ |
| Authentication | Laravel Sanctum |
| Cache | Redis |

## Additional Documentation

| Document | Description |
|----------|-------------|
| [GIS Explanation](GIS_EXPLANATION_AND_USAGE.md) | Geographic Information System usage |
| [Blockchain Explanation](BLOCKCHAIN_EXPLANATION_AND_USAGE.md) | Blockchain integration details |
| [Form Terminology](ADDENDUM_FORM_TERMINOLOGY_CHANGES.md) | Standard terminology definitions |
| [Meeting Agenda](MEETING_AGENDA_CLARIFICATION.md) | Project meeting notes |

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
├── README.md                              # This file
├── STEP_01_STAKEHOLDERS.md               # Stakeholder documentation
├── STEP_02_USER_ROLES_PERMISSIONS.md     # Roles and permissions
├── STEP_03_BUSINESS_PROCESS_FLOW.md      # Business processes
├── STEP_04_MODULES_FEATURES.md           # Features specification
├── STEP_05_DATABASE_DESIGN.md            # Database design
├── STEP_06_TECHNICAL_ARCHITECTURE.md     # Technical architecture
├── GIS_EXPLANATION_AND_USAGE.md          # GIS documentation
├── BLOCKCHAIN_EXPLANATION_AND_USAGE.md   # Blockchain documentation
├── ADDENDUM_FORM_TERMINOLOGY_CHANGES.md  # Terminology guide
└── MEETING_AGENDA_CLARIFICATION.md       # Meeting notes
```

## License

*To be determined*

---

*This project is currently in the planning and documentation phase. Level 1 is complete and ready for clarification meeting before proceeding to Level 2 detailed design.*
