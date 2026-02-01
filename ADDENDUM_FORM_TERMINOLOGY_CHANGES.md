# 📋 HALAL GOAT BIN PROJECT - DOCUMENTATION

## ADDENDUM: UPDATES BASED ON EXISTING FORMS

**Project:** Halal GOAT Bin: A Geographically-Oriented Application and Traceability System  
**Date:** February 1, 2026  
**Document:** Addendum - Changes from Discovered Forms & Terminology  
**Status:** To be incorporated in Level 2 (Detailed Design)

---

# ADDENDUM: CHANGES & UPDATES

## 1. Overview

During the documentation process, existing manual forms used in goat farm management were discovered. These forms reveal industry-standard terminology and data fields that need to be incorporated into our system design.

---

## 2. Source Documents Discovered

| Form | Title | Purpose |
|------|-------|---------|
| Annex 1 | Baseline Survey Form | Farm & owner registration |
| Annex 1 | Stock Information | Goat inventory by breed |
| Annex 1 | Feeds and Feeding System | Feed types and methods |
| Annex 1 | Health Management | Treatment and diseases |
| Annex 1 | Housing | Farm facility details |
| Annex 1 | Marketing | Sales outlets |
| Annex 1 | Problems Checklist | Issues faced by farmers |
| Form 1 | Inventory Record | Monthly livestock count |
| Form 2 | Production & Reproduction Record | Breeding and birth records |
| Form 3 | Disease & Parasite Control | Health/treatment records |
| Financial | Cash Inflow | Sales records |
| Financial | Cash Outflow | Expenses records |

---

## 3. Industry Terminology Discovered

### 3.1 Production Type (Why goat is raised)

| Term | Meaning |
|------|---------|
| **For Breeding** | Goat is kept to produce offspring |
| **For Slaughter** | Goat is raised for meat (chevon) |
| **For Dairy** | Goat is raised for milk production |

### 3.2 Class of Animals (Age Group)

| Term | Age | Description |
|------|-----|-------------|
| **Kid** | Less than 1 month | Newborn baby goat |
| **Kids** | 1-3 months | Young goat |
| **Grower** | 3-8 months | Growing/teenager goat |
| **Buck** | Male 8+ months | Adult male goat |
| **Doe** | Female 8+ months | Adult female goat |

### 3.3 Class of Breeders (Female Reproductive Status)

| Term | Meaning |
|------|---------|
| **Doeling** | Young female, never been bred |
| **Dry Does** | Adult female, not pregnant and not lactating |
| **Pregnant** | Female carrying baby |
| **Lactating** | Female currently producing milk |
| **Buck** | Male used for breeding |

### 3.4 Gender

| Term | Meaning |
|------|---------|
| **Male** | Male goat |
| **Female** | Female goat |

### 3.5 Breed Type

| Term | Meaning |
|------|---------|
| **Native** | Local/indigenous Philippine breed |
| **Upgrade** | Native crossed with improved breed |
| **Cross** | Mixed breeds |
| **Pure** | Purebred (100% single breed) |

### 3.6 Bloodline (Used in Reproduction Records)

| Term | Meaning |
|------|---------|
| **Native** | Local bloodline |
| **Upgrade** | Improved bloodline |
| **Exotic** | Foreign breed |
| **Crossbred** | Mixed bloodline |

### 3.7 Other Important Terms

| Term | Meaning |
|------|---------|
| **Dam** | Mother goat (female parent) |
| **Sire** | Father goat (male parent) |
| **Kidding** | Giving birth |
| **Weaning** | When baby stops drinking mother's milk |
| **Buck Service** | Using male goat for breeding (sometimes charged as service) |

---

## 4. Impact on Documentation

### 4.1 Steps Affected

| Step | Document | Affected? | Impact Level |
|------|----------|-----------|--------------|
| Step 1 | Stakeholders | ❌ No | None |
| Step 2 | User Roles & Permissions | ❌ No | None |
| Step 3 | Business Process Flow | ❌ No | None |
| Step 4 | Modules & Features | ⚠️ Yes | Minor - Add fields |
| Step 5 | Database Design | ✅ Yes | Moderate - Add tables & fields |

### 4.2 Summary of Changes

