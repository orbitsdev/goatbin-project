# System Tables

---

## audit_logs

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| user_id | BIGINT | YES | FK → users |
| action | VARCHAR(50) | NO | Action performed |
| entity_type | VARCHAR(50) | NO | Entity type |
| entity_id | BIGINT | NO | Entity ID |
| old_values | JSON | YES | Old values |
| new_values | JSON | YES | New values |
| ip_address | VARCHAR(45) | YES | IP address |
| user_agent | VARCHAR(255) | YES | Browser/device |
| created_at | TIMESTAMP | NO | Record created |

**Sample Data:**

| id | user_id | action | entity_type | entity_id | ip_address | created_at |
|----|---------|--------|-------------|-----------|------------|------------|
| 1 | 1 | create | goat | 3 | 192.168.1.100 | 2025-01-10 08:30:00 |
| 2 | 3 | update | certification | 1 | 192.168.1.50 | 2025-01-01 10:00:00 |
| 3 | 1 | create | feed_record | 1 | 192.168.1.100 | 2025-01-15 14:20:00 |
| 4 | 1 | update | goat | 6 | 192.168.1.100 | 2025-01-28 09:45:00 |
| 5 | 2 | delete | feed_record | 5 | 192.168.1.105 | 2025-01-20 11:30:00 |

**JSON Examples:**

**old_values (for update action):**
```json
{
  "status": "pending",
  "compliance_score": null
}
```

**new_values (for update action):**
```json
{
  "status": "active",
  "compliance_score": 95.00,
  "issued_date": "2025-01-01"
}
```

**new_values (for create action):**
```json
{
  "goat_code": "HGG-2025-00003",
  "farm_id": 1,
  "breed_id": 1,
  "gender": "female",
  "birth_date": "2025-01-10",
  "status": "active"
}
```

---

## notifications

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| user_id | BIGINT | NO | FK → users |
| type | VARCHAR(50) | NO | Notification type |
| title | VARCHAR(100) | NO | Title |
| message | TEXT | NO | Message |
| data | JSON | YES | Additional data |
| read_at | DATETIME | YES | When read |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | user_id | type | title | message | read_at | created_at |
|----|---------|------|-------|---------|---------|------------|
| 1 | 1 | certification | Certification Approved | Congratulations! Your farm HGF-0001 has been certified as Halal compliant. | 2025-01-01 12:00:00 | 2025-01-01 10:30:00 |
| 2 | 2 | warning | Compliance Warning | Non-halal feed detected in your feed records. Please review and update. | null | 2025-01-16 08:00:00 |
| 3 | 1 | reminder | Vaccination Due | Goat HGG-2025-00001 PPR vaccine is due in 30 days (June 15, 2025). | null | 2025-05-15 08:00:00 |
| 4 | 2 | review | Application Under Review | Your certification application HGC-APP-2025-001 is being reviewed by NCMF. | 2025-01-20 09:00:00 | 2025-01-18 14:00:00 |
| 5 | 1 | system | System Maintenance | System will undergo maintenance on Feb 5, 2025 from 12AM-4AM. | null | 2025-02-01 08:00:00 |

**Notification Types:**

| Type | Description |
|------|-------------|
| certification | Certification status updates |
| warning | Compliance warnings |
| reminder | Due dates and reminders |
| review | Application review status |
| system | System announcements |
| alert | Urgent alerts |

---

## settings

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| key | VARCHAR(100) | NO | Setting key |
| value | TEXT | NO | Setting value |
| type | ENUM('string','number','boolean','json') | NO | Value type |
| description | TEXT | YES | Description |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | key | value | type | description |
|----|-----|-------|------|-------------|
| 1 | min_haram_distance_km | 1.0 | number | Minimum distance from haram facilities in kilometers |
| 2 | certification_validity_days | 365 | number | Certification validity period in days |
| 3 | auto_compliance_check | true | boolean | Enable automatic daily compliance checking |
| 4 | goat_code_prefix | HGG | string | Prefix for goat codes |
| 5 | farm_code_prefix | HGF | string | Prefix for farm codes |
| 6 | qr_code_prefix | HGBP | string | Prefix for QR product codes |
| 7 | transport_code_prefix | HGT | string | Prefix for transport codes |
| 8 | slaughter_code_prefix | HGS | string | Prefix for slaughter codes |
| 9 | vaccination_reminder_days | 30 | number | Days before vaccination due date to send reminder |
| 10 | certification_expiry_reminder_days | 60 | number | Days before cert expiry to send reminder |

**Settings by Category:**

**Distance & Compliance:**
| key | value | description |
|-----|-------|-------------|
| min_haram_distance_km | 1.0 | Minimum distance from haram facilities |
| auto_compliance_check | true | Enable auto compliance checks |
| compliance_check_frequency | daily | How often to run auto checks |

**Code Prefixes:**
| key | value | description |
|-----|-------|-------------|
| goat_code_prefix | HGG | Goat code prefix |
| farm_code_prefix | HGF | Farm code prefix |
| qr_code_prefix | HGBP | QR product code prefix |
| transport_code_prefix | HGT | Transport code prefix |
| slaughter_code_prefix | HGS | Slaughter code prefix |
| certificate_code_prefix | HGC-CERT | Certificate code prefix |
| application_code_prefix | HGC-APP | Application code prefix |

**Reminders & Notifications:**
| key | value | description |
|-----|-------|-------------|
| vaccination_reminder_days | 30 | Days before vaccination due |
| certification_expiry_reminder_days | 60 | Days before cert expiry |
| compliance_warning_threshold | 80 | Score below this triggers warning |

**Certification:**
| key | value | description |
|-----|-------|-------------|
| certification_validity_days | 365 | Certificate valid for 1 year |
| renewal_window_days | 30 | Can renew within 30 days of expiry |
