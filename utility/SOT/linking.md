# 🔗 Hospital Management System - Linking Map
*Your guide to how everything talks to everything else*

---

## 🛠️ UI Utilities Foundation (The Helper)

| Owner | Purpose |
|-------|---------|
| `UI/ui_utils.c` | 🛠️ GTK+ helpers, dialogs, validation, layouts |

**Status:** Partially complete - Dialog functions ✅, Ready: validation & widgets

**Used by:**
- `UI/main_window.c` → Create menu dialogs, confirm actions
- `UI/auth_form.c` → Login dialogs, input validation
- `UI/patient_form.c` → Patient form layouts, field validation
- `UI/appointment_form.c` → Date/time inputs, confirmation dialogs
- `UI/billing_form.c` → Amount validation, confirmation dialogs
- `UI/reports_form.c` → Report dialogs, display formatting

**What it provides:**

```
Dialog Functions (6/6 ✅):
  show_info_dialog()           → Display info message
  show_error_dialog()          → Display error (red icon)
  show_confirmation_dialog()   → Ask Yes/No question
  show_input_dialog()          → Get text from user
  show_input_dialog_masked()   → Get password (masked)
  show_warning_dialog()        → Display warning (bonus)

Validation Functions (7 ready):
  validate_phone()             → Check phone format
  validate_email()             → Check email format
  validate_date()              → Validate YYYYMMDD
  validate_numeric()           → Check number range
  validate_text_field()        → Text length/chars
  validate_empty_field()       → Required field check
  validate_alphanumeric()      → Alphanumeric only

Widget Helpers (8 ready):
  create_text_entry()          → Text input field
  create_password_entry()      → Masked input
  create_button()              → Button with callback
  create_label()               → Formatted labels
  create_combo_box()           → Dropdown selection
  create_text_view()           → Multiline editor
  get_entry_text()             → Get field value
  set_entry_text()             → Set field value

Layout Builders (6 ready):
  create_vbox()                → Vertical layout
  create_hbox()                → Horizontal layout
  create_grid()                → Grid layout
  create_form_field()          → Label + widget pair
  create_scrolled_window()     → Scrollable container
  set_widget_margins()         → Add margins
```

**Design:** Common library shared by all UI forms - no duplication

---

## 🔐 Authentication (Who Gets In?)
| Owner | Purpose |
|-------|---------|
| `Backend/auth_manager.c` | 🎫 Login, sessions, roles |

**Talks to:**
- `UI/auth_form.c` ← login page (TODO)
- `Backend/utils.c` → password hashing
- `Backend/audit_logger.c` → logs who logged in
- `Data/config/credentials.db` → user accounts

**Key Functions:**
```
auth_login()           → User enters username/password
auth_verify_session()  → "Are you still logged in?"
auth_logout()          → Clean exit
```
- `auth_login()` - Called from UI login form
- `auth_verify_session()` - Called on UI operations
- `auth_logout()` - Called on UI logout
(The People)
| Owner | Purpose |
|-------|---------|
| `Backend/patient_manager.c` | 📋 Register, search, update, archive |

**Talks to:**
- `UI/patient_form.c` ← patient dialogs (TODO)
- `Backend/hl7_parser.c` → read/write HL7 format
- `Backend/utils.c` → validation & file operations
- `Backend/audit_logger.c` → track who changed what
- `Data/patients/*.seg` ← where records live

**Key Functions:**
```
patient_create()          → Register new patient
patient_search_by_name()  → Find patient by name
patient_search_by_id()    → Find patient by ID
patient_read()            → Load full record
patient_update_info()     → Edit patient details
```

**Data Stored As:** HL7 segments in `.seg` files
- PID = Demographics (name, DOB, address)
- OBX = Vitals & test results
- HL7 PID segment (demographics)
- HL7 OBX segments (vitals/test results)
- Files: `Data/patients/{patient_id}.seg`

---

### 📅 Appointment Management (The Schedule)
| Owner | Purpose |
|-------|---------|
| `Backend/appointment_manager.c` | 🗓️ Book, reschedule, cancel |