| Category | Type | Count |
|----------|------|-------|
| New Reference Tables | Add | 4 tables |
| goats Table | Update | 10+ new fields |
| Module Features | Update | New form fields |
| System Logic | Add | Auto-calculation |

---

## 5. Database Changes

### 5.1 New Reference Tables to Add

#### Table: production_types
| Field | Type | Description |
|-------|------|-------------|
| id | BIGINT (PK) | Primary key |
| name | VARCHAR(50) | Production type name |
| description | TEXT | Description |
| status | ENUM | active, inactive |
| created_at | TIMESTAMP | Record created |
| updated_at | TIMESTAMP | Record updated |

**Initial Data:**
| ID | Name | Description |
|----|------|-------------|
| 1 | For Breeding | Goat kept to produce offspring |
| 2 | For Slaughter | Goat raised for meat |
| 3 | For Dairy | Goat raised for milk production |

---

#### Table: age_classes
| Field | Type | Description |
|-------|------|-------------|
| id | BIGINT (PK) | Primary key |
| name | VARCHAR(50) | Age class name |
| code | VARCHAR(10) | Short code |
| min_age_days | INT | Minimum age in days |
| max_age_days | INT | Maximum age in days (null for no max) |
| gender | ENUM | male, female, both |
| description | TEXT | Description |
| status | ENUM | active, inactive |
| created_at | TIMESTAMP | Record created |
| updated_at | TIMESTAMP | Record updated |

**Initial Data:**
| ID | Name | Code | Min Days | Max Days | Gender | Description |
|----|------|------|----------|----------|--------|-------------|
| 1 | Kid | KID | 0 | 30 | both | Less than 1 month |
| 2 | Kids | KIDS | 31 | 90 | both | 1-3 months |
| 3 | Grower | GRW | 91 | 240 | both | 3-8 months |
| 4 | Buck | BUCK | 241 | null | male | Male 8+ months |
| 5 | Doe | DOE | 241 | null | female | Female 8+ months |

---

#### Table: breeding_statuses
| Field | Type | Description |
|-------|------|-------------|
| id | BIGINT (PK) | Primary key |
| name | VARCHAR(50) | Status name |
| code | VARCHAR(10) | Short code |
| applicable_gender | ENUM | male, female |
| description | TEXT | Description |
| status | ENUM | active, inactive |
| created_at | TIMESTAMP | Record created |
| updated_at | TIMESTAMP | Record updated |

**Initial Data:**
| ID | Name | Code | Gender | Description |
|----|------|------|--------|-------------|
| 1 | Doeling | DLG | female | Young female, never bred |
| 2 | Dry Does | DRY | female | Not pregnant and not lactating |
| 3 | Pregnant | PRG | female | Currently carrying baby |
| 4 | Lactating | LAC | female | Currently producing milk |
| 5 | Buck | BCK | male | Male used for breeding |

---

#### Table: breed_types
| Field | Type | Description |
|-------|------|-------------|
| id | BIGINT (PK) | Primary key |
| name | VARCHAR(50) | Breed type name |
| code | VARCHAR(10) | Short code |
| description | TEXT | Description |
| status | ENUM | active, inactive |
| created_at | TIMESTAMP | Record created |
| updated_at | TIMESTAMP | Record updated |

**Initial Data:**
| ID | Name | Code | Description |
|----|------|------|-------------|
| 1 | Native | NAT | Local/indigenous breed |
| 2 | Upgrade | UPG | Native crossed with improved breed |
| 3 | Cross | CRS | Mixed breeds |
| 4 | Pure | PUR | Purebred (100% single breed) |

---

### 5.2 Update to goats Table

#### New Fields to Add:

| Field | Type | Description | Notes |
|-------|------|-------------|-------|
| breed_type_id | BIGINT (FK) | Reference to breed_types | Native, Upgrade, Cross, Pure |
| age_class_id | BIGINT (FK) | Reference to age_classes | Auto-calculated based on birth_date |
| production_type_id | BIGINT (FK) | Reference to production_types | For Breeding, Slaughter, Dairy |
| breeding_status_id | BIGINT (FK) | Reference to breeding_statuses | For females only |
| dam_id | BIGINT (FK) | Reference to goats (mother) | Self-referencing |
| sire_id | BIGINT (FK) | Reference to goats (father) | Self-referencing |
| weight_at_birth_kg | DECIMAL(10,2) | Weight at birth | In kilograms |
| weight_at_3mo_kg | DECIMAL(10,2) | Weight at 3 months | In kilograms |
| weight_at_8mo_kg | DECIMAL(10,2) | Weight at 8 months | In kilograms |
| weaning_date | DATE | Date of weaning | When stopped mother's milk |
| weaning_age_months | INT | Age at weaning | In months |
| expected_kidding_date | DATE | Expected birth date | For pregnant does |
| last_breeding_date | DATE | Last breeding date | For tracking |

