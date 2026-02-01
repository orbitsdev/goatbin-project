# 📋 HALAL GOAT BIN PROJECT - DOCUMENTATION

## PROJECT KICKOFF MEETING

**Project:** Halal GOAT Bin: A Geographically-Oriented Application and Traceability System  
**Date:** February 1, 2026  
**Document:** Step 5 - Database Design (High-Level)  
**Status:** OVERVIEW (Detailed design to follow in Level 2)

---

# STEP 5: DATABASE DESIGN (High-Level)

## Overview

This document provides a high-level overview of the database structure — entities, relationships, and possible fields. This is NOT the final detailed design; it serves as a foundation for deeper database design later.

---

## 5.1 Document Scope

| Level | Description | Status |
|-------|-------------|--------|
| **Level 1 (This Document)** | Entity list, simple ERD, possible fields | ✅ Overview |
| **Level 2 (Future)** | Complete fields, data types, constraints, indexes | 🔄 Later |
| **Level 3 (Development)** | Migration files, SQL scripts | 🔄 When coding |

---

## 5.2 Database Entities Overview

### Entity Categories

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         DATABASE ENTITIES                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   USER MANAGEMENT (3 tables)                                            │
│   ├── users                                                             │
│   ├── roles                                                             │
│   └── user_roles                                                        │
│                                                                         │
│   FARM MANAGEMENT (7 tables)                                            │
│   ├── farms                                                             │
│   ├── goats                                                             │
│   ├── health_records                                                    │
│   ├── vaccinations                                                      │
│   ├── feed_records                                                      │
│   ├── inflows                                                           │
│   └── outflows                                                          │
│                                                                         │
│   TRACEABILITY (4 tables)                                               │
│   ├── transports                                                        │
│   ├── slaughter_records                                                 │
│   ├── qr_codes                                                          │
│   └── blockchain_logs                                                   │
│                                                                         │
│   CERTIFICATION (3 tables)                                              │
│   ├── certification_applications                                        │
│   ├── certification_reviews                                             │
│   └── certifications                                                    │
│                                                                         │
│   COMPLIANCE (2 tables)                                                 │
│   ├── compliance_checks                                                 │
│   └── compliance_warnings                                               │
│                                                                         │
│   REFERENCE DATA (9 tables)                                             │
│   ├── breeds                                                            │
│   ├── feed_types                                                        │
│   ├── medicine_types                                                    │
│   ├── illness_types                                                     │
│   ├── provinces                                                         │
│   ├── municipalities                                                    │
│   ├── barangays                                                         │
│   ├── slaughterhouses                                                   │
│   └── haram_facilities                                                  │
│                                                                         │
│   SYSTEM (3 tables)                                                     │
│   ├── audit_logs                                                        │
│   ├── notifications                                                     │
│   └── settings                                                          │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

TOTAL: 31 Tables
```

### Entity Summary Table

| # | Category | Tables | Count |
|---|----------|--------|-------|
| 1 | User Management | users, roles, user_roles | 3 |
| 2 | Farm Management | farms, goats, health_records, vaccinations, feed_records, inflows, outflows | 7 |
| 3 | Traceability | transports, slaughter_records, qr_codes, blockchain_logs | 4 |
| 4 | Certification | certification_applications, certification_reviews, certifications | 3 |
| 5 | Compliance | compliance_checks, compliance_warnings | 2 |
| 6 | Reference Data | breeds, feed_types, medicine_types, illness_types, provinces, municipalities, barangays, slaughterhouses, haram_facilities | 9 |
| 7 | System | audit_logs, notifications, settings | 3 |
| | **TOTAL** | | **31** |

---

## 5.3 Entity Relationship Diagram (ERD)

### ERD - Main Entities (Simplified)

```
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│                                    ERD - MAIN FLOW                                      │
└─────────────────────────────────────────────────────────────────────────────────────────┘

                                         ┌──────────┐
                                         │  roles   │
                                         └────┬─────┘
                                              │ M:N
                                              │
