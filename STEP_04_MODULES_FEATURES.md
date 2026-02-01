# 📋 HALAL GOAT BIN PROJECT - DOCUMENTATION

## PROJECT KICKOFF MEETING

**Project:** Halal GOAT Bin: A Geographically-Oriented Application and Traceability System  
**Date:** February 1, 2026  
**Document:** Step 4 - Modules & Features  
**Status:** DRAFT (Contains TBD items pending clarification meeting)

---

# STEP 4: MODULES & FEATURES

## Overview

This document defines what to build — all modules and features for both the Web Application and Mobile App.

---

## 4.1 System Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        HALAL GOAT BIN SYSTEM                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   ┌─────────────────────────────────────┐   ┌─────────────────────────┐ │
│   │        WEB APPLICATION              │   │      MOBILE APP         │ │
│   │          (Laravel)                  │   │       (Flutter)         │ │
│   ├─────────────────────────────────────┤   ├─────────────────────────┤ │
│   │                                     │   │                         │ │
│   │  • Farm Management Module           │   │  • QR Code Scanner      │ │
│   │  • Traceability Module              │   │  • Product Verification │ │
│   │  • Certification Module             │   │  • SMS Integration      │ │
│   │  • Halal Compliance Module          │   │                         │ │
│   │  • Reports & Analytics Module       │   │                         │ │
│   │  • GIS / Mapping Module             │   │                         │ │
│   │  • User Management Module           │   │                         │ │
│   │  • System Admin Module              │   │                         │ │
│   │                                     │   │                         │ │
│   └─────────────────────────────────────┘   └─────────────────────────┘ │
│                         │                             │                 │
│                         └──────────────┬──────────────┘                 │
│                                        │                                │
│                                        ▼                                │
│                         ┌─────────────────────────────┐                 │
│                         │      SHARED COMPONENTS      │                 │
│                         ├─────────────────────────────┤                 │
│                         │  • Database (MySQL)         │                 │
│                         │  • API (RESTful)            │                 │
│                         │  • Blockchain               │                 │
│                         │  • SMS Gateway              │                 │
│                         └─────────────────────────────┘                 │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 4.2 Module Summary

| # | Module | Description | Platform | Features |
|---|--------|-------------|----------|----------|
| 1 | Farm Management | Farm & goat records, daily operations | Web | 25+ |
| 2 | Traceability | Transport, slaughter, QR codes, blockchain | Web | 15+ |
| 3 | Certification | Halal certification application & approval | Web | 12+ |
| 4 | Halal Compliance | Compliance monitoring & warnings | Web | 8+ |
| 5 | Reports & Analytics | Reports, dashboards, statistics | Web | 15+ |
| 6 | GIS / Mapping | Farm locations, haram facility distance | Web | 8+ |
| 7 | User Management | User accounts, roles, staff management | Web | 12+ |
| 8 | System Admin | System settings, data management | Web | 10+ |
| 9 | Mobile App | QR scanner, product verification | Mobile | 6+ |

**Total: 100+ Features**

---

## 4.3 WEB APPLICATION MODULES

---

### MODULE 1: FARM MANAGEMENT

#### 1.1 Farm Profile

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Create Farm | Register new farm with details | Farm Owner |
| 2 | View Farm | View farm information | Farm Owner, Worker, Certifier, LGU, DA, Admin |
| 3 | Edit Farm | Update farm details | Farm Owner, Admin |
| 4 | Farm Location (GIS) | Map location of farm | Farm Owner (input), All (view) |
| 5 | Haram Distance Calculator | Auto-calculate distance from haram facilities | System (auto) |
| 6 | Farm Photo Gallery | Upload farm photos | Farm Owner |
| 7 | Farm Documents | Upload supporting documents | Farm Owner |

#### 1.2 Goat Records

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Register Goat | Add new goat with details (breed, gender, birth date) | Farm Owner, Worker |
| 2 | View Goat List | List all goats in farm with filters | Farm Owner, Worker, Certifier, LGU, DA, Admin |
| 3 | View Goat Profile | Detailed goat information | Farm Owner, Worker, Certifier, LGU, DA, Admin |
| 4 | Edit Goat | Update goat details | Farm Owner, Worker |
| 5 | Delete Goat | Remove goat record | Farm Owner, Admin |
| 6 | Goat Status Tracking | Track status (Active, Sold, Slaughtered, Dead) | System (auto) |
| 7 | Goat Photo | Upload goat photo | Farm Owner, Worker |
| 8 | Goat History | View complete history of goat | Farm Owner, Worker |

