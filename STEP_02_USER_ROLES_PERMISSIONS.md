# 📋 HALAL GOAT BIN PROJECT - DOCUMENTATION

## PROJECT KICKOFF MEETING

**Project:** Halal GOAT Bin: A Geographically-Oriented Application and Traceability System  
**Date:** February 1, 2026  
**Document:** Step 2 - User Roles & Permissions  

---

# STEP 2: USER ROLES & PERMISSIONS

## Overview

This document defines all user roles, their hierarchy, platform access, and permissions within the Halal GOAT Bin System.

---

## 2.1 Confirmed Roles

These roles are **confirmed** and will be implemented in the system:

| # | Role | Level | Platform | Description |
|---|------|-------|----------|-------------|
| 1 | System Admin | Super | Web | Full system access, user management |
| 2 | Farm Owner | Head | Web + SMS | Owns and manages own farm |
| 3 | Farm Worker | Staff | Web | Works under Farm Owner |
| 4 | Slaughterhouse Head | Head | Web | Manages slaughterhouse operations |
| 5 | Slaughterhouse Staff | Staff | Web | Inputs slaughter data |
| 6 | Certifier Head (NCMF) | Head | Web | Approves/rejects farm certification |
| 7 | Certifier Staff | Staff | Web | Reviews farm data, recommends |
| 8 | LGU Head | Head | Web | Monitors farms, can flag/report |
| 9 | LGU Staff | Staff | Web | View only access |
| 10 | DA Head | Head | Web | Generates official industry reports |
| 11 | DA Staff | Staff | Web | View only access |
| 12 | Consumer | — | Mobile | Scans QR, verifies halal products |

**Total Confirmed Roles: 12**

---

## 2.2 Role Hierarchy Structure

```
┌─────────────────────────────────────────────────────────────┐
│                      SYSTEM ADMIN                           │
│                      (Super Admin)                          │
└─────────────────────────────────────────────────────────────┘
                            │
      ┌─────────────────────┼─────────────────────┐
      │                     │                     │
      ▼                     ▼                     ▼
┌───────────┐        ┌───────────┐        ┌───────────┐
│   FARM    │        │SLAUGHTER- │        │ CERTIFIER │
│   OWNER   │        │HOUSE HEAD │        │   HEAD    │
│  (Head)   │        │  (Head)   │        │  (Head)   │
└───────────┘        └───────────┘        └───────────┘
      │                     │                     │
      ▼                     ▼                     ▼
┌───────────┐        ┌───────────┐        ┌───────────┐
│   FARM    │        │SLAUGHTER- │        │ CERTIFIER │
│  WORKER   │        │HOUSE STAFF│        │   STAFF   │
│  (Staff)  │        │  (Staff)  │        │  (Staff)  │
└───────────┘        └───────────┘        └───────────┘

      ┌─────────────────────┼─────────────────────┐
      │                     │                     │
      ▼                     ▼                     ▼
┌───────────┐        ┌───────────┐        ┌───────────┐
│    LGU    │        │    DA     │        │ CONSUMER  │
│   HEAD    │        │   HEAD    │        │ (Mobile)  │
│  (Head)   │        │  (Head)   │        │           │
└───────────┘        └───────────┘        └───────────┘
      │                     │
      ▼                     ▼
┌───────────┐        ┌───────────┐
│    LGU    │        │    DA     │
│   STAFF   │        │   STAFF   │
│  (Staff)  │        │  (Staff)  │
└───────────┘        └───────────┘
```

---

## 2.3 Head vs Staff Permissions

| Action | Head | Staff |
|--------|------|-------|
| View data | ✅ | ✅ |
| Create/Input data | ✅ | ✅ |
| Edit data | ✅ | ⚠️ Own entries only |
| Delete data | ✅ | ❌ |
| Approve/Reject | ✅ | ❌ |
| Add/Remove staff | ✅ | ❌ |
| Generate reports | ✅ | ❌ |

---

## 2.4 System Modules