**Talks to:**
- `UI/appointment_form.c` ← appointment dialogs (TODO)
- `Backend/patient_manager.c` → "Does this patient exist?"
- `Backend/hl7_parser.c` → read/write SCH segments
- `Backend/audit_logger.c` → log scheduling changes
- `Data/appointments/*.seg` ← appointment records

**Key Functions:**
```
book_appointment()       → Create new appointment
reschedule_appointment() → Change date/time/doctor
cancel_appointment()     → Mark as cancelled
view_appointments()      → List all appointments
```

**Appointment Status:** `PENDING` → `CONFIRMED` → `COMPLETED` or `CANCELLED`

**Data Stored As:** HL7 Schedule (SCH) segments

---

### 💳 Billing/Invoice Feature
**Responsible  & Invoices (The Money)
| Owner | Purpose |
|-------|---------|
| `Backend/billing_manager.c` | 💰 Create invoices, track payments |

**Talks to:**
- `UI/billing_form.c` ← invoice dialogs (TODO)
- `UI/reports_form.c` ← billing reports (TODO)
- `Backend/patient_manager.c` → "Which patient?"
- `Backend/hl7_parser.c` → read/write UB1 segments
- `Backend/audit_logger.c` → log payment changes
- `Data/backups/` ← invoice records

**Key Functions:**
```
create_invoice()         → Generate new bill
update_invoice_status()  → Track payment progress
get_invoice()            → Retrieve invoice details
```

**Payment Status:** `PENDING` → `PARTIAL` → `PAID`

**Data Stored As:** HL7 Billing (UB1) segments
---

### 🔍 Audit Logging Feature
**Responsible Module:** `Backend/audit_logger.c|h`
Passive listener - lo(Who Did What?)
| Owner | Purpose |
|-------|---------|
| `Backend/audit_logger.c` | 📝 Silent witness to everything |

**Calls from:** Every other backend module
**Stores in:** `Data/audit_logs/*.log`
**Viewed by:** `UI/reports_form.c` (TODO)

**Key Function:**
```
audit_log() → Records: timestamp, username, operation, changes
```
*This runs quietly in the background — everything gets logged for compliance* ✓

## File Dependencies Graph

```
🎨 UI Layer (What Users See)
├─ 🛠️ ui_utils ─────────→ GTK+ library (SHARED: used by all UI forms)
│  ├─ Dialog functions: 6/6 ✅ (show_info, show_error, show_confirmation, show_input, masked input)
│  ├─ Validation ready: 7 functions
│  ├─ Widget helpers ready: 8 functions
│  └─ Layout builders ready: 6 functions
├─ 🪟 main_window ──────── Everyone's boss, talks to ALL backends
├─ 🔐 auth_form ─────────→ auth_manager
├─ 👥 patient_form ──────→ patient_manager
├─ 📅 appointment_form ──→ appointment_manager
├─ 💳 billing_form ──────→ billing_manager
└─ 📊 reports_form ──────→ Everyone (for reports)

🔧 Backend Logic (The Brain)
├─ 🔐 auth_manager ──────→ utils (hash passwords)
├─ 👥 patient_manager ──→ hl7_parser + utils
├─ 📅 appointment_manager → patient_manager + hl7_parser + utils
├─ 💳 billing_manager ──→ patient_manager + hl7_parser + utils
└─ 🔍 audit_logger ◀─── CALLED BY ALL (silent logging)

💾 HL7 Data Parser
└─ hl7_parser ──────────→ utils

🌐 Data Storage
├─ Data/patients/*.seg ◀─ patient_manager
├─ Data/appointments/*.seg ◀─ appointment_manager
├─ Data/backups/*.seg ◀─ billing_manager
├─ Data/audit_logs/*.log ◀─ audit_logger
├─ Data/sessions/*.token ◀─ auth_manager
└─ Data/config/credentials.db ◀─ auth_manager
```

---

## 🔀 Cross-Module Communication (How Data Flows)