#### 1.3 Health & Medical Records

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Add Health Record | Record illness, symptoms, diagnosis | Farm Owner, Worker |
| 2 | Add Treatment | Record treatment given | Farm Owner, Worker |
| 3 | Add Medicine | Record medicine administered | Farm Owner, Worker |
| 4 | View Health History | View goat's complete medical history | Farm Owner, Worker, Certifier |
| 5 | Add Vaccination | Record vaccination given | Farm Owner, Worker |
| 6 | Vaccination Schedule | Track upcoming vaccinations | Farm Owner, Worker |
| 7 | Medicine Halal Check | Flag if medicine is non-halal | System (auto) |
| 8 | Health Alerts | Notify if goat health is critical | System (auto) |

#### 1.4 Feed & Nutrition

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Add Feed Record | Record feeding (type, brand, quantity) | Farm Owner, Worker |
| 2 | View Feed History | View feeding records | Farm Owner, Worker, Certifier |
| 3 | Feed Supplier Record | Record feed supplier details | Farm Owner, Worker |
| 4 | Feed Ingredients | Record/view feed ingredients | Farm Owner, Worker |
| 5 | Feed Halal Check | Flag if feed contains haram ingredients | System (auto) |
| 6 | Feed Inventory | Track feed stock levels | Farm Owner, Worker |

#### 1.5 Inflows (Incoming Products/Goats)

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Record Goat Purchase | Goats bought from outside farm | Farm Owner, Worker |
| 2 | Record Goat Birth | New kids born on farm | Farm Owner, Worker |
| 3 | Record Feed Delivery | Feed/supplies received | Farm Owner, Worker |
| 4 | Record Biologics | Vaccines/medicines received | Farm Owner, Worker |
| 5 | View Inflow History | List all incoming records | Farm Owner, Worker |

#### 1.6 Outflows (Outgoing Products/Goats)

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Record Goat Sale | Goats sold to buyers | Farm Owner, Worker |
| 2 | Record Goat for Slaughter | Goats sent to slaughterhouse | Farm Owner, Worker |
| 3 | Record Goat Death | Goats that died (with cause) | Farm Owner, Worker |
| 4 | Record Goat Transfer | Goats transferred to another farm | Farm Owner, Worker |
| 5 | View Outflow History | List all outgoing records | Farm Owner, Worker |

#### 1.7 Production & Forecasting

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Population Dashboard | Current goat count by breed, gender, age | Farm Owner, Worker |
| 2 | Birth Records | Track kids born (monthly/yearly) | Farm Owner, Worker |
| 3 | Death Records | Track deaths (monthly/yearly) | Farm Owner, Worker |
| 4 | Growth Trends | Population growth over time (chart) | Farm Owner |
| 5 | Demand Forecasting | Predict future demand based on trends | Farm Owner |
| 6 | Production Statistics | Production summary statistics | Farm Owner |

---

### MODULE 2: TRACEABILITY

#### 2.1 Transport Tracking 🔄 TBD

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Create Transport Record | Record goats being transported | Farm Owner / 🔄 TBD |
| 2 | View Transport Status | Track goat transit status | Farm Owner, Slaughterhouse |
| 3 | Update Transport Status | Update transit progress | 🔄 TBD |
| 4 | Confirm Arrival | Confirm goats arrived at destination | Slaughterhouse Staff |
| 5 | Transport History | View all transport records | Farm Owner, Slaughterhouse |

**🔄 TBD:** Who is responsible for transport recording? Farm Owner / Slaughterhouse / Separate Transporter role?

