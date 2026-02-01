# Traceability Tables

---

## transports

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| transport_code | VARCHAR(20) | NO | Unique code |
| outflow_id | BIGINT | NO | FK → outflows |
| farm_id | BIGINT | NO | FK → farms (source) |
| slaughterhouse_id | BIGINT | NO | FK → slaughterhouses |
| transport_date | DATE | NO | Date |
| vehicle_info | VARCHAR(100) | YES | Vehicle details |
| driver_name | VARCHAR(100) | YES | Driver name |
| goat_count | INT | NO | Number of goats |
| status | ENUM('pending','in_transit','arrived','cancelled') | NO | Status |
| arrival_date | DATETIME | YES | Arrival date/time |
| arrival_confirmed_by | BIGINT | YES | FK → users |
| notes | TEXT | YES | Notes |
| recorded_by | BIGINT | NO | FK → users |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | transport_code | outflow_id | farm_id | slaughterhouse_id | transport_date | vehicle_info | driver_name | goat_count | status | arrival_date |
|----|----------------|------------|---------|-------------------|----------------|--------------|-------------|------------|--------|--------------|
| 1 | HGT-2025-00001 | 1 | 1 | 1 | 2025-01-28 | Toyota Hilux ABC-1234 | Mario Cruz | 1 | arrived | 2025-01-28 08:30:00 |
| 2 | HGT-2025-00002 | 4 | 2 | 2 | 2025-01-29 | Isuzu ELF XYZ-5678 | Pedro Santos | 3 | in_transit | - |

---

## slaughter_records

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| slaughter_code | VARCHAR(20) | NO | Unique code |
| slaughterhouse_id | BIGINT | NO | FK → slaughterhouses |
| goat_id | BIGINT | NO | FK → goats |
| farm_id | BIGINT | NO | FK → farms (source) |
| transport_id | BIGINT | YES | FK → transports |
| slaughter_date | DATE | NO | Date |
| slaughter_time | TIME | NO | Time |
| slaughterer_name | VARCHAR(100) | NO | Halal slaughterer name |
| live_weight_kg | DECIMAL(10,2) | NO | Weight before |
| carcass_weight_kg | DECIMAL(10,2) | NO | Carcass weight |
| offal_weight_kg | DECIMAL(10,2) | YES | Offal weight |
| meat_cuts | JSON | YES | Types of cuts |
| is_halal_verified | BOOLEAN | NO | Halal verified |
| verification_notes | TEXT | YES | Notes |
| status | ENUM('pending','approved','rejected') | NO | Status |
| approved_by | BIGINT | YES | FK → users |
| approved_at | DATETIME | YES | Approval time |
| recorded_by | BIGINT | NO | FK → users |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | slaughter_code | slaughterhouse_id | goat_id | farm_id | slaughter_date | slaughter_time | slaughterer_name | live_weight_kg | carcass_weight_kg | is_halal_verified | status |
|----|----------------|-------------------|---------|---------|----------------|----------------|------------------|----------------|-------------------|-------------------|--------|
| 1 | HGS-2025-00001 | 1 | 6 | 1 | 2025-01-28 | 09:00:00 | Ustadz Ibrahim | 45.00 | 22.50 | Yes | approved |
| 2 | HGS-2025-00002 | 2 | 9 | 2 | 2025-01-29 | 10:30:00 | Ustadz Ahmad | 38.00 | 19.00 | Yes | pending |

---

## qr_codes

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| qr_code | VARCHAR(20) | NO | Unique QR code |
| slaughter_record_id | BIGINT | NO | FK → slaughter_records |
| goat_id | BIGINT | NO | FK → goats |
| farm_id | BIGINT | NO | FK → farms |
| product_type | VARCHAR(50) | NO | Product type |
| weight_kg | DECIMAL(10,2) | NO | Product weight |
| qr_data | JSON | NO | Full QR data |
| blockchain_hash | VARCHAR(100) | YES | Blockchain hash |
| generated_at | DATETIME | NO | Generation time |
| generated_by | BIGINT | NO | FK → users |
| scan_count | INT | NO | Times scanned |
| last_scanned_at | DATETIME | YES | Last scan time |
| status | ENUM('active','revoked') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | qr_code | slaughter_record_id | goat_id | farm_id | product_type | weight_kg | scan_count | status |
|----|---------|---------------------|---------|---------|--------------|-----------|------------|--------|
| 1 | HGBP-2025-00001 | 1 | 6 | 1 | Chevon (whole carcass) | 22.50 | 3 | active |
| 2 | HGBP-2025-00002 | 2 | 9 | 2 | Chevon (whole carcass) | 19.00 | 0 | active |

**QR Data JSON Example:**

```json
{
  "qr_code": "HGBP-2025-00001",
  "goat_code": "HGG-2025-00006",
  "farm": {
    "code": "HGF-0001",
    "name": "Dela Cruz Goat Farm",
    "location": "Tinoto, Maasim, Sarangani",
    "certified": true,
    "certificate": "HGC-CERT-2025-001"
  },
  "goat": {
    "breed": "Boer",
    "breed_type": "Pure",
    "gender": "male",
    "age_months": 19,
    "production_type": "For Slaughter"
  },
  "slaughter": {
    "date": "2025-01-28",
    "slaughterhouse": "Maasim Halal Slaughterhouse",
    "slaughterer": "Ustadz Ibrahim",
    "halal_verified": true
  },
  "product": {
    "type": "Chevon (whole carcass)",
    "weight_kg": 22.50
  },
  "verification_url": "https://halalgoatbin.ph/verify/HGBP-2025-00001"
}
```

---

## blockchain_logs

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| transaction_hash | VARCHAR(100) | NO | Blockchain hash |
| transaction_type | VARCHAR(50) | NO | Transaction type |
| entity_type | VARCHAR(50) | NO | Entity type |
| entity_id | BIGINT | NO | Entity ID |
| data | JSON | NO | Transaction data |
| timestamp | DATETIME | NO | Transaction time |
| created_at | TIMESTAMP | NO | Record created |

**Sample Data:**

| id | transaction_hash | transaction_type | entity_type | entity_id | timestamp |
|----|------------------|------------------|-------------|-----------|-----------|
| 1 | 0x7f9e8d7c6b5a4... | goat_registered | goat | 6 | 2023-06-15 08:00:00 |
| 2 | 0x1a2b3c4d5e6f7... | slaughter_recorded | slaughter_record | 1 | 2025-01-28 09:30:00 |
| 3 | 0x9f8e7d6c5b4a3... | qr_generated | qr_code | 1 | 2025-01-28 10:00:00 |
| 4 | 0x2b3c4d5e6f7a8... | certification_issued | certification | 1 | 2025-01-01 10:00:00 |
