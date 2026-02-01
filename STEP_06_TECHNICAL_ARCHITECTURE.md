# 📋 HALAL GOAT BIN PROJECT - DOCUMENTATION

## PROJECT KICKOFF MEETING

**Project:** Halal GOAT Bin: A Geographically-Oriented Application and Traceability System  
**Date:** February 1, 2026  
**Document:** Step 6 - Technical Architecture  
**Status:** COMPLETE (Level 1 High-Level Overview)

---

# STEP 6: TECHNICAL ARCHITECTURE

## 1. Overview

This document defines the technical architecture — the technologies, tools, structure, and how components connect together.

---

## 2. Technology Stack

### 2.1 Final Technology Choices

| Layer | Technology | Version | Notes |
|-------|------------|---------|-------|
| **Frontend (Web)** | Nuxt 3 | Latest | Vue 3 based, SSR/CSR |
| **Backend API** | Laravel | 12 | PHP Framework, API only |
| **Mobile App** | Flutter | Latest | Dart language |
| **Authentication** | Laravel Sanctum | Latest | Token-based API auth |
| **Database** | PostgreSQL | 16+ | Better rollback, data integrity |
| **Cache** | Redis | Latest | Optional, for performance |
| **Blockchain** | TBD | - | Hyperledger / Polygon / Simple Hash |
| **GIS/Maps** | TBD | - | OpenStreetMap + Leaflet / Google Maps |
| **SMS Gateway** | TBD | - | Semaphore / Twilio |
| **Hosting** | AWS / DigitalOcean | - | Scalable, maintainable |

### 2.2 Why This Stack?

| Choice | Reason |
|--------|--------|
| **Nuxt 3 + Laravel API** | Faster — frontend fetches only JSON data needed |
| **Separate Frontend/Backend** | Same API serves both Web (Nuxt) and Mobile (Flutter) |
| **Laravel Sanctum** | Simple token-based auth for API |
| **PostgreSQL** | Better data integrity, rollback support |
| **Laravel 12** | Latest version, modern features |

---

## 3. System Architecture

### 3.1 High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                                                                 │
│                           HALAL GOAT BIN SYSTEM                                 │
│                                                                                 │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│   USERS                                                                         │
│   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐             │
│   │  Farm   │  │Slaughter│  │Certifier│  │ LGU/DA  │  │Consumer │             │
│   │  Owner  │  │  house  │  │ (NCMF)  │  │  Staff  │  │(Mobile) │             │
│   └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘             │
│        │            │            │            │            │                   │
│        └────────────┴─────┬──────┴────────────┘            │                   │
│                           │                                │                   │
│                      Web Browser                      Mobile App               │
│                           │                                │                   │
│                           ▼                                ▼                   │
│   ┌─────────────────────────────────────────────────────────────────────────┐  │
│   │                         FRONTEND LAYER                                  │  │
│   │                                                                         │  │
│   │   ┌─────────────────────────────┐    ┌─────────────────────────────┐   │  │
│   │   │      NUXT 3 (Vue 3)         │    │         FLUTTER             │   │  │
│   │   │      (Web Frontend)         │    │      (Mobile App)           │   │  │
│   │   │                             │    │                             │   │  │
│   │   │   • Server-Side Rendering   │    │   • QR Code Scanner         │   │  │
│   │   │   • Client-Side Rendering   │    │   • Product Verification    │   │  │
│   │   │   • All Web Features        │    │   • Offline Support         │   │  │
│   │   │                             │    │                             │   │  │
│   │   └──────────────┬──────────────┘    └──────────────┬──────────────┘   │  │
│   │                  │                                  │                   │  │
│   └──────────────────┼──────────────────────────────────┼───────────────────┘  │
│                      │                                  │                      │
│                      │         REST API                 │                      │
│                      │      (Sanctum Auth)              │                      │
│                      │                                  │                      │
│                      └─────────────┬────────────────────┘                      │
│                                    │                                           │
│                                    ▼                                           │
│   ┌─────────────────────────────────────────────────────────────────────────┐  │
│   │                         BACKEND LAYER                                   │  │
│   │                                                                         │  │
│   │                    ┌─────────────────────────┐                          │  │
│   │                    │                         │                          │  │
│   │                    │    LARAVEL 12 API       │                          │  │
│   │                    │                         │                          │  │
│   │                    │  • RESTful API          │                          │  │
│   │                    │  • Sanctum Auth         │                          │  │
│   │                    │  • Controllers          │                          │  │
│   │                    │  • Services             │                          │  │
│   │                    │  • Models               │                          │  │
│   │                    │                         │                          │  │
│   │                    └───────────┬─────────────┘                          │  │
│   │                                │                                        │  │
│   └────────────────────────────────┼────────────────────────────────────────┘  │
│                                    │                                           │
│                                    ▼                                           │
│   ┌─────────────────────────────────────────────────────────────────────────┐  │
│   │                          DATA LAYER                                     │  │
│   │                                                                         │  │
│   │   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐                  │  │
│   │   │             │   │             │   │             │                  │  │
│   │   │ PostgreSQL  │   │ Blockchain  │   │   Redis     │                  │  │
│   │   │  Database   │   │   Ledger    │   │   Cache     │                  │  │
│   │   │             │   │             │   │  (Optional) │                  │  │
│   │   └─────────────┘   └─────────────┘   └─────────────┘                  │  │
│   │                                                                         │  │
│   └─────────────────────────────────────────────────────────────────────────┘  │
│                                                                                 │
│   ┌─────────────────────────────────────────────────────────────────────────┐  │
│   │                      THIRD-PARTY SERVICES                               │  │
│   │                                                                         │  │
│   │   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐                  │  │
│   │   │             │   │             │   │             │                  │  │
│   │   │  GIS/Maps   │   │ SMS Gateway │   │   Email     │                  │  │
│   │   │  (Leaflet/  │   │ (Semaphore/ │   │  (SMTP/     │                  │  │
│   │   │   Google)   │   │   Twilio)   │   │  Mailgun)   │                  │  │
│   │   │             │   │             │   │             │                  │  │
│   │   └─────────────┘   └─────────────┘   └─────────────┘                  │  │
│   │                                                                         │  │
│   └─────────────────────────────────────────────────────────────────────────┘  │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 API-Centric Architecture

