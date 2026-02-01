# 📋 HALAL GOAT BIN PROJECT - DOCUMENTATION

## PROJECT KICKOFF MEETING

**Project:** Halal GOAT Bin: A Geographically-Oriented Application and Traceability System  
**Date:** February 1, 2026  
**Document:** Step 3 - Business Process Flow Mapping  
**Status:** DRAFT (Contains TBD items pending clarification meeting)

---

# STEP 3: BUSINESS PROCESS FLOW MAPPING

## Overview

This document maps the real-world business process — the complete journey of a goat from farm to consumer.

---

## 3.1 Overall Process Flow (High-Level)

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  STAGE 1 │───▶│  STAGE 2 │───▶│  STAGE 3 │───▶│  STAGE 4 │───▶│  STAGE 5 │
│   FARM   │    │TRANSPORT │    │SLAUGHTER │    │  MARKET  │    │ CONSUMER │
│          │    │          │    │          │    │          │    │          │
│    ✅    │    │   🔄     │    │    ✅    │    │    🔄    │    │    ✅    │
│Confirmed │    │   TBD    │    │Confirmed │    │   TBD    │    │Confirmed │
└──────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘
```

**Legend:**
- ✅ Confirmed — Process is clear
- 🔄 TBD — Needs clarification in meeting

---

## 3.2 STAGE 1: FARM (Production) ✅ CONFIRMED

### What Happens at This Stage:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           STAGE 1: FARM                                 │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  1.1 Farm Registration                                                  │
│      └── Farm Owner registers farm in the system                        │
│      └── Inputs: farm name, location, size, owner details               │
│      └── System: auto-calculates distance from haram facilities (GIS)   │
│                                                                         │
│  1.2 Goat Registration                                                  │
│      └── Farm Owner/Worker registers each goat                          │
│      └── Inputs: breed, gender, birth date, source (born or purchased)  │
│      └── System: generates unique Goat ID                               │
│                                                                         │
│  1.3 Daily Operations                                                   │
│      └── Farm Worker records:                                           │
│          • Feeding (feed type, quantity, supplier)                      │
│          • Health checks (illness, treatment, medicine)                 │
│          • Births (new kids born)                                       │
│          • Deaths (record cause)                                        │
│          • Inflows (new goats purchased, feed delivered)                │
│          • Outflows (goats sold, sent for slaughter)                    │
│                                                                         │
│  1.4 Halal Compliance Monitoring                                        │
│      └── System auto-checks:                                            │
│          • Feed ingredients (halal or haram?)                           │
│          • Medicine used (halal-certified?)                             │
│          • Distance from haram facilities                               │
│          • Goat health status                                           │
│      └── System: flags warnings if non-compliant                        │
│                                                                         │
│  1.5 Certification Application                                          │
│      └── Farm Owner applies for halal certification                     │
│      └── System: submits farm data to Certifier                         │
│      └── Certifier Staff: reviews farm data                             │
│      └── Certifier Head: approves or rejects                            │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Who is Involved:
| Role | Responsibility |
|------|----------------|
| Farm Owner | Registers farm, registers goats, applies for certification |
| Farm Worker | Records daily operations (feeding, health, births, deaths) |
| Certifier Staff | Reviews farm data for certification |
| Certifier Head | Approves/rejects certification |

### Data Captured:
| Data Type | Fields |
|-----------|--------|
| Farm Profile | Farm name, owner, location, size, distance from haram facilities |
| Goat Records | Goat ID, breed, gender, birth date, source |
| Feed Records | Feed type, brand, supplier, ingredients |
| Health Records | Illness, treatment, medicine, vaccination |
| Inflows | Products/goats entering farm, source |
| Outflows | Goats leaving farm, destination |
| Certification | Application date, status, reviewer, approver |

### System Auto-Actions:
| Trigger | Action |
|---------|--------|
| Farm registered | Calculate distance from haram facilities (GIS) |
| Goat registered | Generate unique Goat ID |
| Non-halal feed recorded | Flag warning ⚠️ |
| Non-halal medicine recorded | Flag warning ⚠️ |
| Farm near haram facility | Flag warning ⚠️ |
| Certification approved | Update farm status to "Certified" |

---

## 3.3 STAGE 2: TRANSPORT (Movement) 🔄 TBD

### What Happens at This Stage:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         STAGE 2: TRANSPORT                              │
│                            🔄 TBD                                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  2.1 Outflow Request                                                    │
│      └── Farm Owner creates outflow record                              │
│      └── Selects goats to be transported                                │
│      └── Inputs: destination (slaughterhouse), date, quantity           │
│                                                                         │
│  2.2 Transit Recording                                                  │
│      └── 🔄 TBD: Who records this?                                      │
│      └── Records: transport date, vehicle, destination                  │
│      └── System: links goats to destination slaughterhouse              │
│      └── System: updates goat status to "In Transit"                    │
│                                                                         │
│  2.3 Arrival Confirmation                                               │
│      └── 🔄 TBD: Who confirms this?                                     │
│      └── System: updates goat status to "At Slaughterhouse"             │
│      └── System: verifies goat came from certified farm                 │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### TBD Questions for Meeting:
| # | Question | Options |
|---|----------|---------|
| 1 | Who is responsible for transport? | Farm Owner / Slaughterhouse / Separate Transporter |
| 2 | Should Transporter have system login? | Yes (new role) / No (just record info) |
| 3 | Who confirms arrival at slaughterhouse? | Farm Owner / Slaughterhouse / Both |
| 4 | What data to record during transport? | Date, vehicle, driver / Just date and destination |

### Assumed Data Captured (Pending Confirmation):
| Data Type | Fields |
|-----------|--------|
| Transport Record | Date, goats transported, source farm, destination, vehicle (TBD) |
| Arrival Confirmation | Date, confirmed by, goat count |

---

## 3.4 STAGE 3: SLAUGHTER (Processing) ✅ CONFIRMED

### What Happens at This Stage:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         STAGE 3: SLAUGHTER                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  3.1 Pre-Slaughter Verification                                         │
│      └── Slaughterhouse Staff verifies:                                 │
│          • Goat is from certified halal farm                            │
│          • Goat health status is OK                                     │
│          • Goat ID matches records                                      │
│      └── System: auto-checks certification status                       │
│      └── System: BLOCKS if farm not certified                           │
│                                                                         │
│  3.2 Slaughter Recording                                                │
│      └── Slaughterhouse Staff records:                                  │
│          • Date & time of slaughter                                     │
│          • Goat ID                                                      │
│          • Live weight                                                  │
│          • Slaughterer name (who performed halal slaughter) ✅          │
│      └── System: updates goat status to "Slaughtered"                   │
│                                                                         │
│  3.3 Post-Slaughter Recording                                           │
│      └── Slaughterhouse Staff records:                                  │
│          • Carcass weight                                               │
│          • Offal weight                                                 │
│          • Meat cuts (if processed)                                     │
│                                                                         │
│  3.4 QR Code Generation                                                 │
│      └── System AUTO-GENERATES QR code containing:                      │
│          • Product ID                                                   │
│          • Source farm (name, location, certification)                  │
│          • Goat info (breed, gender, age)                               │
│          • Slaughter info (date, weight, slaughterer)                   │
│          • Halal certification status                                   │
│      └── QR code is attached to meat product                            │
│      └── Data is recorded on BLOCKCHAIN (immutable)                     │
│                                                                         │
│  3.5 Approval (if required)                                             │
│      └── Slaughterhouse Head reviews and approves records               │
│      └── System: finalizes records                                      │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Who is Involved:
| Role | Responsibility |
|------|----------------|
| Slaughterhouse Staff | Verifies goat, records slaughter data, generates QR |
| Slaughterhouse Head | Approves records (if required) |
| Halal Slaughterer | Performs actual slaughter (recorded as field) |

### Data Captured:
| Data Type | Fields |
|-----------|--------|
| Pre-Slaughter | Goat ID, farm certification status, health status |
| Slaughter Record | Date/time, goat ID, live weight, slaughterer name |
| Post-Slaughter | Carcass weight, offal weight, meat cuts |
| QR Code Data | Product ID, farm info, goat info, slaughter info, halal status |
| Blockchain | Immutable record of all slaughter data |

### System Auto-Actions:
| Trigger | Action |
|---------|--------|
| Goat from non-certified farm | BLOCK processing ❌ |
| Slaughter data complete | Generate QR code |
| QR code generated | Record on blockchain |
| Record approved by Head | Finalize and lock record |

---

## 3.5 STAGE 4: MARKET (Distribution) 🔄 TBD

### What Happens at This Stage:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          STAGE 4: MARKET                                │
│                            🔄 TBD                                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  4.1 Product Release                                                    │
│      └── Slaughterhouse releases meat with QR code                      │
│      └── Records: release date, quantity, destination                   │
│                                                                         │
│  4.2 Market/Supermarket Receives (🔄 TBD)                               │
│      └── 🔄 TBD: Does market have system login?                         │
│      └── 🔄 TBD: Or just terminal for verification?                     │
│                                                                         │
│  4.3 Product Display                                                    │
│      └── Meat displayed for sale with QR code visible                   │
│      └── Consumer can scan before purchasing                            │
│                                                                         │
│  Supermarkets mentioned in document:                                    │
│      • SM                                                               │
│      • KCC                                                              │
│      • Gaisano                                                          │
│      • Fit Mart (General Santos City)                                   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### TBD Questions for Meeting:
| # | Question | Options |
|---|----------|---------|
| 1 | What is the role of supermarket in system? | Terminal only / Full user role with login |
| 2 | Should supermarket staff have login accounts? | Yes / No |
| 3 | Do we track products after slaughterhouse? | Yes / No |
| 4 | Will MOA be signed with supermarkets? | Yes / No / Pilot only |
| 5 | Who provides terminal/equipment? | Project / Supermarket / Shared |

---

## 3.6 STAGE 5: CONSUMER (Verification) ✅ CONFIRMED

### What Happens at This Stage:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         STAGE 5: CONSUMER                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  5.1 QR Code Scan                                                       │
│      └── Consumer opens mobile app (Halal GOAT Bin)                     │
│      └── Scans QR code on meat product                                  │
│      └── No login required (public access)                              │
│                                                                         │
│  5.2 Product Verification                                               │
│      └── App displays:                                                  │
│          • Halal certification status ✅ or ❌                          │
│          • Source farm name & location                                  │
│          • Farm certification details                                   │
│          • Goat info (breed, gender, age)                               │
│          • Slaughter date                                               │
│          • Slaughterer name                                             │
│          • Slaughterhouse name                                          │
│      └── Consumer sees: "This product is HALAL VERIFIED" ✅             │
│                                                                         │
│  5.3 Trust & Purchase                                                   │
│      └── Consumer trusts the product                                    │
│      └── Makes purchase with confidence                                 │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Who is Involved:
| Role | Responsibility |
|------|----------------|
| Consumer | Scans QR code, views product info, verifies halal status |

### Data Displayed to Consumer:
| Category | Information Shown |
|----------|-------------------|
| Halal Status | "HALAL VERIFIED ✅" or "NOT VERIFIED ❌" |
| Farm Info | Farm name, location, certification status, certification date |
| Goat Info | Breed, gender, age |
| Slaughter Info | Date, slaughterhouse name, slaughterer name |
| Product Info | Product ID, weight |

---

## 3.7 CERTIFICATION PROCESS FLOW

### Flow Diagram:

```
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│  FARM OWNER │         │  CERTIFIER  │         │  CERTIFIER  │
│             │         │    STAFF    │         │    HEAD     │
└──────┬──────┘         └──────┬──────┘         └──────┬──────┘
       │                       │                       │
       │ 1. Apply for          │                       │
       │    certification      │                       │
       │──────────────────────▶│                       │
       │                       │                       │
       │                       │ 2. Review farm data   │
       │                       │    Check compliance   │
       │                       │──────────────────────▶│
       │                       │                       │
       │                       │    3. Recommend       │
       │                       │       approval        │
       │                       │──────────────────────▶│
       │                       │                       │
       │                       │                       │ 4. Approve
       │                       │                       │    or Reject
       │                       │                       │
       │◀──────────────────────────────────────────────│
       │         5. Notification of result             │
       │                                               │
