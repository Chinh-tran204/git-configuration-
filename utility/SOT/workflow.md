# Hospital Management System - Workflows

## 1. Authentication Flow

```
User Input (UI) → Login Form
        ↓
auth_login(username, password) [backend]
        ↓
Hash password & compare with credentials.db
        ↓
Success: Create SessionInfo (token, role, timeout)
         Store session in Data/sessions/
         Return token to UI
         
Fail: Return error code
      Show login error message
```

**Key Components:**
- Role-based access: ADMIN vs USER
- Session timeout: 8 hours
- Token validation: auth_verify_session()
- Audit logging: every login/logout

---

## 2. Patient Management Flow

```
Create Patient:
  UI patient_form → patient_create()
    ↓ Create HL7 PID segment
    ↓ Generate patient_id
    ↓ Write to Data/patients/{id}.seg
    ↓ Log to audit_logs
    └→ Return to UI

View/Search Patient:
  UI search input → patient_search_by_name/id()
    ↓ Read .seg files from Data/patients/
    ↓ Parse HL7 records
    ↓ Display in table
    
Update Patient:
  UI edit form → patient_update_info()
    ↓ Load existing .seg
    ↓ Modify field
    ↓ Rewrite .seg file
    ↓ Log change to audit_logs
    ↓ Return status
```

**Data Format:** HL7 PID segments stored as .seg files
**Audit:** All changes logged with username, timestamp, field changes

---

## 3. Appointment Management Flow

```
Book Appointment:
  UI appointment_form (patient_id, date/time, doctor)
    ↓
  appointment_manager.book_appointment()
    ↓ Validate patient exists (patient_manager)
    ↓ Check no conflicts in schedule
    ↓ Create HL7 SCH segment
    ↓ Store in Data/appointments/{apt_id}.seg
    ↓ Log to audit_logs
    ↓ Return confirmation
    
Reschedule/Cancel:
  Similar flow with:
    update_appointment() or cancel_appointment()
    Modify SCH status: PENDING → CONFIRMED → COMPLETED/CANCELLED
    Log all changes
```

**Schedule Conflict Detection:**
- Doctor availability
- Patient availability
- Resource availability

**Status Transitions:** PENDING → CONFIRMED → COMPLETED or CANCELLED

---

## 4. Billing/Invoice Flow

```
Create Invoice:
  UI billing_form (patient_id, procedures, amount)
    ↓
  billing_manager.create_invoice()
    ↓ Validate patient exists
    ↓ Calculate charges
    ↓ Create HL7 UB1 segment
    ↓ Store invoice (Data/backups/ or custom)
    ↓ Log to audit_logs
    ↓ Return invoice_id
    
Track Payment:
  UI update payment status
    ↓ Update invoice status: PENDING → PARTIAL → PAID
    ↓ Log transaction
    
Generate Report:
  Aggregate invoices by patient/date/status
    ↓ Display in reports_form
```

**Invoice States:** Pending → Partial Payment → Paid

---

## 5. Audit Logging Flow

```
Every operation (patient, appointment, billing, auth):
  1. Operation completes
  2. audit_logger logs:
     - Username (from session)
     - Timestamp
     - Operation type (CREATE/UPDATE/DELETE)
     - Entity ID
     - Field changes (old → new)
     - Result status (success/fail)
  3. Write to Data/audit_logs/
  4. Maintain for compliance
```

---

## 6. UI Application Lifecycle

```
Application Start
  ↓
Display Login Form (auth_form)
  ↓
User Login
  ↓
Create Session (backend auth_manager)
  ↓
Load Main Window (main_window)
  ├── Render tabs based on role
  │   ├── USER: Patients, My Appointments, Invoices
  │   └── ADMIN: All above + Reports, Audit, User Mgmt
  │
  └── Tabs mapped to forms:
      ├── patient_form
      ├── appointment_form
      ├── billing_form
      └── reports_form
  ↓
User Actions → Backend Calls → Data Updates → UI Refresh
  ↓
User Logout → Destroy Session → Back to Login
```

---

## 7. Data Backup & Recovery

```
Backup Flow (Scripts/backup.sh):
  1. Archive Data/patients/, appointments/, invoices
  2. Compress with timestamp
  3. Store in Data/backups/
  
Restore Flow (Scripts/restore.sh):
  1. List available backups
  2. User selects backup
  3. Extract and restore to Data/
  4. Verify integrity
```

---

## 8. System Maintenance

```
Init Flow (Scripts/init_db.sh):
  1. Create directory structure
  2. Initialize credentials.db with admin user
  3. Set up default configurations
  
Maintenance Flow (Scripts/maintenance.sh):
  1. Archive old audit logs
  2. Cleanup expired sessions
  3. Defragment data files
  4. Generate health report
```

---

## Module Interaction Matrix

| From | To | Function | Data |
|------|-----|----------|------|
| UI auth_form | auth_manager | auth_login() | username, password |
| UI patient_form | patient_manager | patient_create() | demographics |
| UI patient_form | patient_manager | patient_search_by_name() | search query |
| patient_manager | hl7_parser | Parse PID segments | HL7 data |
| UI appointment_form | appointment_manager | book_appointment() | patient_id, date/time |
| appointment_manager | patient_manager | Validate patient | patient_id |
| UI billing_form | billing_manager | create_invoice() | charges data |
| Any Backend | audit_logger | Log operation | operation details |
| Any Backend | utils | validate_input() | user input |
