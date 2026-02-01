# User Management Tables

---

## users

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(100) | NO | Full name |
| email | VARCHAR(100) | NO | Email (unique) |
| password | VARCHAR(255) | NO | Hashed password |
| phone | VARCHAR(20) | YES | Phone number |
| address | TEXT | YES | Address |
| photo | VARCHAR(255) | YES | Profile photo path |
| status | ENUM('active','inactive') | NO | Account status |
| email_verified_at | TIMESTAMP | YES | Email verification date |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | email | phone | status |
|----|------|-------|-------|--------|
| 1 | Juan Dela Cruz | juan@email.com | 09171234567 | active |
| 2 | Maria Santos | maria@email.com | 09181234567 | active |
| 3 | Ahmed Abdullah | ahmed@ncmf.gov.ph | 09191234567 | active |
| 4 | Pedro Reyes | pedro@lgu-maasim.gov.ph | 09201234567 | active |
| 5 | Ali Hassan | ali@da.gov.ph | 09211234567 | active |

---

## roles

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(50) | NO | Role name (system) |
| display_name | VARCHAR(100) | NO | Display name |
| description | TEXT | YES | Role description |
| level | ENUM('super','head','staff','public') | NO | Access level |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | display_name | level |
|----|------|--------------|-------|
| 1 | admin | System Admin | super |
| 2 | farm_owner | Farm Owner | head |
| 3 | farm_worker | Farm Worker | staff |
| 4 | slaughterhouse_head | Slaughterhouse Head | head |
| 5 | slaughterhouse_staff | Slaughterhouse Staff | staff |
| 6 | certifier_head | Certifier Head (NCMF) | head |
| 7 | certifier_staff | Certifier Staff | staff |
| 8 | lgu_head | LGU Head | head |
| 9 | lgu_staff | LGU Staff | staff |
| 10 | da_head | DA Head | head |
| 11 | da_staff | DA Staff | staff |
| 12 | consumer | Consumer | public |

---

## user_roles

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| user_id | BIGINT | NO | FK → users |
| role_id | BIGINT | NO | FK → roles |
| entity_type | ENUM('farm','slaughterhouse','lgu','da','certifier') | YES | Entity type |
| entity_id | BIGINT | YES | Entity ID |
| created_at | TIMESTAMP | NO | Record created |

**Sample Data:**

| id | user_id | role_id | entity_type | entity_id |
|----|---------|---------|-------------|-----------|
| 1 | 1 | 2 | farm | 1 |
| 2 | 2 | 2 | farm | 2 |
| 3 | 3 | 6 | certifier | 1 |
| 4 | 4 | 9 | lgu | 1 |
| 5 | 5 | 11 | da | 1 |