#### 2.2 Slaughter Records

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Pre-Slaughter Verification | Verify goat from certified farm | Slaughterhouse Staff |
| 2 | Block Non-Certified | System blocks goats from non-certified farms | System (auto) |
| 3 | Create Slaughter Record | Input slaughter details | Slaughterhouse Staff |
| 4 | Record Live Weight | Weight before slaughter | Slaughterhouse Staff |
| 5 | Record Slaughterer Name | Who performed halal slaughter | Slaughterhouse Staff |
| 6 | Record Slaughter Time | Date and time of slaughter | Slaughterhouse Staff |
| 7 | Record Carcass Weight | Weight after slaughter | Slaughterhouse Staff |
| 8 | Record Offal Weight | Weight of offals | Slaughterhouse Staff |
| 9 | Record Meat Cuts | Types of cuts produced | Slaughterhouse Staff |
| 10 | View Slaughter Record | View slaughter details | Slaughterhouse Staff, Head |
| 11 | Edit Slaughter Record | Update slaughter details | Slaughterhouse Staff (own), Head (all) |
| 12 | Approve Slaughter Record | Head approves record | Slaughterhouse Head |
| 13 | Slaughter History | List all slaughter records | Slaughterhouse Head, Admin |

#### 2.3 QR Code Management

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Generate QR Code | Auto-generate after slaughter data complete | System (auto) |
| 2 | View QR Code | View QR code on screen | Slaughterhouse Staff |
| 3 | Print QR Code | Print QR code label | Slaughterhouse Staff |
| 4 | QR Code Data | View data embedded in QR | Slaughterhouse Staff, Head |
| 5 | QR Code History | List all generated QR codes | Slaughterhouse Head, Admin |
| 6 | QR Code Verification | Verify QR code is valid | All |

#### 2.4 Blockchain Records

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View Blockchain Log | View immutable transaction records | Admin, Certifier |
| 2 | Verify Transaction | Verify data integrity on blockchain | Admin, Certifier |
| 3 | Transaction History | List all blockchain transactions | Admin |

#### 2.5 Product Release 🔄 TBD

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Record Product Release | Record meat released to market | Slaughterhouse Staff |
| 2 | Release Destination | Record where product is going | Slaughterhouse Staff |
| 3 | View Release History | Track where products went | Slaughterhouse Head |

**🔄 TBD:** Do we track products after they leave slaughterhouse?

---

### MODULE 3: CERTIFICATION

#### 3.1 Certification Application

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Apply for Certification | Submit farm for halal certification | Farm Owner |
| 2 | View Application Form | Pre-filled form with farm data | Farm Owner |
| 3 | Upload Supporting Documents | Attach required documents | Farm Owner |
| 4 | Submit Application | Send application to certifier | Farm Owner |
| 5 | View Application Status | Check application progress | Farm Owner |
| 6 | Cancel Application | Withdraw pending application | Farm Owner |

#### 3.2 Certification Review

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View Pending Applications | List applications waiting for review | Certifier Staff, Head |
| 2 | View Application Details | See full application and farm data | Certifier Staff, Head |
| 3 | Review Farm Data | Check farm compliance data | Certifier Staff |
| 4 | Review Compliance Status | Check auto-generated compliance | Certifier Staff |
| 5 | Add Review Notes | Add comments/observations | Certifier Staff |
| 6 | Recommend Approval | Forward to Head with recommendation | Certifier Staff |
| 7 | Recommend Rejection | Forward to Head with rejection reason | Certifier Staff |

#### 3.3 Certification Approval

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View Recommendations | List applications with staff recommendations | Certifier Head |
| 2 | Approve Certification | Grant halal certification | Certifier Head |
| 3 | Reject Certification | Deny certification with reason | Certifier Head |
| 4 | Request More Info | Return to farm owner for more details | Certifier Head |

#### 3.4 Certification Management

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View Certified Farms | List all certified farms | Certifier, LGU, DA, Admin |
| 2 | View Certification Details | See certification info | Certifier, LGU, DA, Admin |
| 3 | Suspend Certification | Revoke certification (violation) | Certifier Head |
| 4 | Reinstate Certification | Restore suspended certification | Certifier Head |
| 5 | Certification History | View certification timeline | Certifier, Admin |
| 6 | Renewal Reminder | Notify when certification expiring | System (auto) |
| 7 | Certification Statistics | Count of certified farms | Certifier Head, DA, Admin |

---

### MODULE 4: HALAL COMPLIANCE

#### 4.1 Compliance Checklist

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View Compliance Criteria | List of halal requirements | Farm Owner, Certifier |
| 2 | View Farm Compliance | Check farm against criteria | Farm Owner, Certifier |
| 3 | Auto-Check Compliance | System checks compliance status | System (auto) |
| 4 | Compliance Score | Overall compliance percentage | Farm Owner, Certifier |

