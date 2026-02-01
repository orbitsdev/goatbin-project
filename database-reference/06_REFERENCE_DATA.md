# Reference Data Tables

---

## breeds

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(50) | NO | Breed name |
| description | TEXT | YES | Description |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | description | status |
|----|------|-------------|--------|
| 1 | Boer | South African meat breed, fast growth, excellent meat quality | active |
| 2 | Anglo-Nubian | Dual-purpose breed for milk and meat, long ears | active |
| 3 | Saanen | Swiss dairy breed, highest milk production | active |
| 4 | Alpine | French dairy breed, good milk production | active |
| 5 | Native | Philippine indigenous breed, hardy and disease resistant | active |
| 6 | Boer Cross | Boer crossed with native, combines traits | active |

---

## breed_types

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(50) | NO | Breed type name |
| code | VARCHAR(10) | NO | Short code |
| description | TEXT | YES | Description |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | code | description | status |
|----|------|------|-------------|--------|
| 1 | Native | NAT | Local/indigenous Philippine breed | active |
| 2 | Upgrade | UPG | Native crossed with improved breed (25-75% foreign blood) | active |
| 3 | Cross | CRS | Mixed breeds (50-50 or varied) | active |
| 4 | Pure | PUR | Purebred (100% single breed, registered) | active |

---

## production_types

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(50) | NO | Production type |
| description | TEXT | YES | Description |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | description | status |
|----|------|-------------|--------|
| 1 | For Breeding | Goat kept to produce offspring (bucks and does) | active |
| 2 | For Slaughter | Goat raised for meat (chevon) | active |
| 3 | For Dairy | Goat raised for milk production | active |

---

## age_classes

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(50) | NO | Age class name |
| code | VARCHAR(10) | NO | Short code |
| min_age_days | INT | NO | Min age in days |
| max_age_days | INT | YES | Max age (null = no max) |
| gender | ENUM('male','female','both') | NO | Applicable gender |
| description | TEXT | YES | Description |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | code | min_age_days | max_age_days | gender | description | status |
|----|------|------|--------------|--------------|--------|-------------|--------|
| 1 | Kid | KID | 0 | 30 | both | Newborn baby goat, less than 1 month | active |
| 2 | Kids | KIDS | 31 | 90 | both | Young goat, 1-3 months old | active |
| 3 | Grower | GRW | 91 | 240 | both | Growing/teenager goat, 3-8 months | active |
| 4 | Buck | BUCK | 241 | null | male | Adult male goat, 8+ months | active |
| 5 | Doe | DOE | 241 | null | female | Adult female goat, 8+ months | active |

---

## breeding_statuses

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(50) | NO | Status name |
| code | VARCHAR(10) | NO | Short code |
| applicable_gender | ENUM('male','female') | NO | Gender |
| description | TEXT | YES | Description |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | code | applicable_gender | description | status |
|----|------|------|-------------------|-------------|--------|
| 1 | Doeling | DLG | female | Young female goat, never been bred | active |
| 2 | Dry Does | DRY | female | Adult female, not pregnant and not lactating | active |
| 3 | Pregnant | PRG | female | Female currently carrying baby (gestation ~150 days) | active |
| 4 | Lactating | LAC | female | Female currently producing milk | active |
| 5 | Buck | BCK | male | Male goat used for breeding | active |

---

## feed_types

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(50) | NO | Feed type name |
| description | TEXT | YES | Description |
| default_halal_status | BOOLEAN | NO | Default halal |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | description | default_halal_status | status |
|----|------|-------------|----------------------|--------|
| 1 | Commercial Feed | Processed commercial goat feed pellets | Yes | active |
| 2 | Roughage | Grass, hay, straw, natural vegetation | Yes | active |
| 3 | Concentrate | High-protein supplements (check ingredients) | No | active |
| 4 | Molasses | Sugar cane by-product, energy source | Yes | active |
| 5 | Legumes | Ipil-ipil, kakawate, flemengia leaves | Yes | active |
| 6 | Farm By-products | Rice straw, corn stover, peanut hay | Yes | active |

---

## medicine_types

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(100) | NO | Medicine name |
| brand | VARCHAR(100) | YES | Brand |
| is_halal_certified | BOOLEAN | NO | Halal certified |
| halal_certificate | VARCHAR(255) | YES | Certificate file |
| description | TEXT | YES | Description |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | brand | is_halal_certified | description | status |
|----|------|-------|--------------------| -------------|--------|
| 1 | Ivermectin | Ivomec | Yes | Dewormer for internal and external parasites | active |
| 2 | Electrolytes | Vet-Lyte | Yes | Oral rehydration solution for diarrhea | active |
| 3 | Zinc Sulfate | ZincSpray | Yes | Topical spray for foot rot treatment | active |
| 4 | Oxytetracycline | Terramycin | Yes | Broad-spectrum antibiotic | active |
| 5 | Albendazole | Valbazen | Yes | Dewormer for internal parasites | active |
| 6 | Penicillin | Pen-Strep | Yes | Antibiotic for bacterial infections | active |

---

