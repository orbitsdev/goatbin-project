# Compliance Tables

---

## compliance_checks

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| farm_id | BIGINT | NO | FK → farms |
| check_date | DATE | NO | Check date |
| check_type | ENUM('auto','manual') | NO | Check type |
| feed_compliant | BOOLEAN | NO | Feed is halal |
| medicine_compliant | BOOLEAN | NO | Medicine is halal |
| distance_compliant | BOOLEAN | NO | Distance from haram OK |
| health_compliant | BOOLEAN | NO | Goat health OK |
| overall_compliant | BOOLEAN | NO | Overall compliance |
| compliance_score | DECIMAL(5,2) | NO | Compliance % |
| checked_by | BIGINT | YES | FK → users (null if auto) |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | farm_id | check_date | check_type | feed_compliant | medicine_compliant | distance_compliant | health_compliant | overall_compliant | compliance_score | checked_by |
|----|---------|------------|------------|----------------|--------------------|--------------------|------------------|-------------------|------------------|------------|
| 1 | 1 | 2025-01-15 | auto | Yes | Yes | Yes | Yes | Yes | 100.00 | - |
| 2 | 2 | 2025-01-16 | auto | No | Yes | Yes | Yes | No | 75.00 | - |
| 3 | 1 | 2025-01-28 | manual | Yes | Yes | Yes | Yes | Yes | 100.00 | 3 |
| 4 | 2 | 2025-01-20 | manual | No | Yes | Yes | Yes | No | 75.00 | 3 |
| 5 | 3 | 2025-01-25 | auto | Yes | Yes | Yes | No | No | 75.00 | - |

**Compliance Score Calculation:**

| Factor | Weight | Example |
|--------|--------|---------|
| Feed Compliant | 25% | Yes = 25, No = 0 |
| Medicine Compliant | 25% | Yes = 25, No = 0 |
| Distance Compliant | 25% | Yes = 25, No = 0 |
| Health Compliant | 25% | Yes = 25, No = 0 |
| **Total** | **100%** | Sum of all factors |

---

## compliance_warnings

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| farm_id | BIGINT | NO | FK → farms |
| warning_type | ENUM('non_halal_feed','non_halal_medicine','haram_distance','sick_goat') | NO | Warning type |
| warning_date | DATE | NO | Warning date |
| entity_type | VARCHAR(50) | YES | Related entity type |
| entity_id | BIGINT | YES | Entity ID |
| description | TEXT | NO | Description |
| status | ENUM('open','resolved','ignored') | NO | Status |
| resolved_date | DATE | YES | Resolution date |
| resolved_by | BIGINT | YES | FK → users |
| resolution_notes | TEXT | YES | Resolution notes |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | farm_id | warning_type | warning_date | entity_type | entity_id | description | status |
|----|---------|--------------|--------------|-------------|-----------|-------------|--------|
| 1 | 2 | non_halal_feed | 2025-01-16 | feed_record | 3 | Feed record contains non-halal feed (Unknown Brand with animal by-products) | open |
| 2 | 1 | sick_goat | 2025-01-25 | health_record | 3 | Goat HGG-2025-00004 has foot rot - ongoing treatment | resolved |
| 3 | 3 | haram_distance | 2025-01-20 | farm | 3 | Farm is less than 1km from pig farm (DEF Piggery) | open |
| 4 | 2 | non_halal_medicine | 2025-01-18 | health_record | 5 | Medicine used not halal certified | resolved |

**Example of Resolved Warning:**

| id | farm_id | warning_type | description | status | resolved_date | resolved_by | resolution_notes |
|----|---------|--------------|-------------|--------|---------------|-------------|------------------|
| 2 | 1 | sick_goat | Goat #4 has foot rot | resolved | 2025-01-30 | 1 | Goat fully recovered after treatment. Health record updated. |
| 4 | 2 | non_halal_medicine | Medicine not halal certified | resolved | 2025-01-22 | 2 | Replaced with halal-certified alternative (Ivomec). |