```
SAME API — MULTIPLE CLIENTS

┌───────────────────┐                    ┌───────────────────┐
│                   │                    │                   │
│   NUXT 3 (Web)    │                    │ FLUTTER (Mobile)  │
│                   │                    │                   │
│   • Farm Mgmt     │                    │   • QR Scanner    │
│   • Traceability  │                    │   • Verification  │
│   • Certification │                    │   • View Info     │
│   • Reports       │                    │                   │
│   • Admin         │                    │                   │
│                   │                    │                   │
└─────────┬─────────┘                    └─────────┬─────────┘
          │                                        │
          │  REST API + Sanctum Token              │
          │                                        │
          └────────────────┬───────────────────────┘
                           │
                           ▼
                 ┌───────────────────┐
                 │                   │
                 │  LARAVEL 12 API   │
                 │                   │
                 │  SAME endpoints   │
                 │  SAME responses   │
                 │  SAME auth        │
                 │                   │
                 └─────────┬─────────┘
                           │
                           ▼
                 ┌───────────────────┐
                 │                   │
                 │    PostgreSQL     │
                 │    + Blockchain   │
                 │                   │
                 └───────────────────┘
```

---

## 4. Project Structure

### 4.1 Overview — Three Separate Projects

```
halal-goat-bin/
│
├── halal-goat-bin-api/          # Laravel 12 API (Backend)
│
├── halal-goat-bin-web/          # Nuxt 3 (Web Frontend)
│
└── halal-goat-bin-mobile/       # Flutter (Mobile App)
```

### 4.2 Backend: Laravel 12 API