```
HALAL GOAT BIN SYSTEM
│
├── FARM MANAGEMENT MODULE
│   ├── Farm Profile
│   ├── Goat Records
│   ├── Health & Medical Records
│   ├── Feed & Nutrition
│   ├── Inflows (Products Entering Farm)
│   ├── Outflows (Products Leaving Farm)
│   └── Production & Forecasting
│
├── TRACEABILITY MODULE
│   ├── Slaughter Records
│   ├── QR Code Generation
│   ├── Transit Tracking
│   └── Product Verification
│
├── CERTIFICATION MODULE
│   ├── Certification Applications
│   ├── Certification Status
│   └── Certification History
│
├── HALAL COMPLIANCE MODULE
│   ├── Compliance Checklist
│   ├── Auto-Flags & Warnings
│   └── Compliance Reports
│
├── REPORTS & ANALYTICS MODULE
│   ├── Farm Reports
│   ├── Industry Reports
│   └── Dashboard
│
├── GIS / MAPPING MODULE
│   ├── Farm Locations
│   ├── Haram Facility Distance
│   └── Regional Map View
│
├── ADMIN MODULE
│   ├── User Management
│   ├── Role Management
│   └── System Settings
│
└── MOBILE APP
    ├── QR Code Scanner
    ├── Product Verification
    └── SMS Integration
```

---

## 2.5 Module Access Matrix

### Legend:
- ✅ = Full Access (Create, Read, Update, Delete)
- 👁️ = View Only (Read)
- ❌ = No Access

### Farm Management Module

| Feature | Farm Owner | Farm Worker | Slaughter Head | Slaughter Staff | Certifier Head | Certifier Staff | LGU Head | LGU Staff | DA Head | DA Staff | Admin |
|---------|------------|-------------|----------------|-----------------|----------------|-----------------|----------|-----------|---------|----------|-------|
| Farm Profile | ✅ | 👁️ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Goat Records | ✅ | ✅ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Health & Medical | ✅ | ✅ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Feed & Nutrition | ✅ | ✅ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Inflows | ✅ | ✅ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Outflows | ✅ | ✅ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Production & Forecast | ✅ | 👁️ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |

### Traceability Module

| Feature | Farm Owner | Farm Worker | Slaughter Head | Slaughter Staff | Certifier Head | Certifier Staff | LGU Head | LGU Staff | DA Head | DA Staff | Admin |
|---------|------------|-------------|----------------|-----------------|----------------|-----------------|----------|-----------|---------|----------|-------|
| Slaughter Records | 👁️ | ❌ | ✅ | ✅ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| QR Code Generation | ❌ | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Transit Tracking | 👁️ | ❌ | ✅ | ✅ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Product Verification | 👁️ | ❌ | 👁️ | 👁️ | ✅ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |

### Certification Module

| Feature | Farm Owner | Farm Worker | Slaughter Head | Slaughter Staff | Certifier Head | Certifier Staff | LGU Head | LGU Staff | DA Head | DA Staff | Admin |
|---------|------------|-------------|----------------|-----------------|----------------|-----------------|----------|-----------|---------|----------|-------|
| Apply for Certification | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Review Application | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Approve/Reject | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Certification Status | 👁️ | ❌ | ❌ | ❌ | ✅ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |

### Halal Compliance Module

| Feature | Farm Owner | Farm Worker | Slaughter Head | Slaughter Staff | Certifier Head | Certifier Staff | LGU Head | LGU Staff | DA Head | DA Staff | Admin |
|---------|------------|-------------|----------------|-----------------|----------------|-----------------|----------|-----------|---------|----------|-------|
| Compliance Checklist | 👁️ | 👁️ | ❌ | ❌ | ✅ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Auto-Flags & Warnings | 👁️ | 👁️ | ❌ | ❌ | ✅ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Compliance Reports | 👁️ | ❌ | ❌ | ❌ | ✅ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |

### Reports & Analytics Module

| Feature | Farm Owner | Farm Worker | Slaughter Head | Slaughter Staff | Certifier Head | Certifier Staff | LGU Head | LGU Staff | DA Head | DA Staff | Admin |
|---------|------------|-------------|----------------|-----------------|----------------|-----------------|----------|-----------|---------|----------|-------|
| Farm Reports | ✅ | 👁️ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ |
| Industry Reports | ❌ | ❌ | ❌ | ❌ | 👁️ | 👁️ | 👁️ | 👁️ | ✅ | 👁️ | ✅ |
| Dashboard | ✅ | 👁️ | ✅ | 👁️ | ✅ | 👁️ | ✅ | 👁️ | ✅ | 👁️ | ✅ |

