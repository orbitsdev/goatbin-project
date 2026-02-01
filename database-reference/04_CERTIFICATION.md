# Certification Tables

---

## certification_applications

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| application_code | VARCHAR(20) | NO | Unique code |
| farm_id | BIGINT | NO | FK → farms |
| applicant_id | BIGINT | NO | FK → users |
| application_date | DATE | NO | Application date |
| application_type | ENUM('new','renewal') | NO | Type |
| status | ENUM('pending','under_review','approved','rejected','cancelled') | NO | Status |
| documents | JSON | YES | Uploaded documents |
| notes | TEXT | YES | Applicant notes |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | application_code | farm_id | applicant_id | application_date | application_type | status | notes |
|----|------------------|---------|--------------|------------------|------------------|--------|-------|
| 1 | HGC-APP-2024-001 | 1 | 1 | 2024-12-01 | new | approved | First time application |
| 2 | HGC-APP-2025-001 | 2 | 2 | 2025-01-15 | new | under_review | Requesting halal certification |
| 3 | HGC-APP-2025-002 | 3 | 6 | 2025-01-28 | new | pending | New farm registration |
| 4 | HGC-APP-2025-003 | 1 | 1 | 2025-12-01 | renewal | pending | Annual renewal |

---

## certification_reviews

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| application_id | BIGINT | NO | FK → certification_applications |
| reviewer_id | BIGINT | NO | FK → users |
| review_date | DATE | NO | Review date |
| compliance_score | DECIMAL(5,2) | NO | Compliance % |
| review_notes | TEXT | YES | Review notes |
| recommendation | ENUM('approve','reject','need_info') | NO | Recommendation |
| recommendation_notes | TEXT | YES | Recommendation notes |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | application_id | reviewer_id | review_date | compliance_score | recommendation | review_notes |
|----|----------------|-------------|-------------|------------------|----------------|--------------|
| 1 | 1 | 3 | 2024-12-15 | 95.00 | approve | Farm meets all halal requirements. Feed sources verified. Distance from haram facilities is adequate. |
| 2 | 2 | 3 | 2025-01-20 | 75.00 | need_info | Need clarification on feed sources. Some feed records show unknown brands. |
| 3 | 2 | 3 | 2025-01-25 | 92.00 | approve | Feed sources clarified and verified. Approved for certification. |

---

## certifications

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| certificate_code | VARCHAR(20) | NO | Unique code |
| farm_id | BIGINT | NO | FK → farms |
| application_id | BIGINT | NO | FK → certification_applications |
| issued_date | DATE | NO | Issue date |
| expiry_date | DATE | NO | Expiry date |
| status | ENUM('active','expired','suspended','revoked') | NO | Status |
| issued_by | BIGINT | NO | FK → users |
| suspension_reason | TEXT | YES | Suspension reason |
| suspension_date | DATE | YES | Suspension date |
| revocation_reason | TEXT | YES | Revocation reason |
| revocation_date | DATE | YES | Revocation date |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | certificate_code | farm_id | application_id | issued_date | expiry_date | status | issued_by |
|----|------------------|---------|----------------|-------------|-------------|--------|-----------|
| 1 | HGC-CERT-2025-001 | 1 | 1 | 2025-01-01 | 2026-01-01 | active | 3 |
| 2 | HGC-CERT-2025-002 | 2 | 2 | 2025-01-26 | 2026-01-26 | active | 3 |

**Example of Suspended Certification:**

| id | certificate_code | farm_id | status | suspension_reason | suspension_date |
|----|------------------|---------|--------|-------------------|-----------------|
| 3 | HGC-CERT-2024-005 | 5 | suspended | Multiple non-halal feed violations detected | 2025-01-15 |