```

### Certification Status Flow:

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│ NOT APPLIED │────▶│   PENDING   │────▶│UNDER REVIEW │────▶│  APPROVED   │
└─────────────┘     └─────────────┘     └─────────────┘     └──────┬──────┘
                                                │                  │
                                                │                  │
                                                ▼                  ▼
                                         ┌─────────────┐    ┌─────────────┐
                                         │  REJECTED   │    │  SUSPENDED  │
                                         └─────────────┘    └─────────────┘
```

### TBD Questions for Meeting:
| # | Question | Options |
|---|----------|---------|
| 1 | Who can apply for certification? | Farm only / Farm + Slaughterhouse |
| 2 | How long is certification valid? | 1 year / 2 years / Other |
| 3 | How to renew certification? | Re-apply / Auto-renew |
| 4 | What happens on violation? | Immediate suspend / Warning first |

---

## 3.8 COMPLETE FLOW DIAGRAM

```
                                    OVERSIGHT & MONITORING
                    ┌─────────────────────────────────────────────┐
                    │  CERTIFIER ←── Reviews & Certifies farms    │
                    │  LGU ←── Monitors farms in jurisdiction     │
                    │  DA ←── Views industry reports              │
                    │  ADMIN ←── Manages entire system            │
                    └─────────────────────────────────────────────┘
                                         │
                                         ▼
┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐
│   STAGE 1   │   │   STAGE 2   │   │   STAGE 3   │   │   STAGE 4   │   │   STAGE 5   │
│    FARM     │──▶│  TRANSPORT  │──▶│  SLAUGHTER  │──▶│   MARKET    │──▶│  CONSUMER   │
│     ✅      │   │     🔄      │   │     ✅      │   │     🔄      │   │     ✅      │
├─────────────┤   ├─────────────┤   ├─────────────┤   ├─────────────┤   ├─────────────┤
│             │   │             │   │             │   │             │   │             │
│ • Register  │   │ • Outflow   │   │ • Verify    │   │ • Release   │   │ • Scan QR   │
│   farm      │   │   record    │   │   goat      │   │   product   │   │             │
│ • Register  │   │ • Transit   │   │ • Record    │   │ • Display   │   │ • View      │
│   goats     │   │   tracking  │   │   slaughter │   │   for sale  │   │   info      │
│ • Daily     │   │ • Arrival   │   │ • Generate  │   │             │   │             │
│   records   │   │   confirm   │   │   QR code   │   │             │   │ • Verify    │
│ • Apply     │   │             │   │ • Blockchain│   │             │   │   halal     │
│   cert      │   │             │   │             │   │             │   │             │
│             │   │             │   │             │   │             │   │             │
├─────────────┤   ├─────────────┤   ├─────────────┤   ├─────────────┤   ├─────────────┤
│ Farm Owner  │   │ 🔄 TBD      │   │ Slaughter   │   │ 🔄 TBD      │   │ Consumer    │
│ Farm Worker │   │             │   │ Head/Staff  │   │             │   │ (Mobile)    │
└─────────────┘   └─────────────┘   └─────────────┘   └─────────────┘   └─────────────┘
```

