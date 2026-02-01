# Farm Management Tables

---

## farms

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| farm_code | VARCHAR(20) | NO | Unique code (HGF-0001) |
| name | VARCHAR(100) | NO | Farm name |
| owner_id | BIGINT | NO | FK → users |
| address | TEXT | YES | Full address |
| barangay_id | BIGINT | NO | FK → barangays |
| municipality_id | BIGINT | NO | FK → municipalities |
| province_id | BIGINT | NO | FK → provinces |
| latitude | DECIMAL(10,8) | YES | GPS latitude |
| longitude | DECIMAL(11,8) | YES | GPS longitude |
| area_hectares | DECIMAL(10,2) | YES | Farm area |
| haram_distance_km | DECIMAL(10,2) | YES | Distance from haram facility |
| certification_status | ENUM('not_applied','pending','certified','rejected','suspended') | NO | Certification status |
| certification_date | DATE | YES | Date certified |
| certification_expiry | DATE | YES | Certification expiry date |
| status | ENUM('active','inactive') | NO | Farm status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | farm_code | name | owner_id | municipality | province | haram_distance_km | certification_status |
|----|-----------|------|----------|--------------|----------|-------------------|---------------------|
| 1 | HGF-0001 | Dela Cruz Goat Farm | 1 | Maasim | Sarangani | 5.2 | certified |
| 2 | HGF-0002 | Santos Halal Farm | 2 | Kiamba | Sarangani | 3.8 | pending |
| 3 | HGF-0003 | Green Valley Farm | 6 | Lake Sebu | South Cotabato | 8.5 | not_applied |

---

## goats

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| goat_code | VARCHAR(20) | NO | Unique code (HGG-2025-00001) |
| farm_id | BIGINT | NO | FK → farms |
| breed_id | BIGINT | NO | FK → breeds |
| breed_type_id | BIGINT | NO | FK → breed_types |
| gender | ENUM('male','female') | NO | Gender |
| birth_date | DATE | NO | Date of birth |
| age_class_id | BIGINT | NO | FK → age_classes (auto-calculated) |
| production_type_id | BIGINT | NO | FK → production_types |
| breeding_status_id | BIGINT | YES | FK → breeding_statuses (females only) |
| source | ENUM('born','purchased') | NO | How acquired |
| source_farm_id | BIGINT | YES | FK → farms (if purchased) |
| dam_id | BIGINT | YES | FK → goats (mother) |
| sire_id | BIGINT | YES | FK → goats (father) |
| weight_at_birth_kg | DECIMAL(10,2) | YES | Birth weight |
| weight_at_3mo_kg | DECIMAL(10,2) | YES | Weight at 3 months |
| weight_at_8mo_kg | DECIMAL(10,2) | YES | Weight at 8 months |
| weight_current_kg | DECIMAL(10,2) | YES | Current weight |
| weaning_date | DATE | YES | Weaning date |
| weaning_age_months | INT | YES | Age at weaning |
| expected_kidding_date | DATE | YES | Expected birth (pregnant does) |
| last_breeding_date | DATE | YES | Last breeding date |
| status | ENUM('active','sold','slaughtered','dead','transferred') | NO | Status |
| status_date | DATE | YES | Status change date |
| photo | VARCHAR(255) | YES | Photo path |
| notes | TEXT | YES | Notes |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | goat_code | farm_id | breed | breed_type | gender | birth_date | age_class | production_type | breeding_status | weight_current_kg | status |
|----|-----------|---------|-------|------------|--------|------------|-----------|-----------------|-----------------|-------------------|--------|
| 1 | HGG-2025-00001 | 1 | Boer | Pure | male | 2024-03-15 | Buck | For Breeding | Buck | 42.0 | active |
| 2 | HGG-2025-00002 | 1 | Anglo-Nubian | Upgrade | female | 2024-05-20 | Doe | For Breeding | Pregnant | 35.5 | active |
| 3 | HGG-2025-00003 | 1 | Boer | Pure | female | 2025-01-10 | Kid | For Slaughter | Doeling | 4.5 | active |
| 4 | HGG-2025-00004 | 1 | Native | Native | male | 2024-10-01 | Grower | For Slaughter | - | 18.0 | active |
| 5 | HGG-2025-00005 | 2 | Boer Cross | Cross | female | 2024-02-15 | Doe | For Dairy | Lactating | 38.0 | active |
| 6 | HGG-2025-00006 | 1 | Boer | Pure | male | 2023-06-15 | Buck | For Slaughter | Buck | 45.0 | slaughtered |

---

## health_records

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| goat_id | BIGINT | NO | FK → goats |
| record_date | DATE | NO | Date of record |
| illness_type_id | BIGINT | YES | FK → illness_types |
| symptoms | TEXT | YES | Symptoms observed |
| diagnosis | TEXT | YES | Diagnosis |
| treatment | TEXT | YES | Treatment given |
| medicine_type_id | BIGINT | YES | FK → medicine_types |
| medicine_dosage | VARCHAR(50) | YES | Dosage |
| is_medicine_halal | BOOLEAN | NO | Is medicine halal |
| recovery_status | ENUM('ongoing','recovered','critical','died') | NO | Status |
| recovery_date | DATE | YES | Recovery date |
| recorded_by | BIGINT | NO | FK → users |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | goat_id | record_date | illness | symptoms | treatment | medicine | is_halal | recovery_status |
|----|---------|-------------|---------|----------|-----------|----------|----------|-----------------|
| 1 | 2 | 2025-01-15 | Parasites | Weight loss, dull coat | Deworming | Ivermectin | Yes | recovered |
| 2 | 3 | 2025-01-20 | Diarrhea | Loose stool, weakness | Oral rehydration | Electrolytes | Yes | recovered |
| 3 | 4 | 2025-01-25 | Foot Rot | Limping, swollen hoof | Hoof trim + spray | Zinc Sulfate | Yes | ongoing |