### GIS / Mapping Module

| Feature | Farm Owner | Farm Worker | Slaughter Head | Slaughter Staff | Certifier Head | Certifier Staff | LGU Head | LGU Staff | DA Head | DA Staff | Admin |
|---------|------------|-------------|----------------|-----------------|----------------|-----------------|----------|-----------|---------|----------|-------|
| Farm Locations | 👁️ | ❌ | ❌ | ❌ | ✅ | 👁️ | ✅ | 👁️ | ✅ | 👁️ | ✅ |
| Haram Facility Distance | 👁️ | ❌ | ❌ | ❌ | ✅ | 👁️ | ✅ | 👁️ | ✅ | 👁️ | ✅ |
| Regional Map View | ❌ | ❌ | ❌ | ❌ | ✅ | 👁️ | ✅ | 👁️ | ✅ | 👁️ | ✅ |

### Admin Module

| Feature | Farm Owner | Farm Worker | Slaughter Head | Slaughter Staff | Certifier Head | Certifier Staff | LGU Head | LGU Staff | DA Head | DA Staff | Admin |
|---------|------------|-------------|----------------|-----------------|----------------|-----------------|----------|-----------|---------|----------|-------|
| User Management | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Role Management | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| System Settings | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |

### Mobile App (Consumer)

| Feature | Consumer |
|---------|----------|
| QR Code Scanner | ✅ |
| Product Verification | ✅ |
| Product Info Display | ✅ |

**Note:** Consumer has no account required — public access via mobile app.

---

## 2.6 Detailed Permissions per Role

### 1. SYSTEM ADMIN
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| All Modules | ✅ | ✅ | ✅ | ✅ | Full access to everything |

**Notes:**
- Can create/manage all users
- Can configure system settings
- Can backup/restore data
- Can view all farms and data

---

### 2. FARM OWNER (Head)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| Farm Profile | ✅ | ✅ | ✅ | ❌ | Own farm only |
| Goat Records | ✅ | ✅ | ✅ | ✅ | Own farm only |
| Health & Medical | ✅ | ✅ | ✅ | ✅ | Own farm only |
| Feed & Nutrition | ✅ | ✅ | ✅ | ✅ | Own farm only |
| Inflows/Outflows | ✅ | ✅ | ✅ | ✅ | Own farm only |
| Certification | ✅ | ✅ | ❌ | ❌ | Can apply only |
| Farm Reports | ✅ | ✅ | ❌ | ❌ | Own farm only |

**Notes:**
- Can add/remove Farm Workers
- Can submit farm for certification
- Cannot delete farm profile (request to admin)
- Access via Web + SMS

---

### 3. FARM WORKER (Staff)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| Farm Profile | ❌ | ✅ | ❌ | ❌ | View only |
| Goat Records | ✅ | ✅ | ✅ | ❌ | Assigned farm only |
| Health & Medical | ✅ | ✅ | ✅ | ❌ | Assigned farm only |
| Feed & Nutrition | ✅ | ✅ | ✅ | ❌ | Assigned farm only |
| Inflows/Outflows | ✅ | ✅ | ✅ | ❌ | Assigned farm only |

**Notes:**
- Assigned to a specific farm by Farm Owner
- Cannot delete any records
- Cannot view other farms
- Cannot apply for certification

---

### 4. SLAUGHTERHOUSE HEAD (Head)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| Slaughter Records | ✅ | ✅ | ✅ | ✅ | Own slaughterhouse |
| QR Code Generation | ✅ | ✅ | ❌ | ❌ | Auto-generated |
| Transit Tracking | ✅ | ✅ | ✅ | ✅ | — |

**Notes:**
- Can add/remove Slaughterhouse Staff
- Can approve/edit slaughter records
- QR codes are immutable once generated

---

### 5. SLAUGHTERHOUSE STAFF (Staff)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| Slaughter Records | ✅ | ✅ | ⚠️ | ❌ | Own entries only |
| QR Code Generation | ✅ | ✅ | ❌ | ❌ | Auto-generated |
| Transit Tracking | ✅ | ✅ | ⚠️ | ❌ | Own entries only |

**Notes:**
- Can only process goats from certified farms
- Can only edit own entries
- Cannot delete records

---