```
halal-goat-bin-api/
│
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Auth/
│   │   │   │   ├── LoginController.php
│   │   │   │   ├── RegisterController.php
│   │   │   │   └── LogoutController.php
│   │   │   │
│   │   │   ├── Farm/
│   │   │   │   ├── FarmController.php
│   │   │   │   └── FarmWorkerController.php
│   │   │   │
│   │   │   ├── Goat/
│   │   │   │   ├── GoatController.php
│   │   │   │   ├── HealthRecordController.php
│   │   │   │   ├── VaccinationController.php
│   │   │   │   └── FeedRecordController.php
│   │   │   │
│   │   │   ├── Traceability/
│   │   │   │   ├── TransportController.php
│   │   │   │   ├── SlaughterController.php
│   │   │   │   └── QRCodeController.php
│   │   │   │
│   │   │   ├── Certification/
│   │   │   │   ├── ApplicationController.php
│   │   │   │   ├── ReviewController.php
│   │   │   │   └── CertificationController.php
│   │   │   │
│   │   │   ├── Compliance/
│   │   │   │   ├── ComplianceCheckController.php
│   │   │   │   └── WarningController.php
│   │   │   │
│   │   │   ├── Report/
│   │   │   │   ├── FarmReportController.php
│   │   │   │   ├── SlaughterReportController.php
│   │   │   │   └── IndustryReportController.php
│   │   │   │
│   │   │   ├── Admin/
│   │   │   │   ├── UserController.php
│   │   │   │   ├── RoleController.php
│   │   │   │   └── SettingController.php
│   │   │   │
│   │   │   ├── Verification/
│   │   │   │   └── VerificationController.php    # For mobile QR scan
│   │   │   │
│   │   │   └── Reference/
│   │   │       ├── BreedController.php
│   │   │       ├── LocationController.php
│   │   │       └── ...
│   │   │
│   │   ├── Middleware/
│   │   │   ├── RoleMiddleware.php
│   │   │   └── EnsureUserOwnsResource.php
│   │   │
│   │   ├── Requests/                            # Form Validation
│   │   │   ├── Farm/
│   │   │   │   ├── StoreFarmRequest.php
│   │   │   │   └── UpdateFarmRequest.php
│   │   │   ├── Goat/
│   │   │   └── ...
│   │   │
│   │   └── Resources/                           # API Response Transformers
│   │       ├── FarmResource.php
│   │       ├── GoatResource.php
│   │       ├── SlaughterResource.php
│   │       └── ...
│   │
│   ├── Models/
│   │   ├── User.php
│   │   ├── Role.php
│   │   ├── Farm.php
│   │   ├── Goat.php
│   │   ├── HealthRecord.php
│   │   ├── Vaccination.php
│   │   ├── FeedRecord.php
│   │   ├── Inflow.php
│   │   ├── Outflow.php
│   │   ├── Transport.php
│   │   ├── SlaughterRecord.php
│   │   ├── QRCode.php
│   │   ├── BlockchainLog.php
│   │   ├── CertificationApplication.php
│   │   ├── CertificationReview.php
│   │   ├── Certification.php
│   │   ├── ComplianceCheck.php
│   │   ├── ComplianceWarning.php
│   │   ├── Breed.php
│   │   ├── Province.php
│   │   ├── Municipality.php
│   │   ├── Barangay.php
│   │   ├── Slaughterhouse.php
│   │   ├── HaramFacility.php
│   │   └── ...
│   │
│   ├── Services/                                # Business Logic
│   │   ├── Auth/
│   │   │   └── AuthService.php
│   │   ├── Farm/
│   │   │   └── FarmService.php
│   │   ├── Goat/
│   │   │   └── GoatService.php
│   │   ├── Blockchain/
│   │   │   └── BlockchainService.php
│   │   ├── GIS/
│   │   │   └── GISService.php
│   │   ├── SMS/
│   │   │   └── SMSService.php
│   │   ├── QRCode/
│   │   │   └── QRCodeService.php
│   │   └── Compliance/
│   │       └── ComplianceService.php
│   │
│   ├── Repositories/                            # Data Access
│   │   ├── FarmRepository.php
│   │   ├── GoatRepository.php
│   │   ├── SlaughterRepository.php
│   │   └── ...
│   │
│   └── Observers/                               # Model Events
│       ├── GoatObserver.php                     # Auto-calculate age class
│       ├── FarmObserver.php                     # Auto-calculate haram distance
│       └── SlaughterObserver.php                # Auto-generate QR, write blockchain
│
├── database/
│   ├── migrations/
│   │   ├── 0001_create_users_table.php
│   │   ├── 0002_create_roles_table.php
│   │   ├── 0003_create_farms_table.php
│   │   ├── 0004_create_goats_table.php
│   │   └── ...
│   │
│   └── seeders/
│       ├── RoleSeeder.php
│       ├── ProvinceSeeder.php
│       ├── MunicipalitySeeder.php
│       ├── BreedSeeder.php
│       └── ...
│
├── routes/
│   └── api.php                                  # ALL API routes
│
├── config/
│   ├── sanctum.php
│   ├── blockchain.php
│   ├── gis.php
│   └── sms.php
│
├── tests/
│   ├── Feature/
│   │   ├── Auth/
│   │   ├── Farm/
│   │   └── ...
│   └── Unit/
│
└── .env
```

### 4.3 Frontend: Nuxt 3