### 🔗 The Patient-Appointment-Billing Chain
The classic workflow:
```
1️⃣ Register patient
   patient_manager.patient_create() → generates unique patient_id
                                    ↓
2️⃣ Book appointment for patient
   appointment_manager.book_appointment(patient_id)
   "Does patient exist?" ← asks patient_manager
                       ↓
3️⃣ Create invoice after service
   billing_manager.create_invoice(patient_id)
   "Link charges to this patient"
                       ↓
🎯 Everything logged by audit_logger!
```

### ✔️ The Validation Chain
Every operation goes through the same sieve:
```
User types something into UI
         ↓
Main program calls backend function
         ↓
utils.validate_input() checks it
         ↓
Man🚀 Build Order: Which to Code First?BLOCKS all UI features)
3. `auth_form.c|h` - Login (BLOCKS app access)

**Phase 2 (Core Features):**
4. `patient_form.c|h` - Patient management (highest impact)
5. `appointment_form.c|h` - Scheduling

**Phase 3 (Billing & Reporting):**
6. `billing_form.c|h` - Invoice management
7. `reports_form.c|h` - Analytics & export

---

## Data Flow Examples

### Example 1: Patient Lookup
```
UI:📖 Real-World Examples: Data in Motion

### Example 1: "I'm a New Patient"
```
UI patient_form
  ↓ User fills in name, DOB, phone, etc.
  ↓ Clicks "Register"
  ↓
patient_manager.patient_create()
  ├─ Validates all fields (via utils)
  ├─ Generates unique patient_id
  ├─ Creates HL7 PID segment
  ↓
Writes to: Data/patients/{patient_id}.seg
  ↓
audit_logger records
  └─ "User john_doe created patient P001"
  ↓
Returns patient_id to UI ✅ Success!
```

### Example 2: "Book Me an Appointment"
```
UI appointment_form
  ↓ User selects patient, date, time, doctor
  ↓ Clicks "Book"
  ↓
appointment_manager.book_appointment()
  ├─ Asks: "Does patient exist?"
  │  └─ patient_manager.patient_read(patient_id)
  ├─ Checks: "Any conflicts on that date/doctor?"
  ├─ Creates HL7 SCH segment
  ├─ Status: PENDING → CONFIRMED
  ↓
Writes to: Data/appointments/{apt_id}.seg
  ↓
audit_logger records
  └📂 Quick Reference: Who Owns What Data?oked"
  ↓
Re📍 Location | 🎯 Owner | 📋 What It Is | 🔧 Format |
|-----------|---------|-------------|----------|
| `credentials.db` | auth_manager 🔐 | User accounts & passwords | Binary DB |
| `patients/*.seg` | patient_manager 👥 | All patient info | HL7 Text |
| `appointments/*.seg` | appointment_manager 📅 | Scheduled appointments | HL7 Text |
| `backups/*.seg` | billing_manager 💳 | Invoice records | HL7 Text |
| `audit_logs/*.log` | audit_logger 🔍 | "Who did what when" | Text Log |
| `sessions/*.token` | auth_manager 🔐 | Active user sessions | JSON |
| `config/` | init_db.sh scripts | Settings & defaultsme()
  ├─ Reads all files in Data/patients/
  ├─ Parses each .seg file (hl7_parser)
  ├─ Extracts PID data (name, age, etc.)
  ↓
Returns list to UI
  ↓
patient_form displays in scrollable table ✅ Ready to click!

---

## 📂 Quick Reference: Who Owns What Data?

| 📍 Location | 🎯 Owner | 📋 What It Is | 🔧 Format |
|-----------|---------|-------------|----------|
| `credentials.db` | auth_manager 🔐 | User accounts & passwords | Binary DB |
| `patients/*.seg` | patient_manager 👥 | All patient info | HL7 Text |
| `appointments/*.seg` | appointment_manager 📅 | Scheduled appointments | HL7 Text |
| `backups/*.seg` | billing_manager 💳 | Invoice records | HL7 Text |
| `audit_logs/*.log` | audit_logger 🔍 | "Who did what when" | Text Log |
| `sessions/*.token` | auth_manager 🔐 | Active user sessions | JSON |
| `config/` | init_db.sh scripts | Settings & defaults | Various |