#### Updated goats Table Structure:

```
goats
├── id (PK)
├── goat_code (unique)
├── farm_id (FK → farms)
├── breed_id (FK → breeds)
├── breed_type_id (FK → breed_types)          ← NEW
├── gender (male, female)
├── birth_date
├── age_class_id (FK → age_classes)           ← NEW (auto-calculated)
├── production_type_id (FK → production_types) ← NEW
├── breeding_status_id (FK → breeding_statuses)← NEW (females)
├── source (born, purchased)
├── source_farm_id (FK → farms)
├── dam_id (FK → goats)                        ← NEW
├── sire_id (FK → goats)                       ← NEW
├── weight_at_birth_kg                         ← NEW
├── weight_at_3mo_kg                           ← NEW
├── weight_at_8mo_kg                           ← NEW
├── weight_current_kg
├── weaning_date                               ← NEW
├── weaning_age_months                         ← NEW
├── expected_kidding_date                      ← NEW
├── last_breeding_date                         ← NEW
├── status (active, sold, slaughtered, dead, transferred)
├── status_date
├── photo
├── notes
├── created_at
└── updated_at
```

---

### 5.3 Updated Entity Count

| Category | Original | New | Change |
|----------|----------|-----|--------|
| Reference Tables | 9 | 13 | +4 |
| Total Tables | 31 | 35 | +4 |

---

## 6. Module & Feature Changes

### 6.1 Goat Registration Form - New Fields

| Field | Type | Required | Options/Notes |
|-------|------|----------|---------------|
| Production Type | Dropdown | Yes | For Breeding, For Slaughter, For Dairy |
| Breed Type | Dropdown | Yes | Native, Upgrade, Cross, Pure |
| Breed | Dropdown | Yes | Boer, Anglo-Nubian, Saanen, Native, etc. |
| Breeding Status | Dropdown | Females only | Doeling, Dry Does, Pregnant, Lactating |
| Dam (Mother) | Search/Select | No | Select from existing Does in farm |
| Sire (Father) | Search/Select | No | Select from existing Bucks |
| Weight at Birth | Number | No | In kg |
| Weight at 3 months | Number | No | In kg |
| Weight at 8 months | Number | No | In kg |
| Weaning Date | Date | No | When stopped drinking mother's milk |

### 6.2 System Auto-Calculations

| Field | Auto-Calculation Logic |
|-------|------------------------|
| **Age Class** | Based on birth_date and gender: |
| | - Less than 30 days = Kid |
| | - 31-90 days = Kids |
| | - 91-240 days = Grower |
| | - 241+ days + Male = Buck |
| | - 241+ days + Female = Doe |
| **Age (Display)** | Calculate from birth_date to current date |

### 6.3 Breeding Status Transitions

```
FEMALE GOAT LIFECYCLE:

Doeling (young, never bred)
    │
    │ First breeding
    ▼
Pregnant
    │
    │ Gives birth (kidding)
    ▼
Lactating (producing milk)
    │
    │ Milk dries up / weaning complete
    ▼
Dry Does
    │
    │ Bred again
    ▼
Pregnant (cycle repeats)
```

---

## 7. Form-to-System Mapping

### 7.1 Form 1: Inventory Record → System Feature

| Form Field | System Equivalent |
|------------|-------------------|
| Class of Animals | age_class_id + breeding_status_id |
| Number of Head Last Month | Calculated from goats table |
| Number of Head This Month | Calculated from goats table |
| Number Added | Calculated from inflows |
| Number Reduced | Calculated from outflows |
| % Change | Auto-calculated |

**System Feature:** Population Dashboard / Inventory Report

---