```
halal-goat-bin-web/
│
├── pages/
│   ├── index.vue                               # Landing / Dashboard
│   ├── login.vue
│   ├── register.vue
│   │
│   ├── dashboard/
│   │   ├── index.vue                           # Role-based dashboard
│   │   ├── farm-owner.vue
│   │   ├── slaughterhouse.vue
│   │   ├── certifier.vue
│   │   ├── lgu.vue
│   │   ├── da.vue
│   │   └── admin.vue
│   │
│   ├── farms/
│   │   ├── index.vue                           # List farms
│   │   ├── create.vue                          # Create farm
│   │   ├── [id]/
│   │   │   ├── index.vue                       # Farm details
│   │   │   ├── edit.vue                        # Edit farm
│   │   │   ├── goats/
│   │   │   │   ├── index.vue                   # List goats
│   │   │   │   ├── create.vue
│   │   │   │   └── [goatId].vue                # Goat details
│   │   │   ├── health/
│   │   │   ├── feed/
│   │   │   ├── inflows/
│   │   │   └── outflows/
│   │   └── ...
│   │
│   ├── slaughter/
│   │   ├── index.vue
│   │   ├── create.vue
│   │   └── [id].vue
│   │
│   ├── certification/
│   │   ├── index.vue                           # My applications
│   │   ├── apply.vue                           # Apply for certification
│   │   ├── review/                             # For certifiers
│   │   │   ├── index.vue
│   │   │   └── [id].vue
│   │   └── ...
│   │
│   ├── compliance/
│   │   ├── index.vue
│   │   └── warnings.vue
│   │
│   ├── reports/
│   │   ├── index.vue
│   │   ├── farm.vue
│   │   ├── slaughter.vue
│   │   └── industry.vue
│   │
│   ├── map/
│   │   └── index.vue                           # GIS map view
│   │
│   ├── admin/
│   │   ├── users/
│   │   ├── roles/
│   │   ├── settings/
│   │   └── reference-data/
│   │
│   └── profile/
│       └── index.vue
│
├── components/
│   ├── common/
│   │   ├── AppHeader.vue
│   │   ├── AppSidebar.vue
│   │   ├── AppFooter.vue
│   │   ├── LoadingSpinner.vue
│   │   ├── ConfirmModal.vue
│   │   └── AlertMessage.vue
│   │
│   ├── forms/
│   │   ├── FormInput.vue
│   │   ├── FormSelect.vue
│   │   ├── FormTextarea.vue
│   │   ├── FormDatePicker.vue
│   │   └── FormFileUpload.vue
│   │
│   ├── tables/
│   │   ├── DataTable.vue
│   │   ├── Pagination.vue
│   │   └── TableFilter.vue
│   │
│   ├── map/
│   │   ├── FarmMap.vue
│   │   ├── LocationPicker.vue
│   │   └── FarmMarker.vue
│   │
│   ├── farm/
│   │   ├── FarmCard.vue
│   │   ├── FarmForm.vue
│   │   └── FarmStats.vue
│   │
│   ├── goat/
│   │   ├── GoatCard.vue
│   │   ├── GoatForm.vue
│   │   ├── GoatList.vue
│   │   └── GoatTimeline.vue
│   │
│   ├── slaughter/
│   │   ├── SlaughterForm.vue
│   │   ├── SlaughterCard.vue
│   │   └── QRCodeDisplay.vue
│   │
│   ├── certification/
│   │   ├── CertificationStatus.vue
│   │   ├── ApplicationForm.vue
│   │   └── ReviewForm.vue
│   │
│   └── dashboard/
│       ├── StatsCard.vue
│       ├── RecentActivity.vue
│       └── ChartWidget.vue
│
├── composables/                                # Reusable logic
│   ├── useAuth.ts
│   ├── useApi.ts
│   ├── useFarms.ts
│   ├── useGoats.ts
│   ├── useSlaughter.ts
│   ├── useCertification.ts
│   ├── useCompliance.ts
│   ├── useMap.ts
│   └── useNotification.ts
│
├── stores/                                     # Pinia state management
│   ├── auth.ts
│   ├── farm.ts
│   ├── goat.ts
│   ├── notification.ts
│   └── settings.ts
│
├── middleware/
│   ├── auth.ts                                 # Require authentication
│   ├── guest.ts                                # Only for guests
│   └── role.ts                                 # Role-based access
│
├── layouts/
│   ├── default.vue                             # Dashboard layout
│   ├── auth.vue                                # Login/Register layout
│   └── public.vue                              # Public pages
│
├── plugins/
│   ├── api.ts                                  # Axios setup
│   └── toast.ts                                # Notifications
│
├── utils/
│   ├── helpers.ts
│   ├── validators.ts
│   └── formatters.ts
│
├── types/
│   ├── auth.ts
│   ├── farm.ts
│   ├── goat.ts
│   └── api.ts
│
├── assets/
│   ├── css/
│   │   └── main.css
│   └── images/
│
├── public/
│   └── favicon.ico
│
├── nuxt.config.ts
├── tailwind.config.ts                          # If using Tailwind CSS
└── package.json
```

### 4.4 Mobile: Flutter

```
halal-goat-bin-mobile/
│
├── lib/
│   ├── main.dart
│   │
│   ├── config/
│   │   ├── app_config.dart
│   │   ├── api_config.dart
│   │   └── routes.dart
│   │
│   ├── models/
│   │   ├── user.dart
│   │   ├── verification_result.dart
│   │   ├── farm.dart
│   │   ├── goat.dart
│   │   └── slaughter.dart
│   │
│   ├── services/
│   │   ├── api_service.dart
│   │   ├── auth_service.dart
│   │   ├── verification_service.dart
│   │   └── storage_service.dart
│   │
│   ├── providers/                              # State management
│   │   ├── auth_provider.dart
│   │   └── verification_provider.dart
│   │
│   ├── screens/
│   │   ├── splash_screen.dart
│   │   ├── home_screen.dart
│   │   ├── scanner_screen.dart
│   │   ├── verification_result_screen.dart
│   │   ├── history_screen.dart
│   │   └── settings_screen.dart
│   │
│   ├── widgets/
│   │   ├── qr_scanner_widget.dart
│   │   ├── verification_card.dart
│   │   ├── halal_badge.dart
│   │   ├── farm_info_card.dart
│   │   └── loading_widget.dart
│   │
│   └── utils/
│       ├── helpers.dart
│       └── constants.dart
│
├── assets/
│   ├── images/
│   └── fonts/
│
├── test/
│
├── pubspec.yaml
└── README.md
```

---

## 5. API Design

### 5.1 API Base URL

```
Development:  http://localhost:8000/api
Production:   https://api.halalgoatbin.ph/api
```

### 5.2 Authentication Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/auth/register` | Register new user | No |
| POST | `/auth/login` | Login, get token | No |
| POST | `/auth/logout` | Logout, revoke token | Yes |
| GET | `/auth/user` | Get current user | Yes |
| PUT | `/auth/profile` | Update profile | Yes |
| PUT | `/auth/password` | Change password | Yes |

### 5.3 Farm Management Endpoints

| Method | Endpoint | Description | Auth | Roles |
|--------|----------|-------------|------|-------|
| GET | `/farms` | List farms | Yes | All |
| POST | `/farms` | Create farm | Yes | Farm Owner |
| GET | `/farms/{id}` | Get farm details | Yes | All |
| PUT | `/farms/{id}` | Update farm | Yes | Farm Owner |
| DELETE | `/farms/{id}` | Delete farm | Yes | Farm Owner, Admin |