---

## vaccinations

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| goat_id | BIGINT | NO | FK → goats |
| vaccination_date | DATE | NO | Date of vaccination |
| vaccine_name | VARCHAR(100) | NO | Vaccine name |
| vaccine_brand | VARCHAR(100) | YES | Brand |
| dosage | VARCHAR(50) | NO | Dosage given |
| batch_number | VARCHAR(50) | YES | Batch number |
| next_due_date | DATE | YES | Next vaccination due |
| administered_by | VARCHAR(100) | YES | Who administered |
| recorded_by | BIGINT | NO | FK → users |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | goat_id | vaccination_date | vaccine_name | vaccine_brand | dosage | batch_number | next_due_date | administered_by |
|----|---------|------------------|--------------|---------------|--------|--------------|---------------|-----------------|
| 1 | 1 | 2024-06-15 | PPR Vaccine | Raksha PPR | 1ml | PPR-2024-001 | 2025-06-15 | Dr. Garcia |
| 2 | 2 | 2024-08-20 | Enterotoxemia | Covexin 8 | 2ml | COV-2024-052 | 2025-08-20 | Dr. Garcia |
| 3 | 1 | 2025-01-10 | Dewormer | Ivomec | 5ml | IVO-2025-003 | 2025-04-10 | Juan Dela Cruz |
| 4 | 4 | 2025-01-12 | PPR Vaccine | Raksha PPR | 1ml | PPR-2025-001 | 2026-01-12 | Dr. Garcia |

---

## feed_records

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| farm_id | BIGINT | NO | FK → farms |
| feed_date | DATE | NO | Date of feeding |
| feed_type_id | BIGINT | NO | FK → feed_types |
| brand | VARCHAR(100) | YES | Feed brand |
| supplier | VARCHAR(100) | YES | Supplier |
| quantity_kg | DECIMAL(10,2) | NO | Quantity in kg |
| ingredients | TEXT | YES | Feed ingredients |
| is_halal | BOOLEAN | NO | Is feed halal |
| halal_flag_reason | TEXT | YES | Reason if flagged |
| recorded_by | BIGINT | NO | FK → users |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | farm_id | feed_date | feed_type | brand | supplier | quantity_kg | is_halal | halal_flag_reason |
|----|---------|-----------|-----------|-------|----------|-------------|----------|-------------------|
| 1 | 1 | 2025-01-15 | Commercial Feed | B-Meg Goat Grower | San Miguel Foods | 50.00 | Yes | - |
| 2 | 1 | 2025-01-15 | Roughage | Natural Grass | Own farm | 100.00 | Yes | - |
| 3 | 2 | 2025-01-16 | Concentrate | Unknown Brand | Local market | 25.00 | No | Contains animal by-products |
| 4 | 1 | 2025-01-20 | Molasses | Molasses Mix | Coop | 30.00 | Yes | - |

---

## inflows

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| farm_id | BIGINT | NO | FK → farms |
| inflow_type | ENUM('goat_purchase','goat_birth','feed','biologics','other') | NO | Type |
| inflow_date | DATE | NO | Date |
| goat_id | BIGINT | YES | FK → goats (if goat) |
| source | VARCHAR(100) | YES | Source |
| quantity | INT | YES | Quantity |
| description | TEXT | YES | Description |
| recorded_by | BIGINT | NO | FK → users |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | farm_id | inflow_type | inflow_date | goat_id | source | quantity | description |
|----|---------|-------------|-------------|---------|--------|----------|-------------|
| 1 | 1 | goat_birth | 2025-01-10 | 3 | Own farm | 1 | Kid born from Doe #2 |
| 2 | 1 | goat_purchase | 2025-01-05 | 4 | Kiamba Market | 1 | Purchased grower male |
| 3 | 1 | feed | 2025-01-15 | - | San Miguel Foods | 50 | Monthly feed supply |
| 4 | 1 | biologics | 2025-01-10 | - | Veterinary Clinic | 10 | Vaccines and dewormers |

---

## outflows

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| farm_id | BIGINT | NO | FK → farms |
| outflow_type | ENUM('sale','slaughter','death','transfer') | NO | Type |
| outflow_date | DATE | NO | Date |
| goat_id | BIGINT | NO | FK → goats |
| destination | VARCHAR(100) | YES | Destination |
| slaughterhouse_id | BIGINT | YES | FK → slaughterhouses |
| quantity | INT | NO | Quantity |
| price | DECIMAL(10,2) | YES | Sale price |
| death_cause | TEXT | YES | Cause of death |
| notes | TEXT | YES | Notes |
| recorded_by | BIGINT | NO | FK → users |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | farm_id | outflow_type | outflow_date | goat_id | destination | slaughterhouse_id | price | death_cause |
|----|---------|--------------|--------------|---------|-------------|-------------------|-------|-------------|
| 1 | 1 | slaughter | 2025-01-28 | 6 | Maasim Halal Slaughterhouse | 1 | 8500.00 | - |
| 2 | 1 | sale | 2025-01-20 | 7 | Local buyer - Mr. Ramos | - | 6000.00 | - |
| 3 | 2 | death | 2025-01-18 | 8 | - | - | - | Pneumonia |