#### 4.2 Warnings & Flags

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View Warnings | List compliance warnings for farm | Farm Owner, Certifier, LGU |
| 2 | Flag: Non-Halal Feed | Auto-flag haram feed ingredients | System (auto) |
| 3 | Flag: Non-Halal Medicine | Auto-flag non-certified medicine | System (auto) |
| 4 | Flag: Near Haram Facility | Auto-flag if too close to haram | System (auto) |
| 5 | Flag: Sick Goat for Slaughter | Auto-flag unhealthy goat | System (auto) |
| 6 | Resolve Warning | Mark issue as resolved | Farm Owner |
| 7 | Warning History | View past warnings | Farm Owner, Certifier |

#### 4.3 Compliance Reports

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Farm Compliance Report | Individual farm compliance summary | Farm Owner, Certifier |
| 2 | Industry Compliance Report | Regional compliance statistics | DA, Admin |
| 3 | Non-Compliant Farms List | List farms with violations | Certifier, LGU |

---

### MODULE 5: REPORTS & ANALYTICS

#### 5.1 Farm Reports

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Farm Summary Report | Overview of farm operations | Farm Owner |
| 2 | Production Report | Goat production statistics | Farm Owner |
| 3 | Health Report | Health/medical summary | Farm Owner |
| 4 | Feed Report | Feeding records summary | Farm Owner |
| 5 | Financial Summary | Sales/purchases overview | Farm Owner |
| 6 | Export to PDF | Download report as PDF | Farm Owner |
| 7 | Export to Excel | Download report as Excel | Farm Owner |

#### 5.2 Slaughterhouse Reports

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Daily Slaughter Report | Today's slaughter summary | Slaughterhouse Head |
| 2 | Weekly Slaughter Report | Weekly slaughter statistics | Slaughterhouse Head |
| 3 | Monthly Slaughter Report | Monthly slaughter summary | Slaughterhouse Head |
| 4 | Product Output Report | Meat production statistics | Slaughterhouse Head |
| 5 | Source Farms Report | Which farms supplied goats | Slaughterhouse Head |

#### 5.3 Industry Reports

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Regional Statistics | Halal goat industry overview | DA Head |
| 2 | Certification Statistics | Certified vs non-certified farms | DA, Certifier |
| 3 | Production Trends | Industry production over time | DA Head |
| 4 | Municipality Breakdown | Statistics by LGU | DA Head, LGU Head |
| 5 | Trend Analysis | Industry growth trends | DA Head |

#### 5.4 Dashboards

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Farm Dashboard | Farm owner's overview (goats, health, compliance) | Farm Owner |
| 2 | Worker Dashboard | Assigned tasks and quick actions | Farm Worker |
| 3 | Slaughterhouse Dashboard | Daily operations overview | Slaughterhouse Head, Staff |
| 4 | Certifier Dashboard | Pending applications, certified farms | Certifier Head, Staff |
| 5 | LGU Dashboard | Farms in jurisdiction, compliance | LGU Head, Staff |
| 6 | DA Dashboard | Industry-wide statistics | DA Head, Staff |
| 7 | Admin Dashboard | System-wide overview, alerts | Admin |

---

### MODULE 6: GIS / MAPPING

#### 6.1 Farm Mapping

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Set Farm Location | Pin farm on map | Farm Owner |
| 2 | View Farm on Map | Display single farm location | All |
| 3 | View All Farms | Regional map of all farms | Certifier, LGU, DA, Admin |
| 4 | Filter by Certification | Show certified/non-certified | Certifier, LGU, DA, Admin |
| 5 | Filter by Municipality | Show farms by LGU | LGU |
| 6 | Farm Info Popup | Click farm to see basic info | Certifier, LGU, DA, Admin |

#### 6.2 Haram Facility Mapping

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View Haram Facilities | Display haram facilities on map | Certifier, Admin |
| 2 | Add Haram Facility | Register haram facility location | Admin |
| 3 | Distance Calculator | Calculate distance from farm to haram | System (auto) |
| 4 | Distance Warning | Alert if farm too close | System (auto) |

#### 6.3 Regional View

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View by Municipality | Filter farms by municipality | LGU |
| 2 | View by Province | Filter farms by province | DA |
| 3 | Region 12 Overview | Full region map | DA |
| 4 | Heat Map | Density of farms by area | DA, Admin |