### 5.4 Goat Management Endpoints

| Method | Endpoint | Description | Auth | Roles |
|--------|----------|-------------|------|-------|
| GET | `/farms/{farmId}/goats` | List goats in farm | Yes | Farm roles |
| POST | `/farms/{farmId}/goats` | Add goat | Yes | Farm Owner, Worker |
| GET | `/goats/{id}` | Get goat details | Yes | Farm roles |
| PUT | `/goats/{id}` | Update goat | Yes | Farm Owner, Worker |
| DELETE | `/goats/{id}` | Delete goat | Yes | Farm Owner |
| GET | `/goats/{id}/health-records` | Get health records | Yes | Farm roles |
| POST | `/goats/{id}/health-records` | Add health record | Yes | Farm Owner, Worker |
| GET | `/goats/{id}/vaccinations` | Get vaccinations | Yes | Farm roles |
| POST | `/goats/{id}/vaccinations` | Add vaccination | Yes | Farm Owner, Worker |

### 5.5 Traceability Endpoints

| Method | Endpoint | Description | Auth | Roles |
|--------|----------|-------------|------|-------|
| GET | `/transports` | List transports | Yes | Farm, Slaughter |
| POST | `/transports` | Create transport | Yes | Farm Owner |
| PUT | `/transports/{id}/confirm` | Confirm arrival | Yes | Slaughter Staff |
| GET | `/slaughter-records` | List slaughter records | Yes | Slaughter roles |
| POST | `/slaughter-records` | Create slaughter record | Yes | Slaughter Staff |
| PUT | `/slaughter-records/{id}` | Update slaughter | Yes | Slaughter Staff |
| PUT | `/slaughter-records/{id}/approve` | Approve (Head) | Yes | Slaughter Head |
| GET | `/qr-codes/{code}` | Get QR code data | Yes | All |

### 5.6 Certification Endpoints

| Method | Endpoint | Description | Auth | Roles |
|--------|----------|-------------|------|-------|
| GET | `/certification/applications` | List applications | Yes | Various |
| POST | `/certification/applications` | Apply for cert | Yes | Farm Owner |
| GET | `/certification/applications/{id}` | Get application | Yes | Various |
| POST | `/certification/applications/{id}/review` | Add review | Yes | Certifier Staff |
| POST | `/certification/applications/{id}/approve` | Approve | Yes | Certifier Head |
| POST | `/certification/applications/{id}/reject` | Reject | Yes | Certifier Head |
| GET | `/certifications` | List certifications | Yes | Various |
| PUT | `/certifications/{id}/suspend` | Suspend cert | Yes | Certifier Head |

### 5.7 Verification Endpoint (Public/Mobile)

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/verify/{qr_code}` | Verify product by QR | No |
| GET | `/verify/hash/{hash}` | Verify by blockchain hash | No |

### 5.8 Reference Data Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/reference/breeds` | List breeds | Yes |
| GET | `/reference/provinces` | List provinces | Yes |
| GET | `/reference/municipalities/{provinceId}` | List municipalities | Yes |
| GET | `/reference/barangays/{municipalityId}` | List barangays | Yes |
| GET | `/reference/feed-types` | List feed types | Yes |
| GET | `/reference/medicine-types` | List medicine types | Yes |
| GET | `/reference/illness-types` | List illness types | Yes |

### 5.9 API Response Format

**Success Response:**
```json
{
    "success": true,
    "message": "Farm created successfully",
    "data": {
        "id": 1,
        "farm_code": "HGF-0001",
        "name": "Ahmad's Halal Goat Farm",
        "owner": {
            "id": 1,
            "name": "Ahmad Hassan"
        },
        "location": {
            "address": "Purok 5, Barangay Tinoto",
            "municipality": "Maasim",
            "province": "Sarangani",
            "latitude": 6.1234,
            "longitude": 125.5678
        },
        "certification_status": "certified",
        "created_at": "2026-02-01T10:30:00Z"
    }
}
```

**Error Response:**
```json
{
    "success": false,
    "message": "Validation failed",
    "errors": {
        "name": ["The name field is required."],
        "latitude": ["The latitude must be a valid coordinate."]
    }
}
```

**Verification Response:**
```json
{
    "success": true,
    "verified": true,
    "halal_status": "VERIFIED",
    "data": {
        "product": {
            "qr_code": "HGBP-2026-00001",
            "type": "Chevon",
            "weight_kg": 2.5
        },
        "farm": {
            "name": "Ahmad's Halal Goat Farm",
            "location": "Maasim, Sarangani",
            "certified": true,
            "certification_date": "2025-06-15"
        },
        "goat": {
            "code": "HGG-2025-00123",
            "breed": "Boer",
            "gender": "Male",
            "age_months": 18
        },
        "slaughter": {
            "date": "2026-02-01",
            "slaughterhouse": "Halal Processing Center",
            "slaughterer": "Imam Hassan Abdullah",
            "live_weight_kg": 35,
            "carcass_weight_kg": 18
        },
        "blockchain": {
            "hash": "7f8a9b2c3d4e5f6a7b8c9d0e...",
            "timestamp": "2026-02-01T10:30:00Z",
            "verified": true
        }
    }
}
```