---

## 3.9 Summary

### Confirmed Stages:
| Stage | Status | Key Process |
|-------|--------|-------------|
| Stage 1: Farm | ✅ Confirmed | Registration, daily operations, certification |
| Stage 3: Slaughter | ✅ Confirmed | Verification, slaughter recording, QR generation |
| Stage 5: Consumer | ✅ Confirmed | QR scanning, product verification |

### TBD Stages (Pending Meeting):
| Stage | Status | Questions to Clarify |
|-------|--------|----------------------|
| Stage 2: Transport | 🔄 TBD | Who handles? Separate role? |
| Stage 4: Market | 🔄 TBD | Terminal only or full role? MOA needed? |

### TBD Items Summary:
| # | Topic | Question |
|---|-------|----------|
| 1 | Transport | Who is responsible for transport? |
| 2 | Transport | Should Transporter have login? |
| 3 | Transport | Who confirms arrival? |
| 4 | Market | Terminal only or full user role? |
| 5 | Market | Should market staff have login? |
| 6 | Market | Do we track after slaughterhouse? |
| 7 | Certification | Who can apply? |
| 8 | Certification | How long is certification valid? |
| 9 | Certification | How to renew? |

---

## ✅ STEP 3 COMPLETE (DRAFT)

**Status:** Draft — Contains TBD items pending clarification meeting

**Next Steps:**
1. Conduct clarification meeting (see Meeting Agenda document)
2. Update this document with meeting outcomes
3. Proceed to Step 4: Modules & Features

---

*Document Version: 1.0 (DRAFT)*  
*Last Updated: February 1, 2026*  
*Status: Pending clarification meeting*