### 7.2 Form 2: Production & Reproduction → System Feature

| Form Field | System Equivalent |
|------------|-------------------|
| Buck ID | sire_id |
| Dam | dam_id |
| Blood line | breed_type_id |
| Date of Breeding | last_breeding_date |
| Expected Date of Kidding | expected_kidding_date |
| Kidding Date | birth_date (of new kid) |
| Sex | gender |
| Birth Type | New field: birth_type (single, twin, triplet) |
| Birth Status | New field: birth_status (alive, dead) |
| Weight at Birth | weight_at_birth_kg |
| Weight 3 months | weight_at_3mo_kg |
| Weight 8 months | weight_at_8mo_kg |
| Slaughtered Weight/Age | In slaughter_records table |
| Age at Weaning | weaning_age_months |

**System Feature:** Production & Reproduction Records (new sub-module)

---

### 7.3 Form 3: Disease & Parasite Control → System Feature

| Form Field | System Equivalent |
|------------|-------------------|
| Animal ID | goat_id |
| Classification | age_class_id + gender |
| Symptoms | symptoms (in health_records) |
| Date of Occurrence | record_date |
| Biologics Given | medicine_type_id + treatment |
| Quantity Used | medicine_dosage |
| Remarks (dead or alive) | recovery_status |

**System Feature:** Health & Medical Records (already exists)

---

### 7.4 Financial Report → System Feature

| Form Section | System Equivalent |
|--------------|-------------------|
| Cash Inflow (Sales) | New table: financial_inflows (optional) |
| Cash Outflow (Expenses) | New table: financial_outflows (optional) |

**Note:** Financial module is optional — can be added in Phase 2 or later.

---

## 8. Additional Considerations

### 8.1 Possible New Module: Breeding Management

Based on Form 2, a dedicated **Breeding Management** sub-module may be useful:

| Feature | Description |
|---------|-------------|
| Record Breeding Event | Record when buck mates with doe |
| Expected Kidding Date | Auto-calculate (150 days gestation) |
| Kidding Record | Record birth details |
| Lineage Tracking | Track dam/sire relationships |
| Breeding History | View breeding history per goat |

### 8.2 Possible New Module: Financial Management

Based on Financial Forms, a **Financial Module** could include:

| Feature | Description |
|---------|-------------|
| Record Sales | Animals, manure, buck service, forages |
| Record Expenses | Feeds, biologics, labor, utilities |
| Financial Reports | Income vs expenses |

**Recommendation:** Mark as Phase 2 feature — not core to halal traceability.

---

## 9. Summary of Changes

### 9.1 Database Changes

| Change Type | Count | Details |
|-------------|-------|---------|
| New Tables | 4 | production_types, age_classes, breeding_statuses, breed_types |
| Updated Tables | 1 | goats (13 new fields) |
| Total New Fields | 13 | In goats table |

### 9.2 Feature Changes

| Change Type | Count | Details |
|-------------|-------|---------|
| New Form Fields | 10 | In Goat Registration |
| Auto-Calculations | 2 | Age Class, Age Display |
| New Sub-Module | 1 | Breeding Management (optional) |

### 9.3 Optional Future Additions

| Addition | Priority | Phase |
|----------|----------|-------|
| Financial Module | Low | Phase 2+ |
| Breeding Management | Medium | Phase 1 or 2 |
| Inventory Reports | Medium | Phase 1 |

---

## 10. Action Items

| # | Action | When | Status |
|---|--------|------|--------|
| 1 | Incorporate changes in Level 2 Database Design | During detailed design | 🔄 Pending |
| 2 | Update goats table with new fields | During detailed design | 🔄 Pending |
| 3 | Add new reference tables | During detailed design | 🔄 Pending |
| 4 | Update Goat Registration form wireframe | During UI design | 🔄 Pending |
| 5 | Decide on Breeding Management module | In meeting | 🔄 TBD |
| 6 | Decide on Financial module | In meeting | 🔄 TBD |

---

## ✅ ADDENDUM COMPLETE

**This document serves as a record of changes to be incorporated in Level 2 (Detailed Design).**

---

*Document Version: 1.0*  
*Last Updated: February 1, 2026*  
*Related Documents: Step 4 (Modules), Step 5 (Database)*