---

## 6. Authentication & Security

### 6.1 Authentication Flow

```
NUXT (Web) + FLUTTER (Mobile) — Both use Sanctum Token

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   STEP 1: User Login                                            │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │                                                         │  │
│   │   POST /api/auth/login                                  │  │
│   │   {                                                     │  │
│   │       "email": "ahmad@example.com",                     │  │
│   │       "password": "password123"                         │  │
│   │   }                                                     │  │
│   │                                                         │  │
│   └─────────────────────────────────────────────────────────┘  │
│                           │                                     │
│                           ▼                                     │
│   STEP 2: Server Returns Token                                  │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │                                                         │  │
│   │   {                                                     │  │
│   │       "success": true,                                  │  │
│   │       "data": {                                         │  │
│   │           "token": "1|abc123xyz...",                    │  │
│   │           "user": {                                     │  │
│   │               "id": 1,                                  │  │
│   │               "name": "Ahmad Hassan",                   │  │
│   │               "role": "farm_owner"                      │  │
│   │           }                                             │  │
│   │       }                                                 │  │
│   │   }                                                     │  │
│   │                                                         │  │
│   └─────────────────────────────────────────────────────────┘  │
│                           │                                     │
│                           ▼                                     │
│   STEP 3: Client Stores Token                                   │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │                                                         │  │
│   │   Nuxt: Store in cookie/localStorage                    │  │
│   │   Flutter: Store in secure storage                      │  │
│   │                                                         │  │
│   └─────────────────────────────────────────────────────────┘  │
│                           │                                     │
│                           ▼                                     │
│   STEP 4: Include Token in All Requests                         │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │                                                         │  │
│   │   GET /api/farms                                        │  │
│   │   Headers:                                              │  │
│   │       Authorization: Bearer 1|abc123xyz...              │  │
│   │       Accept: application/json                          │  │
│   │                                                         │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 6.2 Role-Based Authorization

```php
// Laravel Middleware Example

// routes/api.php
Route::middleware(['auth:sanctum'])->group(function () {

    // Farm Owner only
    Route::middleware(['role:farm_owner'])->group(function () {
        Route::post('/farms', [FarmController::class, 'store']);
        Route::put('/farms/{id}', [FarmController::class, 'update']);
    });

    // Certifier Head only
    Route::middleware(['role:certifier_head'])->group(function () {
        Route::post('/certification/applications/{id}/approve', ...);
        Route::post('/certification/applications/{id}/reject', ...);
    });

    // Multiple roles
    Route::middleware(['role:farm_owner,farm_worker'])->group(function () {
        Route::post('/goats', [GoatController::class, 'store']);
    });

});
```

### 6.3 Security Measures

| Security | Implementation |
|----------|----------------|
| **HTTPS** | SSL certificate (required for production) |
| **CORS** | Configure allowed origins in Laravel |
| **Rate Limiting** | Laravel throttle middleware |
| **Input Validation** | Laravel Form Request classes |
| **SQL Injection** | Eloquent ORM (parameterized queries) |
| **XSS Protection** | Vue/Nuxt auto-escapes output |
| **CSRF** | Sanctum handles via tokens |
| **Password Hashing** | bcrypt (Laravel default) |
| **Token Expiry** | Configure in Sanctum |

---

## 7. Third-Party Services

### 7.1 GIS / Maps (TBD)

**Option A: OpenStreetMap + Leaflet (Recommended)**
```
Cost: FREE
Package: vue-leaflet
```

**Option B: Google Maps**
```
Cost: Freemium (free with limits)
Package: @fawmi/vue-google-maps
API Key: Required
```

**Configuration (.env):**
```env
GIS_PROVIDER=openstreetmap
# or
GIS_PROVIDER=google
GOOGLE_MAPS_API_KEY=your-api-key
```

### 7.2 SMS Gateway (TBD)

**Option A: Semaphore (Philippine Provider)**
```
Cost: ~₱0.35/SMS
Website: semaphore.co
```

**Option B: Twilio**
```
Cost: ~₱0.50/SMS
Website: twilio.com
```

**Configuration (.env):**
```env
SMS_PROVIDER=semaphore
SEMAPHORE_API_KEY=your-api-key
SEMAPHORE_SENDER_NAME=HalalGoat
```

### 7.3 Blockchain (TBD)

**Option A: Simple Hash Chain**
```
Cost: FREE
Implementation: Built into Laravel
Complexity: Easy
```

**Option B: Polygon (Public)**
```
Cost: Low gas fees
Implementation: Web3 PHP library
Complexity: Medium
```

**Option C: Hyperledger Fabric (Private)**
```
Cost: Server cost
Implementation: Separate service
Complexity: Complex
```

**Configuration (.env):**
```env
BLOCKCHAIN_PROVIDER=simple
# or
BLOCKCHAIN_PROVIDER=polygon
POLYGON_RPC_URL=https://polygon-rpc.com
POLYGON_PRIVATE_KEY=your-private-key
# or
BLOCKCHAIN_PROVIDER=hyperledger
HYPERLEDGER_API_URL=http://blockchain-api:3000
```

### 7.4 Email

**Options: SMTP, Mailgun, SendGrid, AWS SES**

**Configuration (.env):**
```env
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=587
MAIL_USERNAME=your-username
MAIL_PASSWORD=your-password
MAIL_FROM_ADDRESS=noreply@halalgoatbin.ph
MAIL_FROM_NAME="Halal GOAT Bin"
```

---

## 8. Deployment Architecture

### 8.1 Development Environment

```
LOCAL DEVELOPMENT

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   Developer Machine                                             │
│                                                                 │
│   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐         │
│   │   Laravel   │   │    Nuxt     │   │  PostgreSQL │         │
│   │   (API)     │   │   (Web)     │   │     (DB)    │         │
│   │             │   │             │   │             │         │
│   │ localhost:  │   │ localhost:  │   │ localhost:  │         │
│   │    8000     │   │    3000     │   │    5432     │         │
│   └─────────────┘   └─────────────┘   └─────────────┘         │
│                                                                 │
│   Tools:                                                        │
│   • Laravel Sail (Docker) OR php artisan serve                 │
│   • npm run dev (Nuxt)                                         │
│   • TablePlus / DBeaver (DB GUI)                               │
│   • Postman (API testing)                                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 8.2 Production: Single Server (Pilot)

