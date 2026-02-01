# 📋 HALAL GOAT BIN PROJECT - DOCUMENTATION

## PROJECT KICKOFF MEETING

**Project:** Halal GOAT Bin: A Geographically-Oriented Application and Traceability System  
**Date:** February 1, 2026  
**Document:** Step 1 - Stakeholder Identification  

---

# STEP 1: STAKEHOLDER IDENTIFICATION

## Overview

This document identifies all stakeholders (users/entities) who will interact with the Halal GOAT Bin System.

---

## 1.1 List of Stakeholders

| # | Stakeholder | Description | How They Use the System |
|---|-------------|-------------|-------------------------|
| 1 | **Goat Farmer / Farm Owner** | Owns and operates the halal goat farm | Inputs farm data, goat records, production data |
| 2 | **Farm Worker / Technician** | Works at the farm, handles daily operations | Records goat health, feeding, births, deaths |
| 3 | **Slaughterhouse Staff** | Processes goats for meat | Records slaughter data, generates QR codes |
| 4 | **Halal Certifying Body** | Verifies if farm is halal-compliant (e.g., NCMF) | Reviews farm data, approves certification |
| 5 | **LGU Personnel** | Local government monitors halal farms | Monitors farms, sanctions bogus farms |
| 6 | **Department of Agriculture (DA)** | Government agency for agriculture | Oversees industry, views reports |
| 7 | **Trader / Distributor** | Buys goats from farms, sells to markets | Tracks goat transit, verifies sources |
| 8 | **Consumer (Muslim Buyer)** | Buys goat meat (chevon) | Scans QR code to verify halal authenticity |
| 9 | **System Administrator** | Manages the system | User management, system maintenance |

---

## 1.2 Stakeholders by Platform Access

| Web Application Users | Mobile App Users |
|-----------------------|------------------|
| Goat Farmer | Consumer |
| Farm Worker | Goat Farmer (SMS) |
| Slaughterhouse Staff | |
| Halal Certifier | |
| LGU Personnel | |
| DA Personnel | |
| System Admin | |

---

## 1.3 Stakeholder Flow Diagram

```
PRODUCTION                PROCESSING              DISTRIBUTION           CONSUMPTION
    │                         │                        │                      │
    ▼                         ▼                        ▼                      ▼
┌────────┐              ┌────────────┐           ┌──────────┐           ┌──────────┐
│ FARMER │ ──goat──▶   │SLAUGHTERHOUSE│ ──meat──▶│ TRADER/  │ ──meat──▶│ CONSUMER │
│        │              │   STAFF     │           │ MARKET   │           │          │
└────────┘              └────────────┘           └──────────┘           └──────────┘
    │                         │                        │                      │
    │                         │                        │                      │
    ▼                         ▼                        ▼                      ▼
 Records                  Records                  Tracks               Scans QR
 farm data               slaughter data           transit              verifies halal


        ┌──────────────────────────────────────────────────┐
        │              OVERSIGHT / MONITORING              │
        ├──────────────────────────────────────────────────┤
        │  • Halal Certifier (NCMF)                        │
        │  • LGU Personnel                                 │
        │  • Department of Agriculture                     │
        │  • System Admin                                  │
        └──────────────────────────────────────────────────┘
```

---

## 1.4 Stakeholder Categories

### A. Primary Users (Direct System Users)
- Goat Farmer / Farm Owner
- Farm Worker / Technician
- Slaughterhouse Staff
- Consumer

### B. Regulatory / Oversight Users
- Halal Certifying Body (NCMF)
- LGU Personnel
- Department of Agriculture

### C. Business Users
- Trader / Distributor

### D. System Users
- System Administrator

---

## 1.5 Summary

| Total Stakeholders | Web Users | Mobile Users |
|--------------------|-----------|--------------|
| 9 | 7 | 2 |

---

## ✅ STEP 1 COMPLETE

**Next Step:** Step 2 - User Roles & Permissions

---

*Document Version: 1.0*  
*Last Updated: February 1, 2026*