---

### MODULE 7: USER MANAGEMENT

#### 7.1 Authentication

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Register Account | Create new user account | Public |
| 2 | Login | Access system with credentials | All users |
| 3 | Logout | Exit system | All users |
| 4 | Forgot Password | Reset password via email | All users |
| 5 | Change Password | Update own password | All users |
| 6 | Two-Factor Authentication | Optional 2FA security | All users |

#### 7.2 User Profile

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View Profile | View own profile details | All users |
| 2 | Edit Profile | Update own profile | All users |
| 3 | Upload Photo | Add profile picture | All users |
| 4 | Notification Settings | Configure notifications | All users |

#### 7.3 User Administration

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | View All Users | List all system users | Admin |
| 2 | Search Users | Search by name, role, status | Admin |
| 3 | Create User | Add new user account | Admin |
| 4 | Edit User | Update user details | Admin |
| 5 | Activate User | Enable user account | Admin |
| 6 | Deactivate User | Disable user account | Admin |
| 7 | Delete User | Remove user permanently | Admin |
| 8 | Assign Role | Set user role | Admin |
| 9 | Reset Password | Admin reset user password | Admin |

#### 7.4 Staff Management (Head → Staff)

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Add Farm Worker | Farm owner invites worker | Farm Owner |
| 2 | View Farm Workers | List workers under farm | Farm Owner |
| 3 | Remove Farm Worker | Remove worker from farm | Farm Owner |
| 4 | Add Slaughterhouse Staff | Head adds staff | Slaughterhouse Head |
| 5 | View Slaughterhouse Staff | List staff under slaughterhouse | Slaughterhouse Head |
| 6 | Remove Slaughterhouse Staff | Remove staff | Slaughterhouse Head |
| 7 | Add Certifier Staff | Head adds staff | Certifier Head |
| 8 | Add LGU Staff | Head adds staff | LGU Head |
| 9 | Add DA Staff | Head adds staff | DA Head |

---

### MODULE 8: SYSTEM ADMINISTRATION

#### 8.1 System Settings

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | General Settings | System name, logo, contact | Admin |
| 2 | Halal Criteria Settings | Define compliance requirements | Admin |
| 3 | Distance Threshold | Set minimum distance from haram | Admin |
| 4 | Notification Settings | Configure system alerts | Admin |
| 5 | Email Settings | SMTP configuration | Admin |
| 6 | SMS Settings | SMS gateway configuration | Admin |

#### 8.2 Data Management

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Backup Database | Create system backup | Admin |
| 2 | Restore Database | Restore from backup | Admin |
| 3 | Export Data | Export data to file | Admin |
| 4 | Import Data | Import data from file | Admin |
| 5 | Audit Log | View system activity log | Admin |
| 6 | Error Log | View system error log | Admin |

#### 8.3 Reference Data Management

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| 1 | Manage Goat Breeds | Add/edit/delete breed list | Admin |
| 2 | Manage Feed Types | Add/edit/delete feed types | Admin |
| 3 | Manage Medicine Types | Add/edit medicine with halal status | Admin |
| 4 | Manage Illness Types | Add/edit illness categories | Admin |
| 5 | Manage Locations | Municipality/barangay list | Admin |
| 6 | Manage Slaughterhouses | Register slaughterhouses | Admin |
| 7 | Manage Haram Facilities | Register haram facility locations | Admin |

---

## 4.4 MOBILE APPLICATION FEATURES

### Mobile App: Halal GOAT Bin

| # | Feature | Description | User Access |
|---|---------|-------------|-------------|
| **QR Code Scanner** | | |
| 1 | Open Scanner | Launch camera for QR scanning | Consumer (public) |
| 2 | Scan QR Code | Read QR code from product | Consumer |
| 3 | Flashlight Toggle | Turn on light for dark areas | Consumer |
| **Product Verification** | | |
| 4 | View Halal Status | Display "HALAL VERIFIED ✅" or "NOT VERIFIED ❌" | Consumer |
| 5 | View Product Info | Product ID, weight, date | Consumer |
| 6 | View Farm Info | Farm name, location, certification | Consumer |
| 7 | View Goat Info | Breed, gender, age | Consumer |
| 8 | View Slaughter Info | Date, slaughterhouse, slaughterer | Consumer |
| 9 | View Certification | Certification status and date | Consumer |
| **History & Favorites** | | |
| 10 | Scan History | List of previously scanned products | Consumer |
| 11 | Clear History | Delete scan history | Consumer |
| **SMS Integration** | | |
| 12 | SMS Data Entry | Farmers send data via SMS format | Farm Owner |
| 13 | SMS Notifications | Receive alerts via SMS | Farm Owner |
| **App Settings** | | |
| 14 | Language Selection | Choose app language | Consumer |
| 15 | About App | App info, version, contact | Consumer |

