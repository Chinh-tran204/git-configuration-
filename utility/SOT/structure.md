# Hospital Management System - Architecture

## Project Overview
Hospital Management System is a C-based backend application with GTK+ UI for managing:
- Patient records (HL7 format)
- Appointments scheduling
- Billing/invoicing
- User authentication
- Audit logging

---

## Directory Structure

### `/Backend` - Core Business Logic (C modules)
**Status:** Completed ✅

Core modules handling hospital operations:
- **auth_manager** - User authentication, session management (roles: ADMIN, USER)
- **patient_manager** - Patient CRUD operations, HL7 record handling
- **appointment_manager** - Schedule management, conflict detection
- **billing_manager** - Invoice generation, payment tracking
- **hl7_parser** - HL7 message parsing (PID, OBX, SCH, UB1 segments)
- **audit_logger** - Activity logging, compliance tracking
- **utils** - Common utilities (file I/O, validation, hashing)
- **Makefile** - Build configuration

### `/UI` - User Interface Layer (GTK+)
**Status:** ui_utils PARTIALLY COMPLETE (header + dialog functions) | 6 modules remaining

**Completed:**
- **ui_utils** - GTK+ helper framework
  - Header: 519 lines, 34 functions ✅
  - Dialog functions: 6/6 implemented ✅ (show_info, show_error, show_confirmation, show_input, etc.)
  - Validation functions: 7/7 headers ready (validate_phone, validate_email, validate_date, etc.)
  - Widget helpers: 8/8 headers ready (create_text_entry, create_button, create_label, etc.)
  - Layout builders: 6/6 headers ready (create_vbox, create_hbox, create_grid, etc.)

**Modules to develop (6 remaining):**
- **main_window** - Application frame, menu system, tabs
- **auth_form** - Login/logout interface
- **patient_form** - Patient registration, search, details view
- **appointment_form** - Schedule management dialogs
- **billing_form** - Invoice creation, payment tracking
- **reports_form** - Report generation interface

### `/Data` - Runtime Data Storage
Subdirectories for HL7 records:
- **patients/** - Patient .seg files
- **appointments/** - Appointment records
- **audit_logs/** - Activity logs
- **sessions/** - Active session tokens
- **backups/** - Data backups
- **config/** - Configuration files (credentials.db, etc.)

### `/Scripts` - Operational Tools (Bash)
**Status:** Complete ✅

- **init_db.sh** - Database initialization
- **backup.sh** - Data backup
- **restore.sh** - Data recovery
- **hl7_validator.sh** - HL7 message validation
- **maintenance.sh** - System maintenance

### `/Tests` - Test Suite
**Status:** Missing ❌

To contain: Unit tests, integration tests, test data

---

## Module Dependencies

```
Auth System
├── auth_manager.c ──→ utils.c (hashing)
├── audit_logger.c ──→ (logs auth events)
└── Backend/credentials.db ──→ (user database)

Patient System
├── patient_manager.c ──→ hl7_parser.c (record parsing)
├── audit_logger.c ──→ (logs patient changes)
└── Data/patients/ ──→ (HL7 .seg files)

Appointment System
├── appointment_manager.c ──→ hl7_parser.c (SCH segments)
├── patient_manager.c ──→ (patient lookup)
├── audit_logger.c ──→ (logs appointments)
└── Data/appointments/ ──→ (apt records)

Billing System
├── billing_manager.c ──→ hl7_parser.c (UB1 segments)
├── patient_manager.c ──→ (patient lookup)
├── audit_logger.c ──→ (logs billing events)
└── Data/backups/ ──→ (invoice backups)

UI Layer
├── main_window.c ──→ (all backend modules)
├── auth_form.c ──→ auth_manager.c
├── patient_form.c ──→ patient_manager.c
├── appointment_form.c ──→ appointment_manager.c
├── billing_form.c ──→ billing_manager.c
└── ui_utils.c ──→ (GTK+ helpers)
```

---

## Key Structures (HL7-Based)

| Segment | Purpose | Stored In |
|---------|---------|-----------|
| **PID** | Patient ID, demographics | patient_manager.h |
| **OBX** | Observations (vitals, test results) | patient_manager.h |
| **SCH** | Schedule (appointments) | appointment_manager.h |
| **UB1** | Billing/charges data | billing_manager.h |

---

## Build Targets

- **Backend Build** - `make` in Backend/
- **UI Build** - `make` in UI/ (once UI modules completed)
- **Full Build** - Build both backend and UI
