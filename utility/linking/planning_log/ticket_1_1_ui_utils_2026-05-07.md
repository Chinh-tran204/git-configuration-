# Plan: Create UI Utilities Module

Date: 2026-05-07

## Summary
Build foundational GTK+ utility library for common UI operations. This module provides reusable components and helpers that all other UI forms will depend on: dialogs, form validation, layout helpers, and widget wrappers. Foundation for entire UI layer.

## Plan

1. **Design Module Header (ui_utils.h)**
   - Define dialog function signatures: `show_info_dialog()`, `show_error_dialog()`, `show_confirmation_dialog()`
   - Define form validation functions: `validate_text_entry()`, `validate_email()`, `validate_phone()`, `validate_date()`
   - Define layout helpers: `create_vbox()`, `create_hbox()`, `create_grid()`
   - Define widget wrappers: `create_text_entry()`, `create_button()`, `create_label()`
   - Include GTK headers and helper structures

2. **Implement Dialog Functions**
   - Implement `show_info_dialog(parent_window, title, message)` - informational modal
   - Implement `show_error_dialog(parent_window, title, error_message)` - error reporting modal
   - Implement `show_confirmation_dialog(parent_window, title, question)` - returns YES/NO/CANCEL
   - Set modal behavior and proper parent-child relationships

3. **Implement Form Validation Utilities**
   - Implement `validate_text_entry(text, min_len, max_len, regex_pattern)` - general text validation
   - Implement `validate_email(email_string)` - email format check
   - Implement `validate_phone(phone_string)` - phone number format check
   - Implement `validate_date(date_string, format)` - date format and range validation
   - Return validation status and error messages

4. **Implement Layout Helper Functions**
   - Implement `create_vbox(spacing, margin)` - returns packed vertical box container
   - Implement `create_hbox(spacing, margin)` - returns packed horizontal box container
   - Implement `create_grid(rows, cols, row_spacing, col_spacing)` - returns grid layout
   - Set standard defaults for consistent UI appearance

5. **Implement Widget Wrapper Functions**
   - Implement `create_text_entry(placeholder, max_len, is_password)` - text input wrapper
   - Implement `create_button(label, callback, data)` - button wrapper with signal connection
   - Implement `create_label(text, markup, alignment)` - label wrapper with formatting
   - Implement `add_widget_to_container()` - consistent widget packing helper

6. **Add Helper Utilities**
   - Implement `clear_container(container)` - remove all child widgets
   - Implement `get_text_entry_contents()` - safe text extraction
   - Implement `set_widget_enabled()` - enable/disable widget state
   - Implement `get_selected_combo_item()` - combo box helper

7. **Code Organization & Dependencies**
   - Include proper GTK+ 3.0 headers
   - Use consistent naming conventions
   - Add documentation comments for all functions
   - Avoid external dependencies beyond GTK+

8. **Verification & Testing**
   - Verify header compiles without errors
   - Test dialog creation and display
   - Test validation functions with edge cases (empty, special chars, boundary values)
   - Test layout creation and widget packing
   - Verify no memory leaks in dialog cleanup
---