---

## 4.5 QR Code Data Structure

### Data Embedded in QR Code:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         QR CODE CONTENTS                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  PRODUCT INFORMATION                                                    │
│  ├── Product ID: HGBP-2026-00001                                        │
│  ├── Product Type: Chevon (Goat Meat)                                   │
│  ├── Weight: 2.5 kg                                                     │
│  └── QR Generated: 2026-02-01 10:30:00                                  │
│                                                                         │
│  FARM INFORMATION                                                       │
│  ├── Farm ID: HGF-0001                                                  │
│  ├── Farm Name: Ahmad's Halal Goat Farm                                 │
│  ├── Location: Maasim, Sarangani                                        │
│  ├── Certification Status: CERTIFIED ✅                                 │
│  └── Certification Date: 2025-06-15                                     │
│                                                                         │
│  GOAT INFORMATION                                                       │
│  ├── Goat ID: HGG-2025-00123                                            │
│  ├── Breed: Boer                                                        │
│  ├── Gender: Male                                                       │
│  └── Age: 18 months                                                     │
│                                                                         │
│  SLAUGHTER INFORMATION                                                  │
│  ├── Slaughter Date: 2026-02-01                                         │
│  ├── Slaughterhouse: Halal Processing Center, Gen. Santos               │
│  ├── Slaughterer: Imam Hassan Abdullah                                  │
│  ├── Live Weight: 35 kg                                                 │
│  └── Carcass Weight: 18 kg                                              │
│                                                                         │
│  VERIFICATION                                                           │
│  ├── Blockchain Hash: 0x7f8a9b2c...                                     │
│  └── Verify URL: https://halalgoatbin.ph/verify/HGBP-2026-00001         │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 4.6 TBD Features (Pending Meeting)

| # | Module | Feature | Question |
|---|--------|---------|----------|
| 1 | Traceability | Transport Tracking | Who records transport? Separate role? |
| 2 | Traceability | Product Release | Track after slaughterhouse? |
| 3 | New Module? | Market/Retailer Features | Include market role with login? |
| 4 | Certification | Slaughterhouse Certification | Can slaughterhouse apply for certification? |

---

## 4.7 Feature Priority (Suggested)

### Phase 1: Core Features (Must Have)

| Module | Priority Features |
|--------|-------------------|
| Farm Management | Farm profile, goat records, health records |
| Traceability | Slaughter records, QR code generation |
| Certification | Application, review, approval |
| User Management | Authentication, basic user admin |
| Mobile App | QR scanner, product verification |

### Phase 2: Important Features (Should Have)

| Module | Priority Features |
|--------|-------------------|
| Farm Management | Feed records, inflows/outflows, forecasting |
| Halal Compliance | Compliance checklist, warnings |
| Reports | Farm reports, slaughterhouse reports |
| GIS/Mapping | Farm mapping, haram distance |

### Phase 3: Enhancement Features (Nice to Have)

| Module | Priority Features |
|--------|-------------------|
| Reports | Industry reports, advanced dashboards |
| GIS/Mapping | Heat maps, regional views |
| System Admin | Advanced settings, audit logs |
| Mobile App | SMS integration, history |

---

## 4.8 Summary

| Category | Count |
|----------|-------|
| Total Modules | 9 |
| Web Features | 110+ |
| Mobile Features | 15+ |
| TBD Features | 4 |

---

## ✅ STEP 4 COMPLETE (DRAFT)

**Status:** Draft — Contains TBD items pending clarification meeting

**Next Steps:**
1. Conduct clarification meeting
2. Update TBD features based on meeting outcomes
3. Proceed to Step 5: Database Design (High-Level)

---

*Document Version: 1.0 (DRAFT)*  
*Last Updated: February 1, 2026*  
*Status: Pending clarification meeting*