```
SINGLE SERVER — Good for Pilot/MVP

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   DigitalOcean Droplet / AWS EC2                               │
│   ($20-40/month)                                                │
│                                                                 │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │                                                         │  │
│   │   Ubuntu 22.04 / 24.04                                  │  │
│   │                                                         │  │
│   │   ┌───────────────────────────────────────────────┐    │  │
│   │   │                 Nginx                          │    │  │
│   │   │         (Reverse Proxy + Static)              │    │  │
│   │   └────────────────┬──────────────────────────────┘    │  │
│   │                    │                                    │  │
│   │         ┌──────────┴──────────┐                        │  │
│   │         │                     │                        │  │
│   │         ▼                     ▼                        │  │
│   │   ┌───────────┐        ┌───────────┐                  │  │
│   │   │  Laravel  │        │   Nuxt    │                  │  │
│   │   │   (API)   │        │  (SSR)    │                  │  │
│   │   │  PHP-FPM  │        │  Node.js  │                  │  │
│   │   └─────┬─────┘        └───────────┘                  │  │
│   │         │                                              │  │
│   │         ▼                                              │  │
│   │   ┌───────────┐                                       │  │
│   │   │ PostgreSQL│                                       │  │
│   │   │           │                                       │  │
│   │   └───────────┘                                       │  │
│   │                                                         │  │
│   └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│   Domains:                                                      │
│   • api.halalgoatbin.ph → Laravel API                          │
│   • halalgoatbin.ph → Nuxt Frontend                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 8.3 Production: Scalable (Future)

```
SCALABLE ARCHITECTURE — For High Traffic

┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   AWS / DigitalOcean (Scalable)                                │
│                                                                 │
│                    ┌───────────────┐                           │
│                    │ Load Balancer │                           │
│                    └───────┬───────┘                           │
│                            │                                    │
│              ┌─────────────┼─────────────┐                     │
│              │             │             │                     │
│              ▼             ▼             ▼                     │
│        ┌─────────┐   ┌─────────┐   ┌─────────┐                │
│        │  App 1  │   │  App 2  │   │  App 3  │                │
│        │ Laravel │   │ Laravel │   │ Laravel │                │
│        │ + Nuxt  │   │ + Nuxt  │   │ + Nuxt  │                │
│        └────┬────┘   └────┬────┘   └────┬────┘                │
│             │             │             │                      │
│             └─────────────┼─────────────┘                      │
│                           │                                    │
│                           ▼                                    │
│              ┌────────────────────────┐                       │
│              │   Managed PostgreSQL   │                       │
│              │   (AWS RDS / DO DB)    │                       │
│              └────────────────────────┘                       │
│                                                                 │
│   Additional:                                                   │
│   • Redis for caching/sessions                                 │
│   • S3 for file storage                                        │
│   • CloudFront for CDN                                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 8.4 Deployment Recommendation

| Phase | Architecture | Estimated Cost |
|-------|--------------|----------------|
| **Development** | Local (Docker/Sail) | Free |
| **Pilot/MVP** | Single Server (DO $20-40) | $20-40/month |
| **Production** | Scalable (Multiple servers) | $100-300+/month |

---

## 9. Development Tools

### 9.1 Required Tools

| Tool | Purpose | Download |
|------|---------|----------|
| **VS Code** | Code editor | code.visualstudio.com |
| **Git** | Version control | git-scm.com |
| **Node.js** | For Nuxt | nodejs.org (v18+) |
| **PHP** | For Laravel | php.net (v8.2+) |
| **Composer** | PHP packages | getcomposer.org |
| **PostgreSQL** | Database | postgresql.org |
| **Docker** | Containers (optional) | docker.com |

### 9.2 Recommended VS Code Extensions

| Extension | Purpose |
|-----------|---------|
| **Volar** | Vue 3 support |
| **Laravel Extension Pack** | Laravel support |
| **Prettier** | Code formatting |
| **ESLint** | JavaScript linting |
| **PHP Intelephense** | PHP intelligence |
| **GitLens** | Git integration |
| **Thunder Client** | API testing |