┌──────────────────────────────────────────────────────────────────────────────────────┐
│                                         │                                            │
│  ┌──────────┐  1:M   ┌──────────┐      │      ┌───────────────────┐                 │
│  │  users   │───────▶│  farms   │◀─────┴─────▶│ certification_    │                 │
│  │          │        │          │             │ applications      │                 │
│  └──────────┘        └────┬─────┘             └─────────┬─────────┘                 │
│                           │                             │                            │
│                           │ 1:M                         │ 1:1                        │
│                           │                             ▼                            │
│                           │                    ┌───────────────────┐                 │
│                           │                    │  certifications   │                 │
│                           │                    └───────────────────┘                 │
│                           │                                                          │
│                           ▼                                                          │
│                      ┌──────────┐                                                    │
│                      │  goats   │                                                    │
│                      └────┬─────┘                                                    │
│                           │                                                          │
│         ┌─────────────────┼─────────────────┬─────────────────┐                     │
│         │ 1:M             │ 1:M             │ 1:M             │ 1:M                  │
│         ▼                 ▼                 ▼                 ▼                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                 │
│  │   health_   │  │vaccinations │  │  outflows   │  │  transports │                 │
│  │   records   │  │             │  │             │  │   (TBD)     │                 │
│  └─────────────┘  └─────────────┘  └──────┬──────┘  └──────┬──────┘                 │
│                                           │                 │                        │
│                                           │ 1:1             │ 1:M                    │
│                                           ▼                 ▼                        │
│                                    ┌────────────────────────────┐                    │
│                                    │     slaughter_records      │                    │
│                                    └─────────────┬──────────────┘                    │
│                                                  │                                   │
│                                                  │ 1:1                               │
│                                                  ▼                                   │
│                                           ┌──────────┐                               │
│                                           │ qr_codes │                               │
│                                           └──────────┘                               │
│                                                                                      │
└──────────────────────────────────────────────────────────────────────────────────────┘
```

### ERD - Reference Data

```
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│                               ERD - REFERENCE DATA                                      │
└─────────────────────────────────────────────────────────────────────────────────────────┘

┌───────────────┐      ┌───────────────┐      ┌───────────────┐
│   provinces   │ 1:M  │ municipalities│ 1:M  │   barangays   │
│               │─────▶│               │─────▶│               │
└───────────────┘      └───────┬───────┘      └───────────────┘
                               │
                               │ Referenced by:
                               ▼
                ┌──────────────────────────────┐
                │  farms, slaughterhouses,     │
                │  haram_facilities            │
                └──────────────────────────────┘


┌───────────────┐      ┌───────────────┐      ┌───────────────┐
│    breeds     │      │  feed_types   │      │medicine_types │
└───────┬───────┘      └───────┬───────┘      └───────┬───────┘
        │                      │                      │
        │ Referenced by:       │ Referenced by:       │ Referenced by:
        ▼                      ▼                      ▼
   ┌─────────┐          ┌─────────────┐        ┌─────────────┐
   │  goats  │          │feed_records │        │health_records│
   └─────────┘          └─────────────┘        └─────────────┘


┌───────────────┐      ┌───────────────┐
│illness_types  │      │haram_facilities│
└───────┬───────┘      └───────┬───────┘
        │                      │
        │ Referenced by:       │ Used for:
        ▼                      ▼
   ┌─────────────┐      ┌─────────────────┐
   │health_records│     │ Distance calc   │
   └─────────────┘      │ for farms       │
                        └─────────────────┘
```

### ERD - User & Roles

```
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│                                 ERD - USER & ROLES                                      │
└─────────────────────────────────────────────────────────────────────────────────────────┘

┌───────────────┐           ┌───────────────┐           ┌───────────────┐
│    users      │    M:N    │  user_roles   │    M:1    │    roles      │
│               │◀─────────▶│               │◀─────────▶│               │
│ - id          │           │ - user_id     │           │ - id          │
│ - name        │           │ - role_id     │           │ - name        │
│ - email       │           │ - entity_type │           │ - level       │
│ - password    │           │ - entity_id   │           │               │
└───────────────┘           └───────────────┘           └───────────────┘
                                   │
                                   │ entity_type can be:
                                   │ - farm
                                   │ - slaughterhouse
                                   │ - lgu
                                   │ - da
                                   │ - certifier
                                   ▼
                    ┌──────────────────────────────┐
                    │  Links user to specific      │
                    │  farm, slaughterhouse, etc.  │
                    └──────────────────────────────┘
