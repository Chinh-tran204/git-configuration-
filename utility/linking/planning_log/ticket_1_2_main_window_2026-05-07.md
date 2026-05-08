# Plan: Create Main Window Module

Date: 2026-05-07

## Summary
Build the central GTK+ application window that serves as the hub for all UI modules. This window provides navigation via menu bar and tabs, session management, and user role display. It acts as the main dispatcher between all other UI forms.

## Plan

1. **Design Module Architecture**
   - Define `main_window.h` structure: GTK application, window widget, menu bar, notebook (tabs), status bar
   - Define function signatures for initialization, menu creation, tab management, cleanup
   - Plan integration points with `auth_manager.c` for session validation

2. **Implement GTK+ Foundation**
   - Create GTK application instance
   - Create main window widget with title, size, position
   - Connect window close/destroy signals to proper handlers
   - Implement `main_window_init()` and `main_window_cleanup()`

3. **Build Menu Bar**
   - Create menu bar widget in main window
   - Implement File menu (Logout, Exit callbacks)
   - Implement Tools menu (placeholder items)
   - Implement Help menu (About, placeholder items)
   - Connect menu item signals to corresponding callbacks

4. **Create Tabbed Interface (Notebook)**
   - Add GTK Notebook widget as main content area
   - Reserve tab slots for: Patients, Appointments, Billing, Audit Logs, Users (admin), Settings (admin)
   - Use placeholder labels/widgets for each tab initially
   - Implement tab switching and visibility logic

5. **Integrate Session Management**
   - Call `auth_manager.c: get_user_info()` after login to retrieve username and role
   - Store session token in main_window structure
   - Validate session on window focus or at intervals
   - Implement session expiry handlers

6. **Implement Logout & Exit Flow**
   - Show confirmation dialog on logout/exit
   - Call cleanup functions for active modules
   - Call `auth_manager.c: logout()` to invalidate session
   - Clear session data and return to login window

7. **Display User Information**
   - Add status bar to show username and role
   - Update window title with application name and username
   - Show role-dependent UI elements (e.g., hide admin tabs from users)

8. **Verification & Testing**
   - Verify GTK+ window initializes without crashes
   - Test menu callbacks execute
   - Test tab switching
   - Test logout clears session and returns to login

## Current Step
1

---