## illness_types

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(50) | NO | Illness name |
| description | TEXT | YES | Description |
| severity | ENUM('low','medium','high','critical') | NO | Severity |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | description | severity | status |
|----|------|-------------|----------|--------|
| 1 | Parasites | Internal (worms) or external (lice, ticks) parasites | medium | active |
| 2 | Diarrhea | Bacterial, viral, or dietary diarrhea | medium | active |
| 3 | Foot Rot | Bacterial infection of hooves, causes lameness | medium | active |
| 4 | Pneumonia | Respiratory infection, can be fatal | high | active |
| 5 | PPR | Peste des Petits Ruminants, highly contagious viral disease | critical | active |
| 6 | Bloat | Gas accumulation in rumen, emergency condition | high | active |
| 7 | Mastitis | Udder infection in lactating does | medium | active |
| 8 | Enterotoxemia | Overeating disease, caused by Clostridium bacteria | high | active |

---

## provinces

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(100) | NO | Province name |
| region | VARCHAR(50) | NO | Region |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | region | status |
|----|------|--------|--------|
| 1 | Sarangani | Region XII (SOCCSKSARGEN) | active |
| 2 | South Cotabato | Region XII (SOCCSKSARGEN) | active |
| 3 | Sultan Kudarat | Region XII (SOCCSKSARGEN) | active |
| 4 | Cotabato | Region XII (SOCCSKSARGEN) | active |

---

## municipalities

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| province_id | BIGINT | NO | FK → provinces |
| name | VARCHAR(100) | NO | Municipality name |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | province_id | province | name | status |
|----|-------------|----------|------|--------|
| 1 | 1 | Sarangani | Maasim | active |
| 2 | 1 | Sarangani | Kiamba | active |
| 3 | 1 | Sarangani | Maitum | active |
| 4 | 2 | South Cotabato | Lake Sebu | active |
| 5 | 2 | South Cotabato | Surallah | active |
| 6 | 2 | South Cotabato | Sto. Nino | active |
| 7 | 3 | Sultan Kudarat | Isulan | active |
| 8 | 3 | Sultan Kudarat | Tacurong | active |
| 9 | 3 | Sultan Kudarat | Pres. Quirino | active |

---

## barangays

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| municipality_id | BIGINT | NO | FK → municipalities |
| name | VARCHAR(100) | NO | Barangay name |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | municipality_id | municipality | name | status |
|----|-----------------|--------------|------|--------|
| 1 | 1 | Maasim | Tinoto | active |
| 2 | 1 | Maasim | Kamanga | active |
| 3 | 1 | Maasim | Poblacion | active |
| 4 | 2 | Kiamba | Lamian | active |
| 5 | 2 | Kiamba | Poblacion | active |
| 6 | 4 | Lake Sebu | Ned | active |
| 7 | 4 | Lake Sebu | Poblacion | active |
| 8 | 4 | Lake Sebu | Lamfugon | active |

---

## slaughterhouses

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| code | VARCHAR(20) | NO | Unique code |
| name | VARCHAR(100) | NO | Slaughterhouse name |
| address | TEXT | YES | Address |
| municipality_id | BIGINT | NO | FK → municipalities |
| latitude | DECIMAL(10,8) | YES | GPS latitude |
| longitude | DECIMAL(11,8) | YES | GPS longitude |
| contact_person | VARCHAR(100) | YES | Contact person |
| contact_phone | VARCHAR(20) | YES | Phone |
| is_halal_certified | BOOLEAN | NO | Halal certified |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | code | name | municipality | contact_person | contact_phone | is_halal_certified | status |
|----|------|------|--------------|----------------|---------------|--------------------| -------|
| 1 | SH-001 | Maasim Halal Slaughterhouse | Maasim | Ibrahim Santos | 09171112222 | Yes | active |
| 2 | SH-002 | Kiamba Public Slaughterhouse | Kiamba | Omar Hassan | 09181113333 | Yes | active |
| 3 | SH-003 | Lake Sebu Slaughterhouse | Lake Sebu | Pending | - | No | active |
| 4 | SH-004 | Surallah Halal Facility | Surallah | Ahmad Malik | 09191114444 | Yes | active |

---

## haram_facilities

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | BIGINT | NO | Primary Key |
| name | VARCHAR(100) | NO | Facility name |
| type | ENUM('pig_farm','non_halal_slaughterhouse','other') | NO | Type |
| address | TEXT | YES | Address |
| municipality_id | BIGINT | NO | FK → municipalities |
| latitude | DECIMAL(10,8) | NO | GPS latitude |
| longitude | DECIMAL(11,8) | NO | GPS longitude |
| status | ENUM('active','inactive') | NO | Status |
| created_at | TIMESTAMP | NO | Record created |
| updated_at | TIMESTAMP | NO | Record updated |

**Sample Data:**

| id | name | type | municipality | latitude | longitude | status |
|----|------|------|--------------|----------|-----------|--------|
| 1 | ABC Piggery | pig_farm | Maasim | 5.852100 | 125.014700 | active |
| 2 | XYZ Hog Farm | pig_farm | Kiamba | 5.983200 | 124.621400 | active |
| 3 | DEF Piggery | pig_farm | Lake Sebu | 6.112300 | 124.756800 | active |
| 4 | GHI Pig Farm | pig_farm | Surallah | 6.234500 | 124.889100 | active |
| 5 | Municipal Slaughterhouse (Non-Halal) | non_halal_slaughterhouse | Tacurong | 6.456700 | 124.678900 | active |