```

---

## 5.4 Table Definitions (Overview)

**Note:** These are POSSIBLE fields — not final. Detailed field definitions will be done in Level 2.

---

### USER MANAGEMENT TABLES

#### Table: users
| Field | Description |
|-------|-------------|
| id | Primary key |
| name | Full name |
| email | Email address (unique) |
| password | Hashed password |
| phone | Phone number |
| address | Address |
| photo | Profile photo path |
| status | active, inactive |
| email_verified_at | Email verification date |
| created_at | Record created |
| updated_at | Record updated |

#### Table: roles
| Field | Description |
|-------|-------------|
| id | Primary key |
| name | Role name (system name) |
| display_name | Display name |
| description | Role description |
| level | super, head, staff, public |
| created_at | Record created |
| updated_at | Record updated |

**Possible Roles:**
| Role Name | Display Name | Level |
|-----------|--------------|-------|
| admin | System Admin | super |
| farm_owner | Farm Owner | head |
| farm_worker | Farm Worker | staff |
| slaughterhouse_head | Slaughterhouse Head | head |
| slaughterhouse_staff | Slaughterhouse Staff | staff |
| certifier_head | Certifier Head | head |
| certifier_staff | Certifier Staff | staff |
| lgu_head | LGU Head | head |
| lgu_staff | LGU Staff | staff |
| da_head | DA Head | head |
| da_staff | DA Staff | staff |
| consumer | Consumer | public |

#### Table: user_roles
| Field | Description |
|-------|-------------|
| id | Primary key |
| user_id | Reference to users |
| role_id | Reference to roles |
| entity_type | farm, slaughterhouse, lgu, da, certifier |
| entity_id | ID of the related entity |
| created_at | Record created |

---

### FARM MANAGEMENT TABLES

#### Table: farms
| Field | Description |
|-------|-------------|
| id | Primary key |
| farm_code | Unique farm code (HGF-0001) |
| name | Farm name |
| owner_id | Reference to users |
| address | Farm address |
| barangay_id | Reference to barangays |
| municipality_id | Reference to municipalities |
| province_id | Reference to provinces |
| latitude | GPS latitude |
| longitude | GPS longitude |
| area_hectares | Farm area |
| haram_distance_km | Distance from nearest haram facility |
| certification_status | not_applied, pending, certified, rejected, suspended |
| certification_date | Date certified |
| certification_expiry | Certification expiry |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

#### Table: goats
| Field | Description |
|-------|-------------|
| id | Primary key |
| goat_code | Unique goat code (HGG-2025-00001) |
| farm_id | Reference to farms |
| breed_id | Reference to breeds |
| gender | male, female |
| birth_date | Date of birth |
| source | born, purchased |
| source_farm_id | If purchased, source farm |
| mother_id | Reference to mother goat |
| father_id | Reference to father goat |
| weight_kg | Current weight |
| status | active, sold, slaughtered, dead, transferred |
| status_date | Date of status change |
| photo | Goat photo path |
| notes | Additional notes |
| created_at | Record created |
| updated_at | Record updated |

#### Table: health_records
| Field | Description |
|-------|-------------|
| id | Primary key |
| goat_id | Reference to goats |
| record_date | Date of record |
| illness_type_id | Reference to illness_types |
| symptoms | Symptoms observed |
| diagnosis | Diagnosis |
| treatment | Treatment given |
| medicine_type_id | Reference to medicine_types |
| medicine_dosage | Dosage given |
| is_medicine_halal | Is medicine halal certified |
| recovery_status | ongoing, recovered, critical, died |
| recovery_date | Date recovered |
| recorded_by | Reference to users |
| created_at | Record created |
| updated_at | Record updated |

#### Table: vaccinations
| Field | Description |
|-------|-------------|
| id | Primary key |
| goat_id | Reference to goats |
| vaccination_date | Date of vaccination |
| vaccine_name | Vaccine name |
| vaccine_brand | Vaccine brand |
| dosage | Dosage given |
| batch_number | Vaccine batch number |
| next_due_date | Next vaccination due |
| administered_by | Who administered |
| recorded_by | Reference to users |
| created_at | Record created |
| updated_at | Record updated |

#### Table: feed_records
| Field | Description |
|-------|-------------|
| id | Primary key |
| farm_id | Reference to farms |
| feed_date | Date of feeding |
| feed_type_id | Reference to feed_types |
| brand | Feed brand |
| supplier | Feed supplier |
| quantity_kg | Quantity in kg |
| ingredients | Feed ingredients |
| is_halal | Is feed halal certified |
| halal_flag_reason | Reason if flagged non-halal |
| recorded_by | Reference to users |
| created_at | Record created |
| updated_at | Record updated |

#### Table: inflows
| Field | Description |
|-------|-------------|
| id | Primary key |
| farm_id | Reference to farms |
| inflow_type | goat_purchase, goat_birth, feed, biologics, other |
| inflow_date | Date of inflow |
| goat_id | Reference to goats (if goat) |
| source | Source of inflow |
| quantity | Quantity |
| description | Description |
| recorded_by | Reference to users |
| created_at | Record created |
| updated_at | Record updated |

#### Table: outflows
| Field | Description |
|-------|-------------|
| id | Primary key |
| farm_id | Reference to farms |
| outflow_type | sale, slaughter, death, transfer |
| outflow_date | Date of outflow |
| goat_id | Reference to goats |
| destination | Destination |
| slaughterhouse_id | Reference to slaughterhouses |
| quantity | Quantity |
| price | Sale price (if sold) |
| death_cause | Cause of death (if died) |
| notes | Additional notes |
| recorded_by | Reference to users |
| created_at | Record created |
| updated_at | Record updated |

---

### TRACEABILITY TABLES

#### Table: transports 🔄 TBD
| Field | Description |
|-------|-------------|
| id | Primary key |
| transport_code | Unique transport code |
| outflow_id | Reference to outflows |
| farm_id | Source farm |
| slaughterhouse_id | Destination slaughterhouse |
| transport_date | Date of transport |
| vehicle_info | Vehicle details |
| driver_name | Driver name 🔄 TBD |
| goat_count | Number of goats |
| status | pending, in_transit, arrived, cancelled |
| arrival_date | Arrival date/time |
| arrival_confirmed_by | Reference to users |
| notes | Additional notes |
| recorded_by | Reference to users |
| created_at | Record created |
| updated_at | Record updated |

#### Table: slaughter_records
| Field | Description |
|-------|-------------|
| id | Primary key |
| slaughter_code | Unique slaughter code |
| slaughterhouse_id | Reference to slaughterhouses |
| goat_id | Reference to goats |
| farm_id | Source farm |
| transport_id | Reference to transports |
| slaughter_date | Date of slaughter |
| slaughter_time | Time of slaughter |
| slaughterer_name | Name of halal slaughterer |
| live_weight_kg | Weight before slaughter |
| carcass_weight_kg | Carcass weight |
| offal_weight_kg | Offal weight |
| meat_cuts | Types of cuts (JSON) |
| is_halal_verified | Halal verification status |
| verification_notes | Verification notes |
| status | pending, approved, rejected |
| approved_by | Reference to users |
| approved_at | Approval date/time |
| recorded_by | Reference to users |
| created_at | Record created |
| updated_at | Record updated |

#### Table: qr_codes
| Field | Description |
|-------|-------------|
| id | Primary key |
| qr_code | Unique QR code (HGBP-2026-00001) |
| slaughter_record_id | Reference to slaughter_records |
| goat_id | Reference to goats |
| farm_id | Reference to farms |
| product_type | Product type (chevon) |
| weight_kg | Product weight |
| qr_data | Full QR data (JSON) |
| blockchain_hash | Blockchain transaction hash |
| generated_at | QR generation time |
| generated_by | Reference to users |
| scan_count | Number of times scanned |
| last_scanned_at | Last scan time |
| status | active, revoked |
| created_at | Record created |
| updated_at | Record updated |

#### Table: blockchain_logs
| Field | Description |
|-------|-------------|
| id | Primary key |
| transaction_hash | Blockchain hash |
| transaction_type | Type of transaction |
| entity_type | Related entity |
| entity_id | Entity ID |
| data | Transaction data (JSON) |
| timestamp | Transaction time |
| created_at | Record created |

---

### CERTIFICATION TABLES

#### Table: certification_applications
| Field | Description |
|-------|-------------|
| id | Primary key |
| application_code | Unique application code |
| farm_id | Reference to farms |
| applicant_id | Reference to users |
| application_date | Date applied |
| application_type | new, renewal |
| status | pending, under_review, approved, rejected, cancelled |
| documents | Uploaded documents (JSON) |
| notes | Applicant notes |
| created_at | Record created |
| updated_at | Record updated |

#### Table: certification_reviews
| Field | Description |
|-------|-------------|
| id | Primary key |
| application_id | Reference to certification_applications |
| reviewer_id | Reference to users |
| review_date | Date of review |
| compliance_score | Compliance percentage |
| review_notes | Review notes |
| recommendation | approve, reject, need_info |
| recommendation_notes | Recommendation notes |
| created_at | Record created |
| updated_at | Record updated |

#### Table: certifications
| Field | Description |
|-------|-------------|
| id | Primary key |
| certificate_code | Unique certificate code |
| farm_id | Reference to farms |
| application_id | Reference to certification_applications |
| issued_date | Date issued |
| expiry_date | Expiry date |
| status | active, expired, suspended, revoked |
| issued_by | Reference to users |
| suspension_reason | Reason if suspended |
| suspension_date | Date suspended |
| revocation_reason | Reason if revoked |
| revocation_date | Date revoked |
| created_at | Record created |
| updated_at | Record updated |

---

### COMPLIANCE TABLES

#### Table: compliance_checks
| Field | Description |
|-------|-------------|
| id | Primary key |
| farm_id | Reference to farms |
| check_date | Date of check |
| check_type | auto, manual |
| feed_compliant | Feed is halal |
| medicine_compliant | Medicine is halal |
| distance_compliant | Distance from haram OK |
| health_compliant | Goat health OK |
| overall_compliant | Overall compliance |
| compliance_score | Compliance percentage |
| checked_by | Reference to users |
| created_at | Record created |
| updated_at | Record updated |

#### Table: compliance_warnings
| Field | Description |
|-------|-------------|
| id | Primary key |
| farm_id | Reference to farms |
| warning_type | non_halal_feed, non_halal_medicine, haram_distance, sick_goat |
| warning_date | Date warning raised |
| entity_type | Related entity |
| entity_id | Entity ID |
| description | Warning description |
| status | open, resolved, ignored |
| resolved_date | Date resolved |
| resolved_by | Reference to users |
| resolution_notes | Resolution notes |
| created_at | Record created |
| updated_at | Record updated |

---

### REFERENCE DATA TABLES

#### Table: breeds
| Field | Description |
|-------|-------------|
| id | Primary key |
| name | Breed name |
| description | Description |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

**Sample Data:**
| Name |
|------|
| Boer |
| Anglo-Nubian |
| Saanen |
| Alpine |
| Native |

#### Table: feed_types
| Field | Description |
|-------|-------------|
| id | Primary key |
| name | Feed type name |
| description | Description |
| default_halal_status | Default halal status |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

#### Table: medicine_types
| Field | Description |
|-------|-------------|
| id | Primary key |
| name | Medicine name |
| brand | Brand |
| is_halal_certified | Halal certified |
| halal_certificate | Certificate file |
| description | Description |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

#### Table: illness_types
| Field | Description |
|-------|-------------|
| id | Primary key |
| name | Illness name |
| description | Description |
| severity | low, medium, high, critical |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

#### Table: provinces
| Field | Description |
|-------|-------------|
| id | Primary key |
| name | Province name |
| region | Region |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

**Sample Data (Region 12):**
| Name |
|------|
| Sarangani |
| South Cotabato |
| Sultan Kudarat |
| Cotabato |

#### Table: municipalities
| Field | Description |
|-------|-------------|
| id | Primary key |
| province_id | Reference to provinces |
| name | Municipality name |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

**Sample Data (from document):**
| Province | Municipality |
|----------|--------------|
| Sarangani | Maasim |
| Sarangani | Kiamba |
| Sarangani | Maitum |
| South Cotabato | Lake Sebu |
| South Cotabato | Surallah |
| South Cotabato | Sto. Niño |
| Sultan Kudarat | Isulan |
| Sultan Kudarat | Pres. Quirino |
| Sultan Kudarat | Tacurong |

#### Table: barangays
| Field | Description |
|-------|-------------|
| id | Primary key |
| municipality_id | Reference to municipalities |
| name | Barangay name |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

#### Table: slaughterhouses
| Field | Description |
|-------|-------------|
| id | Primary key |
| code | Unique code |
| name | Slaughterhouse name |
| address | Address |
| municipality_id | Reference to municipalities |
| latitude | GPS latitude |
| longitude | GPS longitude |
| contact_person | Contact person |
| contact_phone | Contact phone |
| is_halal_certified | Halal certified |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

#### Table: haram_facilities
| Field | Description |
|-------|-------------|
| id | Primary key |
| name | Facility name |
| type | pig_farm, non_halal_slaughterhouse, other |
| address | Address |
| municipality_id | Reference to municipalities |
| latitude | GPS latitude |
| longitude | GPS longitude |
| status | active, inactive |
| created_at | Record created |
| updated_at | Record updated |

---

### SYSTEM TABLES

#### Table: audit_logs
| Field | Description |
|-------|-------------|
| id | Primary key |
| user_id | Reference to users |
| action | Action performed |
| entity_type | Entity affected |
| entity_id | Entity ID |
| old_values | Old values (JSON) |
| new_values | New values (JSON) |
| ip_address | User IP address |
| user_agent | Browser/device info |
| created_at | Record created |

#### Table: notifications
| Field | Description |
|-------|-------------|
| id | Primary key |
| user_id | Reference to users |
| type | Notification type |
| title | Notification title |
| message | Notification message |
| data | Additional data (JSON) |
| read_at | When read |
| created_at | Record created |
| updated_at | Record updated |

#### Table: settings
| Field | Description |
|-------|-------------|
| id | Primary key |
| key | Setting key |
| value | Setting value |
| type | string, number, boolean, json |
| description | Setting description |
| created_at | Record created |
| updated_at | Record updated |

---

## 5.5 Key Relationships Summary

| Parent Table | Child Table | Relationship | Description |
|--------------|-------------|--------------|-------------|
| users | farms | 1:M | One user can own many farms |
| users | user_roles | 1:M | One user can have many roles |
| roles | user_roles | 1:M | One role assigned to many users |
| farms | goats | 1:M | One farm has many goats |
| goats | health_records | 1:M | One goat has many health records |
| goats | vaccinations | 1:M | One goat has many vaccinations |
| farms | feed_records | 1:M | One farm has many feed records |
| farms | inflows | 1:M | One farm has many inflows |
| farms | outflows | 1:M | One farm has many outflows |
| outflows | transports | 1:1 | One outflow has one transport |
| goats | slaughter_records | 1:1 | One goat has one slaughter record |
| slaughter_records | qr_codes | 1:1 | One slaughter = one QR code |
| farms | certification_applications | 1:M | One farm can apply many times |
| certification_applications | certifications | 1:1 | One approved app = one cert |
| farms | compliance_checks | 1:M | One farm has many checks |
| farms | compliance_warnings | 1:M | One farm can have many warnings |
| provinces | municipalities | 1:M | One province has many municipalities |
| municipalities | barangays | 1:M | One municipality has many barangays |
| breeds | goats | 1:M | One breed for many goats |
| feed_types | feed_records | 1:M | One type for many records |
| medicine_types | health_records | 1:M | One type for many records |
| illness_types | health_records | 1:M | One type for many records |
| slaughterhouses | slaughter_records | 1:M | One slaughterhouse, many slaughters |

---

## 5.6 TBD Items (Pending Meeting)

| # | Table/Field | Question |
|---|-------------|----------|
| 1 | transports | Who records transport? Fields may change |
| 2 | transports.driver_name | Is this needed? Or separate Transporter role? |
| 3 | market-related tables | If market is included, need new tables |

---

## 5.7 Summary

| Category | Count |
|----------|-------|
| Total Tables | 31 |
| User Management | 3 |
| Farm Management | 7 |
| Traceability | 4 |
| Certification | 3 |
| Compliance | 2 |
| Reference Data | 9 |
| System | 3 |

---

## 5.8 Next Steps (Level 2 - Detailed Design)

When we proceed to Level 2, we will add:

| Item | Description |
|------|-------------|
| Complete field list | All fields with exact specifications |
| Data types | VARCHAR(100), BIGINT, DECIMAL(10,2), etc. |
| Constraints | NOT NULL, UNIQUE, DEFAULT values |
| Indexes | Primary, foreign, unique, composite indexes |
| Foreign key rules | ON DELETE CASCADE, ON UPDATE CASCADE, etc. |
| Migration files | Laravel migration scripts |
| Seeders | Initial data seeders |

---

## 5.9 Sample Data Examples

This section provides realistic sample data to help visualize what the database will contain.

---

### SAMPLE: users

| id | name | email | phone | status |
|----|------|-------|-------|--------|
| 1 | Juan Dela Cruz | juan@email.com | 09171234567 | active |
| 2 | Maria Santos | maria@email.com | 09181234567 | active |
| 3 | Ahmed Abdullah | ahmed@ncmf.gov.ph | 09191234567 | active |
| 4 | Pedro Reyes | pedro@lgu-maasim.gov.ph | 09201234567 | active |

---

### SAMPLE: roles

| id | name | display_name | level |
|----|------|--------------|-------|
| 1 | admin | System Admin | super |
| 2 | farm_owner | Farm Owner | head |
| 3 | farm_worker | Farm Worker | staff |
| 4 | certifier_head | Certifier Head (NCMF) | head |
| 5 | lgu_staff | LGU Staff | staff |
| 6 | consumer | Consumer | public |

---

### SAMPLE: farms

| id | farm_code | name | owner_id | barangay | municipality | province | certification_status |
|----|-----------|------|----------|----------|--------------|----------|---------------------|
| 1 | HGF-0001 | Dela Cruz Goat Farm | 1 | Tinoto | Maasim | Sarangani | certified |
| 2 | HGF-0002 | Santos Farm | 2 | Lamian | Kiamba | Sarangani | pending |
| 3 | HGF-0003 | Green Valley Farm | 5 | Ned | Lake Sebu | South Cotabato | not_applied |

---

### SAMPLE: goats

| id | goat_code | farm_id | breed | gender | birth_date | age_class | status |
|----|-----------|---------|-------|--------|------------|-----------|--------|
| 1 | HGG-2025-00001 | 1 | Boer | male | 2024-03-15 | Buck | active |
| 2 | HGG-2025-00002 | 1 | Anglo-Nubian | female | 2024-05-20 | Doe | active |
| 3 | HGG-2025-00003 | 1 | Native | female | 2025-01-10 | Kid | active |
| 4 | HGG-2025-00004 | 2 | Boer Cross | male | 2024-08-01 | Grower | active |
| 5 | HGG-2025-00005 | 1 | Boer | male | 2023-06-15 | Buck | slaughtered |

---

### SAMPLE: health_records

| id | goat_id | record_date | illness | symptoms | treatment | medicine | is_halal | recovery_status |
|----|---------|-------------|---------|----------|-----------|----------|----------|-----------------|
| 1 | 2 | 2025-01-15 | Parasites | Weight loss, dull coat | Deworming | Ivermectin | Yes | recovered |
| 2 | 3 | 2025-01-20 | Diarrhea | Loose stool | Oral rehydration | Electrolytes | Yes | recovered |
| 3 | 4 | 2025-01-25 | Foot rot | Limping | Hoof trim + spray | Zinc Sulfate | Yes | ongoing |

---

### SAMPLE: feed_records

| id | farm_id | feed_date | feed_type | brand | quantity_kg | is_halal | halal_flag_reason |
|----|---------|-----------|-----------|-------|-------------|----------|-------------------|
| 1 | 1 | 2025-01-15 | Commercial Feed | B-Meg Goat Grower | 50 | Yes | - |
| 2 | 1 | 2025-01-15 | Roughage | Natural Grass | 100 | Yes | - |
| 3 | 2 | 2025-01-16 | Concentrate | Unknown Brand | 25 | No | Contains animal by-products |

---

### SAMPLE: vaccinations

| id | goat_id | vaccination_date | vaccine_name | dosage | next_due_date | administered_by |
|----|---------|------------------|--------------|--------|---------------|-----------------|
| 1 | 1 | 2024-06-15 | PPR Vaccine | 1 ml | 2025-06-15 | Dr. Garcia |
| 2 | 2 | 2024-08-20 | Enterotoxemia | 2 ml | 2025-08-20 | Dr. Garcia |
| 3 | 1 | 2025-01-10 | Dewormer | 5 ml | 2025-04-10 | Farm Worker |

---

### SAMPLE: slaughter_records

| id | slaughter_code | slaughterhouse | goat_id | slaughter_date | slaughterer_name | live_weight_kg | carcass_weight_kg | is_halal_verified |
|----|----------------|----------------|---------|----------------|------------------|----------------|-------------------|-------------------|
| 1 | HGS-2025-00001 | Maasim Halal Slaughterhouse | 5 | 2025-01-28 | Ustadz Ibrahim | 35.5 | 17.2 | Yes |

---

### SAMPLE: qr_codes

| id | qr_code | slaughter_record_id | goat_id | farm_id | product_type | weight_kg | scan_count |
|----|---------|---------------------|---------|---------|--------------|-----------|------------|
| 1 | HGBP-2026-00001 | 1 | 5 | 1 | Chevon (whole) | 17.2 | 0 |

---

### SAMPLE: certification_applications

| id | application_code | farm_id | applicant_id | application_date | application_type | status |
|----|------------------|---------|--------------|------------------|------------------|--------|
| 1 | HGC-APP-2025-001 | 1 | 1 | 2024-12-01 | new | approved |
| 2 | HGC-APP-2025-002 | 2 | 2 | 2025-01-15 | new | under_review |
| 3 | HGC-APP-2025-003 | 3 | 5 | 2025-01-28 | new | pending |

---

### SAMPLE: certifications

| id | certificate_code | farm_id | issued_date | expiry_date | status | issued_by |
|----|------------------|---------|-------------|-------------|--------|-----------|
| 1 | HGC-CERT-2025-001 | 1 | 2025-01-01 | 2026-01-01 | active | Ahmed Abdullah |

---

### SAMPLE: compliance_checks

| id | farm_id | check_date | check_type | feed_compliant | medicine_compliant | distance_compliant | overall_compliant | compliance_score |
|----|---------|------------|------------|----------------|--------------------|--------------------|-------------------|------------------|
| 1 | 1 | 2025-01-15 | auto | Yes | Yes | Yes | Yes | 100% |
| 2 | 2 | 2025-01-16 | auto | No | Yes | Yes | No | 75% |
| 3 | 1 | 2025-01-28 | manual | Yes | Yes | Yes | Yes | 100% |

---

### SAMPLE: compliance_warnings

| id | farm_id | warning_type | warning_date | description | status |
|----|---------|--------------|--------------|-------------|--------|
| 1 | 2 | non_halal_feed | 2025-01-16 | Feed record contains non-halal feed (Unknown Brand) | open |

---

### SAMPLE: provinces, municipalities, barangays

**provinces:**
| id | name | region |
|----|------|--------|
| 1 | Sarangani | Region XII |
| 2 | South Cotabato | Region XII |
| 3 | Sultan Kudarat | Region XII |

**municipalities:**
| id | province_id | name |
|----|-------------|------|
| 1 | 1 | Maasim |
| 2 | 1 | Kiamba |
| 3 | 1 | Maitum |
| 4 | 2 | Lake Sebu |
| 5 | 2 | Surallah |

**barangays:**
| id | municipality_id | name |
|----|-----------------|------|
| 1 | 1 | Tinoto |
| 2 | 1 | Kamanga |
| 3 | 2 | Lamian |
| 4 | 4 | Ned |
| 5 | 4 | Poblacion |

---

### SAMPLE: slaughterhouses

| id | code | name | municipality_id | is_halal_certified | status |
|----|------|------|-----------------|--------------------|----|
| 1 | SH-001 | Maasim Halal Slaughterhouse | 1 | Yes | active |
| 2 | SH-002 | Kiamba Public Slaughterhouse | 2 | Yes | active |

---

### SAMPLE: haram_facilities

| id | name | type | municipality_id | latitude | longitude |
|----|------|------|-----------------|----------|-----------|
| 1 | ABC Piggery | pig_farm | 1 | 5.8521 | 125.0147 |
| 2 | XYZ Hog Farm | pig_farm | 2 | 5.9832 | 124.6214 |

---

### SAMPLE: audit_logs

| id | user_id | action | entity_type | entity_id | old_values | new_values | created_at |
|----|---------|--------|-------------|-----------|------------|------------|------------|
| 1 | 1 | create | goat | 3 | null | {"goat_code":"HGG-2025-00003"...} | 2025-01-10 08:30:00 |
| 2 | 3 | update | certification | 1 | {"status":"pending"} | {"status":"active"} | 2025-01-01 10:00:00 |
| 3 | 1 | create | feed_record | 1 | null | {"feed_type":"Commercial Feed"...} | 2025-01-15 14:20:00 |

---

### SAMPLE: notifications

| id | user_id | type | title | message | read_at |
|----|---------|------|-------|---------|---------|
| 1 | 1 | certification | Certification Approved | Your farm HGF-0001 has been certified! | 2025-01-01 12:00:00 |
| 2 | 2 | warning | Compliance Warning | Non-halal feed detected in your records | null |
| 3 | 1 | reminder | Vaccination Due | Goat HGG-2025-00001 PPR vaccine due in 30 days | null |

---

## ✅ STEP 5 COMPLETE (OVERVIEW)

**Status:** High-Level Overview — Detailed design to follow in Level 2

**Next Steps:**
1. Conduct clarification meeting
2. Update TBD items
3. Proceed to Level 2 detailed database design (or other steps)

---

*Document Version: 1.1 (OVERVIEW)*
*Last Updated: February 1, 2026*
*Status: High-Level — Not Final*