### 6. CERTIFIER HEAD (NCMF) (Head)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| Farm Data | ❌ | ✅ | ❌ | ❌ | View all farms |
| Certification | ✅ | ✅ | ✅ | ❌ | Approve/Reject |
| Compliance | ✅ | ✅ | ✅ | ❌ | Add remarks |
| GIS/Mapping | ❌ | ✅ | ❌ | ❌ | View all |

**Notes:**
- Can approve/reject/suspend farm certification
- Can add certification remarks/comments
- Can add/remove Certifier Staff

---

### 7. CERTIFIER STAFF (Staff)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| Farm Data | ❌ | ✅ | ❌ | ❌ | View all farms |
| Certification | ❌ | ✅ | ❌ | ❌ | View only |
| Compliance | ❌ | ✅ | ❌ | ❌ | View only |

**Notes:**
- Can review farm data
- Can recommend (but not approve)
- Cannot modify certification status

---

### 8. LGU HEAD (Head)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| Farm Data | ❌ | ✅ | ❌ | ❌ | Own jurisdiction only |
| Certification | ❌ | ✅ | ❌ | ❌ | View only |
| GIS/Mapping | ❌ | ✅ | ❌ | ❌ | Own jurisdiction |
| Reports | ❌ | ✅ | ❌ | ❌ | Own jurisdiction |

**Notes:**
- Can only see farms in their municipality
- Can flag/report suspicious farms
- Can add/remove LGU Staff

---

### 9. LGU STAFF (Staff)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| Farm Data | ❌ | ✅ | ❌ | ❌ | Own jurisdiction only |
| Certification | ❌ | ✅ | ❌ | ❌ | View only |

**Notes:**
- View-only access
- Cannot flag farms (escalate to LGU Head)

---

### 10. DA HEAD (Head)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| All Farm Data | ❌ | ✅ | ❌ | ❌ | Region 12 |
| Industry Reports | ✅ | ✅ | ❌ | ❌ | Can generate |
| GIS/Mapping | ❌ | ✅ | ❌ | ❌ | Region 12 |

**Notes:**
- View-only access to all farms (Region 12)
- Can generate and export industry reports
- Dashboard overview of entire halal goat industry

---

### 11. DA STAFF (Staff)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| All Farm Data | ❌ | ✅ | ❌ | ❌ | Region 12 |
| Industry Reports | ❌ | ✅ | ❌ | ❌ | View only |

**Notes:**
- View-only access
- Cannot generate reports (view only)

---

### 12. CONSUMER (Mobile App)
| Module | Create | Read | Update | Delete | Special |
|--------|--------|------|--------|--------|---------|
| QR Scanner | ❌ | ✅ | ❌ | ❌ | Public |
| Product Info | ❌ | ✅ | ❌ | ❌ | Public |

**Notes:**
- Mobile app only
- No account required (public access)
- Can only scan QR and view product details

---

## 2.7 Possible Future Roles

These roles **may be needed** once we fully understand the existing process:

| # | Role | Why Possibly Needed | Decision |
|---|------|---------------------|----------|
| 1 | Transporter | Track goat movement farm → slaughterhouse | 🔄 TBD |
| 2 | Halal Slaughterer (Imam) | Record who performed halal slaughter | 🔄 TBD |
| 3 | Veterinarian | Official health certification | 🔄 TBD |
| 4 | Trader | Buys/sells goats between entities | 🔄 TBD |
| 5 | Meat Processor | Processes carcass into cuts/products | 🔄 TBD |
| 6 | Retailer / Vendor | Sells meat at market | 🔄 TBD |
| 7 | Cooperative Head | Manages group of farms | 🔄 TBD |
| 8 | Meat Inspector | Government quality inspection | 🔄 TBD |
| 9 | Auditor | External verification | 🔄 TBD |

**Note:** These roles will be evaluated in Step 3 (Business Flow Mapping).

---

## 2.8 Summary

| Category | Count |
|----------|-------|
| **Confirmed Roles** | 12 |
| **Possible Future Roles** | 9 |
| **Total Modules** | 7 |
| **Web Users** | 11 |
| **Mobile Users** | 1 (Consumer) |

---

## ✅ STEP 2 COMPLETE

**Next Step:** Step 3 - Business Process Flow Mapping

---

*Document Version: 1.0*  
*Last Updated: February 1, 2026*