### 9.3 Other Tools

| Tool | Purpose |
|------|---------|
| **TablePlus / DBeaver** | Database GUI |
| **Postman / Insomnia** | API testing |
| **Figma** | UI design |
| **GitHub / GitLab** | Code repository |

---

## 10. Environment Configuration

### 10.1 Laravel API (.env)

```env
APP_NAME="Halal GOAT Bin API"
APP_ENV=local
APP_KEY=base64:xxx
APP_DEBUG=true
APP_URL=http://localhost:8000

# Database
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=halal_goat_bin
DB_USERNAME=postgres
DB_PASSWORD=secret

# Sanctum
SANCTUM_STATEFUL_DOMAINS=localhost:3000

# GIS
GIS_PROVIDER=openstreetmap
GOOGLE_MAPS_API_KEY=

# SMS
SMS_PROVIDER=semaphore
SEMAPHORE_API_KEY=
SEMAPHORE_SENDER_NAME=HalalGoat

# Blockchain
BLOCKCHAIN_PROVIDER=simple

# Email
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=587
MAIL_USERNAME=
MAIL_PASSWORD=
```

### 10.2 Nuxt (.env)

```env
NUXT_PUBLIC_API_BASE_URL=http://localhost:8000/api
NUXT_PUBLIC_APP_NAME="Halal GOAT Bin"
```

---

## 11. Summary

### 11.1 Technology Stack (Final)

| Component | Technology | Version |
|-----------|------------|---------|
| **Backend API** | Laravel | 12 |
| **Frontend Web** | Nuxt | 3 |
| **Mobile App** | Flutter | Latest |
| **Authentication** | Laravel Sanctum | Latest |
| **Database** | PostgreSQL | 16+ |
| **GIS/Maps** | TBD | OpenStreetMap / Google |
| **SMS Gateway** | TBD | Semaphore / Twilio |
| **Blockchain** | TBD | Simple / Polygon / Hyperledger |
| **Hosting** | AWS / DigitalOcean | - |

### 11.2 Architecture Summary

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   NUXT 3 (Web)  ────┐                                          │
│                     │                                          │
│                     ├───▶  LARAVEL 12 API  ───▶  PostgreSQL    │
│                     │           │                              │
│   FLUTTER (Mobile) ─┘           │                              │
│                                 ▼                              │
│                            Blockchain                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 11.3 Project Structure Summary

| Project | Technology | Purpose |
|---------|------------|---------|
| `halal-goat-bin-api` | Laravel 12 | Backend API |
| `halal-goat-bin-web` | Nuxt 3 | Web Frontend |
| `halal-goat-bin-mobile` | Flutter | Mobile App |

---

## 12. TBD Items (To Be Decided)

| # | Item | Options | Decision |
|---|------|---------|----------|
| 1 | GIS Provider | OpenStreetMap + Leaflet / Google Maps | 🔄 TBD |
| 2 | SMS Provider | Semaphore / Twilio | 🔄 TBD |
| 3 | Blockchain | Simple Hash / Polygon / Hyperledger | 🔄 TBD |
| 4 | Hosting Provider | AWS / DigitalOcean | 🔄 TBD |

---

## ✅ STEP 6 COMPLETE — LEVEL 1 COMPLETE!

**This completes the Level 1 (High-Level Overview) documentation.**

---

## 13. All Documents Summary (Level 1)

| # | Document | Description | Status |
|---|----------|-------------|--------|
| 1 | STEP_01_STAKEHOLDERS.md | Who is involved | ✅ Complete |
| 2 | STEP_02_USER_ROLES_PERMISSIONS.md | Roles and access | ✅ Complete |
| 3 | STEP_03_BUSINESS_PROCESS_FLOW.md | How it works | ✅ Complete |
| 4 | STEP_04_MODULES_FEATURES.md | What to build | ✅ Complete |
| 5 | STEP_05_DATABASE_DESIGN.md | Data structure | ✅ Complete |
| 6 | STEP_06_TECHNICAL_ARCHITECTURE.md | How to build | ✅ Complete |
| 7 | MEETING_AGENDA_CLARIFICATION.md | Questions for meeting | ✅ Complete |
| 8 | ADDENDUM_FORM_TERMINOLOGY_CHANGES.md | Goat terminology updates | ✅ Complete |
| 9 | GIS_EXPLANATION_AND_USAGE.md | GIS explanation | ✅ Complete |
| 10 | BLOCKCHAIN_EXPLANATION_AND_USAGE.md | Blockchain explanation | ✅ Complete |

---

## 14. Next Steps (Level 2)

When ready to proceed to Level 2 (Detailed Design):

| Step | Description |
|------|-------------|
| 1 | Detailed database schema (field types, constraints, indexes) |
| 2 | API documentation (OpenAPI/Swagger) |
| 3 | UI/UX wireframes and mockups |
| 4 | User stories and acceptance criteria |
| 5 | Development sprint planning |

---

*Document Version: 1.0*  
*Last Updated: February 1, 2026*  
*Status: Level 1 Complete*
