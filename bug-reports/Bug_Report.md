# Bug Report — OrangeHRM Manual Testing Project

**Project:** OrangeHRM Manual Testing  
**Reported By:** [Jayanta Das]  
**Testing Period:** March 10 – March 28, 2025  
**Total Bugs:** 15  
**Critical:** 2 | **High:** 5 | **Medium:** 6 | **Low:** 2  
**Application URL:** https://opensource-demo.orangehrmlive.com  
**Environment:** Chrome 123.0 / Windows 11

---

## Bug Summary Table

| Bug ID | Title | Module | Severity | Priority | Status |
|---|---|---|---|---|---|
| BUG_001 | Forgot password shows success for non-existent username | Login | Medium | P3 | Open |
| BUG_002 | No account lockout after repeated failed login attempts | Login | Critical | P1 | Open |
| BUG_003 | Time at Work widget shows zero without any indicator | Dashboard | Low | P4 | Open |
| BUG_004 | Search results not cleared when Reset is clicked on specific filter combos | PIM | Medium | P3 | Open |
| BUG_005 | Employee ID field accepts special characters | PIM | High | P2 | Open |
| BUG_006 | Duplicate employee ID error message not descriptive | PIM | Medium | P3 | Open |
| BUG_007 | Leave application allowed for past dates without warning | Leave | High | P2 | Open |
| BUG_008 | Overlapping leave dates not validated on front end | Leave | Critical | P1 | Open |
| BUG_009 | Leave balance shows stale data after entitlement changes | Leave | Medium | P3 | Open |
| BUG_010 | Dashboard widget arrangement not preserved across sessions | Dashboard | Low | P4 | Open |
| BUG_011 | Phone number field accepts alphabetic characters | PIM | High | P2 | Open |
| BUG_012 | Apply button on Leave form active with empty mandatory fields | Leave | Medium | P3 | Open |
| BUG_013 | No session timeout warning before auto logout | General | Medium | P3 | Open |
| BUG_014 | Export shows 0 count in summary but exports full data | PIM | Medium | P3 | Open |

---

## Detailed Bug Reports

---

### BUG_001

**Bug ID:** BUG_001  
**Title:** Forgot password shows success message for non-existent username  
**Module:** Login  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 11, 2025  
**Status:** Open  
**Related Test Case:** TC_LGN_009  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

When a user enters a username that does not exist in the system on the "Forgot Password" / "Reset Password" page and clicks "Reset Password", the application displays the same success message ("Reset Password link sent successfully") as it would for a valid username. There is no differentiation between a valid and invalid username.

**Steps to Reproduce:**

1. Navigate to the login page: https://opensource-demo.orangehrmlive.com
2. Click on the "Forgot your password?" link below the login form
3. On the Reset Password page, enter `unknownuser99` in the Username field
4. Click **Reset Password**
5. Observe the message displayed

**Expected Result:**

Either a clear error message ("Username not found") or a consistent generic message — the key expectation is that the response doesn't actively confirm or deny account existence. However, if the message is generic (for security), that should be documented as intentional. Currently the message reads as a success when it isn't.

**Actual Result:**

Message displayed: "Reset Password link sent successfully." This is the same message shown for a valid user, making it impossible for a legitimate user to know whether their reset request was actually processed.

**Screenshots:** `screenshots/BUG_001_forgot_password_invalid_user.png`

**Impact:**

Users who mistype their username will believe a reset email is on the way, wait indefinitely, and then reach out to support — increasing support overhead. Medium impact on UX.

**Suggested Fix:**

Show a clear error for invalid usernames, or standardise to a generic message like: "If this username exists in our system, a password reset link has been sent to the associated email address." This improves both UX (honest) and security (doesn't confirm account existence).

---

### BUG_002

**Bug ID:** BUG_002  
**Title:** No account lockout after repeated failed login attempts  
**Module:** Login  
**Severity:** Critical  
**Priority:** P1 – Critical  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 11, 2025  
**Status:** Open  
**Related Test Case:** TC_LGN_010  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

The login page does not implement any account lockout, rate limiting, or CAPTCHA mechanism after multiple consecutive failed login attempts. An attacker can make unlimited login attempts without any automated protection.

**Steps to Reproduce:**

1. Navigate to https://opensource-demo.orangehrmlive.com
2. Enter username `Admin` and any incorrect password (e.g., `wrongpass1`)
3. Click Login — note the "Invalid credentials" error
4. Repeat with different incorrect passwords 10+ times in a row
5. Observe whether any lockout, CAPTCHA, or delay mechanism activates

**Expected Result:**

After 3–5 consecutive failed login attempts, one of the following should occur:
- Account is temporarily locked for a defined period (e.g., 15 minutes)
- A CAPTCHA challenge is presented to the user
- Login attempts are rate-limited with increasing delays
- An alert is sent to the account owner

**Actual Result:**

After 10+ failed attempts, the login page continued to accept attempts without any additional challenge, delay, or lockout. The same "Invalid credentials" message was shown each time.

**Screenshots:** `screenshots/BUG_002_no_lockout_after_10_attempts.png`

**Impact:**

**High security risk.** Without rate limiting or lockout, the login page is vulnerable to brute-force attacks. An automated script could systematically attempt passwords until the correct one is found. This is particularly critical for admin accounts.

**Suggested Fix:**

Implement account lockout after 5 failed attempts with a 15-minute cooldown. Alternatively, implement progressive delays (exponential backoff) or a CAPTCHA after 3 failed attempts. Send an email notification to the account owner when multiple failed attempts are detected.

---

### BUG_003

**Bug ID:** BUG_003  
**Title:** "Time at Work" dashboard widget shows 00:00 without explanation  
**Module:** Dashboard  
**Severity:** Low  
**Priority:** P4 – Low  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 12, 2025  
**Status:** Open  
**Related Test Case:** TC_DSH_004  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

The "Time at Work" widget on the Dashboard displays "00:00" at all times, even after the user has been logged in for several minutes. No indicator or help text explains why it shows zero or how to activate it. This is confusing for new users.

**Steps to Reproduce:**

1. Log in with valid credentials
2. Land on the Dashboard
3. Locate the "Time at Work" widget
4. Observe the time displayed — it reads "00:00"
5. Wait 5 minutes and refresh the page
6. Observe that the time still reads "00:00"

**Expected Result:**

The widget should either:
(a) Automatically track time from the moment of login, or
(b) Display a clear message: "No attendance punched in. Click here to punch in." with a direct action button

**Actual Result:**

Widget showed "00:00" with no explanation. A small sub-label reads "Current day's time" but gives no guidance on how to activate tracking.

**Screenshots:** `screenshots/BUG_003_time_widget_zero.png`

**Impact:**

Low functional impact. This is a UX issue that may confuse users unfamiliar with the punch-in system. Could lead to HR complaints about inaccurate time tracking if employees assume the widget auto-tracks from login.

**Suggested Fix:**

Add a helper message or a direct "Punch In" button inside the widget when no punch-in exists for the current day.

---

### BUG_005

**Bug ID:** BUG_005  
**Title:** Employee search results not cleared correctly when Reset is clicked with active Sub Unit filter  
**Module:** PIM – Employee Management  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 16, 2025  
**Status:** Open  
**Related Test Case:** TC_PIM_010  
**Browser/OS:** Firefox 124.0 / Windows 11

---

**Description:**

When the "Sub Unit" filter is selected along with a name filter and the user clicks Reset, the Sub Unit dropdown resets visually but the search results still appear to be filtered by sub unit. This behaviour was observed specifically on Firefox. Chrome did not show the same inconsistency.

**Steps to Reproduce:**

1. Navigate to PIM → Employee List on **Firefox**
2. Enter a partial name in the Employee Name field
3. Select a Sub Unit from the Sub Unit dropdown
4. Click Search — note the filtered results
5. Click Reset
6. Observe the results — the name field clears but the sub unit filter may still be applied to the displayed results

**Expected Result:**

All filters are cleared and the full unfiltered employee list is restored.

**Actual Result:**

On Firefox, the Sub Unit field appeared reset in the UI but the displayed results were still filtered. Only after clicking Search again (with empty fields) did the full list appear.

**Screenshots:** `screenshots/BUG_004_reset_subunit_filter_firefox.png`

**Impact:**

Medium — affects users on Firefox who may believe they're seeing all employees when they're actually seeing a filtered subset. Could lead to "missing employee" confusion.

**Suggested Fix:**

Ensure the Reset button triggers a complete state reset including all internal filter state, not just the visible UI state. After reset, auto-execute a fresh search query with no filters.

---

### BUG_006

**Bug ID:** BUG_006  
**Title:** Employee ID field accepts special characters without validation  
**Module:** PIM – Employee Management  
**Severity:** High  
**Priority:** P2 – High  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 16, 2025  
**Status:** Open  
**Related Test Case:** TC_PIM_005  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

The Employee ID field on the Add Employee page does not validate against special characters. Values like `EMP@#!001` are accepted and saved to the system. Employee IDs are often used as keys in reports, exports, and integrations, making this a data integrity concern.

**Steps to Reproduce:**

1. Navigate to PIM → Employee List → Add Employee
2. Enter a valid First and Last Name
3. Clear the auto-generated Employee ID
4. Type `EMP@#!001` in the Employee ID field
5. Click Save

**Expected Result:**

Validation error: "Employee ID can only contain alphanumeric characters."

**Actual Result:**

Employee was saved with ID `EMP@#!001`. No validation error.

**Screenshots:** `screenshots/BUG_005_employee_id_special_chars.png`

**Impact:**

High data integrity impact. Special characters in IDs can break CSV exports, database queries, URL parameters, and third-party integrations that use the Employee ID as a key.

**Suggested Fix:**

Add a regex validator on the Employee ID field: `^[a-zA-Z0-9-]*$` (allow alphanumeric and hyphen only). Show an inline validation error if the input doesn't match.

---

### BUG_007

**Bug ID:** BUG_007  
**Title:** Duplicate Employee ID error message is not descriptive  
**Module:** PIM – Employee Management  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 17, 2025  
**Status:** Open  
**Related Test Case:** TC_PIM_003  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

When an employee is saved with a duplicate Employee ID (one that already exists in the system), the error message shown is generic and doesn't clearly explain what went wrong.

**Steps to Reproduce:**

1. Navigate to PIM → Add Employee
2. Note the ID of any existing employee (e.g., `0001`)
3. Enter First/Last Name for a new employee
4. Manually set the Employee ID to `0001`
5. Click Save

**Expected Result:**

Error message: "Employee ID 0001 is already in use. Please enter a unique Employee ID."

**Actual Result:**

Error message: "Employee Id already exists" — technically correct but doesn't specify which ID is conflicting, making it slightly unclear for admins managing large employee lists.

**Screenshots:** `screenshots/BUG_006_duplicate_id_generic_error.png`

**Impact:**

Low–Medium. Minor UX issue, not a functionality failure. The error does prevent the duplicate from being saved.

**Suggested Fix:**

Improve the error message to include the ID that's conflicting: "Employee ID '0001' is already assigned. Please use a different ID."

---

### BUG_008

**Bug ID:** BUG_008  
**Title:** Leave application accepted for past dates without any warning  
**Module:** Leave Management  
**Severity:** High  
**Priority:** P2 – High  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 21, 2025  
**Status:** Open  
**Related Test Case:** TC_LVE_004  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

Employees can submit a leave application for dates that are entirely in the past without receiving any warning, confirmation prompt, or validation error. The application is created with "Pending Approval" status, the same as any other application.

**Steps to Reproduce:**

1. Log in and navigate to Leave → Apply
2. Select any leave type (e.g., Casual Leave)
3. Set From Date to 10 days ago (using the date picker)
4. Set To Date to 8 days ago
5. Add any comment
6. Click Apply

**Expected Result:**

A warning dialog or inline message should appear: "You are applying leave for dates in the past. Do you still want to proceed?" with Confirm and Cancel options. Alternatively, past-date leave could be blocked entirely with a message directing the user to contact HR directly.

**Actual Result:**

The application was accepted and submitted without any warning. Status showed as "Pending Approval."

**Screenshots:** `screenshots/BUG_007_past_date_leave_accepted.png`

**Impact:**

High. Employees can accidentally apply leave for wrong dates (especially likely when misreading the date format). Backdated leave can create payroll and compliance issues. HR would need to manually review all pending applications to catch this.

**Suggested Fix:**

Add a front-end check: if `From Date < today`, show a confirmation dialog before allowing the submission. Consider making the behaviour configurable — some organisations do allow backdated leave (e.g., sick leave after the fact).

---

### BUG_009

**Bug ID:** BUG_009  
**Title:** Overlapping leave date ranges not validated on the front end  
**Module:** Leave Management  
**Severity:** Critical  
**Priority:** P1 – Critical  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 22, 2025  
**Status:** Open  
**Related Test Case:** TC_LVE_006  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

When an employee submits a second leave application whose dates overlap with an already existing (pending or approved) leave application, the system does not warn the user or prevent the submission. Both applications are created successfully with overlapping date ranges.

**Steps to Reproduce:**

1. Submit a leave application for next Monday to Friday (Application A)
2. Navigate to Leave → Apply again
3. Submit a second application for next Wednesday to Friday (Application B — overlapping with A)
4. Navigate to My Leave List

**Expected Result:**

Step 3 should trigger a validation message: "You already have an existing leave application for some or all of these dates. Please review your leave list before applying."

**Actual Result:**

Application B was created without any error. Both applications now show in My Leave List with overlapping dates. An admin reviewing leave requests would have to manually identify and resolve the conflict.

**Screenshots:** `screenshots/BUG_008_overlapping_leave_accepted.png`

**Impact:**

**Critical.** Overlapping leave creates accounting discrepancies (employee can't be on leave twice for the same day), complicates payroll calculations, and puts burden on HR to manually detect and resolve conflicts. This is a core business logic failure.

**Suggested Fix:**

Before submitting a new leave application, check the employee's existing leave applications for date range conflicts. If a conflict is found, show a clear error: "You already have leave applied for [overlapping dates]. Please cancel the existing application before applying new leave."

---

### BUG_010

**Bug ID:** BUG_010  
**Title:** Leave balance shows stale data after leave type entitlement is updated  
**Module:** Leave Management  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 23, 2025  
**Status:** Open  
**Related Test Case:** TC_LVE_012  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

When an admin updates a user's leave entitlement and the employee immediately goes to Apply Leave, the balance displayed under the leave type reflects the old (pre-update) balance. A page refresh is required to see the updated balance.

**Steps to Reproduce:**

1. As Admin, navigate to Leave → Leave Entitlements
2. Update the Annual Leave entitlement for a user (e.g., from 14 to 20 days)
3. Save the change
4. Log in as the affected employee (or use the same session if testing as admin)
5. Go to Leave → Apply
6. Select Annual Leave
7. Observe the balance shown immediately

**Expected Result:**

The balance shown should immediately reflect the updated value (20 days).

**Actual Result:**

Balance still showed the old value (14 days) until the page was refreshed. After refresh, the new balance (20 days) appeared correctly.

**Screenshots:** `screenshots/BUG_009_stale_leave_balance.png`

**Impact:**

Medium. Users might see an incorrect balance and either under-apply (thinking they have less leave) or try to apply more leave than they believe they have. Shouldn't affect actual approval but creates confusion.

**Suggested Fix:**

Fetch the leave balance dynamically each time the leave type selection changes in the Apply Leave form, rather than using a cached value.

---

### BUG_011

**Bug ID:** BUG_011  
**Title:** Dashboard widget arrangement not preserved after logout and re-login  
**Module:** Dashboard  
**Severity:** Low  
**Priority:** P4 – Low  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 13, 2025  
**Status:** Open  
**Related Test Case:** N/A (found during exploratory testing)  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

The Dashboard allows users to rearrange widgets by dragging and dropping them. However, the new arrangement is not saved — after logging out and back in, the widgets return to their original default positions.

**Steps to Reproduce:**

1. Log in and go to the Dashboard
2. Drag and drop any widget to a different position on the Dashboard
3. Log out
4. Log in again
5. Observe the Dashboard widget positions

**Expected Result:**

Widget positions should be saved to the user's profile and persist across sessions.

**Actual Result:**

All widgets returned to their default positions after re-login. The user's customisation was lost.

**Screenshots:** `screenshots/BUG_010_widget_positions_not_saved.png`

**Impact:**

Low. Cosmetic/preference issue. Doesn't affect core functionality.

**Suggested Fix:**

Save widget positions to the user's profile or browser localStorage when they are rearranged. Reload saved positions on login.

---

### BUG_012

**Bug ID:** BUG_012  
**Title:** Phone number field in Contact Details accepts alphabetic characters  
**Module:** PIM – Employee Management  
**Severity:** High  
**Priority:** P2 – High  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 17, 2025  
**Status:** Open  
**Related Test Case:** TC_PIM_015  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

The Work Phone and Mobile fields in the employee Contact Details tab accept and save alphabetic characters without any validation. Phone number fields should only accept numeric digits along with standard formatting characters (+, -, (, )).

**Steps to Reproduce:**

1. Navigate to any employee profile in PIM
2. Click on the **Contact Details** tab
3. In the Work Phone field, type: `CALL-ME-MAYBE`
4. Click **Save**

**Expected Result:**

Validation error: "Please enter a valid phone number (digits only)."

**Actual Result:**

`CALL-ME-MAYBE` was accepted and saved as the Work Phone number. No error.

**Screenshots:** `screenshots/BUG_011_phone_accepts_alphabets.png`

**Impact:**

High data quality impact. Nonsensical phone numbers saved in the system make the data unreliable for HR operations, payroll, emergency contact lookup, and any system that integrates with employee contact data.

**Suggested Fix:**

Add input validation: allow only digits, spaces, hyphens, plus signs, and parentheses. Limit field length to 15 characters (international standard). Regex: `^[0-9+\-() ]{7,15}$`.

---

### BUG_013

**Bug ID:** BUG_013  
**Title:** Apply button on Leave form remains active when mandatory fields are empty  
**Module:** Leave Management  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 24, 2025  
**Status:** Open  
**Related Test Case:** TC_LVE_013  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

The "Apply" button on the Leave application form is always active (enabled) regardless of whether mandatory fields have been filled. Clicking it with empty fields does trigger validation messages, but the UX would be better if the button were disabled until minimum required fields are completed.

**Steps to Reproduce:**

1. Navigate to Leave → Apply
2. Do not fill any fields
3. Observe the Apply button — it is enabled
4. Click Apply
5. Observe the validation errors

**Expected Result:**

Apply button should be disabled (greyed out) with a tooltip "Please fill in all required fields" until Leave Type and date fields are filled.

**Actual Result:**

Apply button is always enabled. Clicking it shows validation errors, which works, but the initial state of an always-enabled button is misleading.

**Screenshots:** `screenshots/BUG_012_apply_button_always_enabled.png`

**Impact:**

Low UX issue. Not a functional bug. Current behaviour (showing validation on click) is acceptable as a fallback.

**Suggested Fix:**

Disable the Apply button initially. Enable it reactively when the Leave Type dropdown and both date fields have valid values.

---

### BUG_014

**Bug ID:** BUG_014  
**Title:** No session timeout warning before automatic logout  
**Module:** General / Security  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 26, 2025  
**Status:** Open  
**Related Test Case:** N/A (found during extended exploratory session)  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

The application automatically logs out the user after a period of inactivity, but no warning is shown before the timeout occurs. The user is abruptly redirected to the login page, and any unsaved work (e.g., a partially filled employee form) is lost.

**Steps to Reproduce:**

1. Log in as Admin
2. Open a form (e.g., Add Employee) and partially fill in some fields
3. Leave the browser idle for 15–20 minutes
4. Attempt to interact with the page

**Expected Result:**

A warning dialog should appear 2–3 minutes before the session expires: "Your session will expire in 2 minutes due to inactivity. Click OK to continue your session." If dismissed, the user is logged out gracefully with any form data preserved.

**Actual Result:**

No warning was shown. After inactivity, the user was silently redirected to the login page. Any unsaved form data was lost.

**Screenshots:** `screenshots/BUG_013_no_timeout_warning.png`

**Impact:**

Medium. Loss of unsaved work is frustrating for users filling in long forms (like detailed employee records). Could reduce data quality if users rush through forms to avoid timeouts.

**Suggested Fix:**

Implement a session expiry warning modal with a countdown timer. Include a "Keep me logged in" option that refreshes the session token.

---

### BUG_015

**Bug ID:** BUG_015  
**Title:** Export employee list shows "0 Records" in summary but exports full data  
**Module:** PIM – Employee Management  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]  
**Date Reported:** March 19, 2025  
**Status:** Open  
**Related Test Case:** TC_PIM_019  
**Browser/OS:** Chrome 123.0 / Windows 11

---

**Description:**

When using the Export functionality on the Employee List without applying any filters, the export confirmation message briefly shows "0 records exported" or the count doesn't match the actual data in the downloaded file. The downloaded CSV contains the correct full employee list, but the on-screen count is misleading.

**Steps to Reproduce:**

1. Navigate to PIM → Employee List
2. Do not apply any filters
3. Click the Export (download) button
4. Observe any confirmation message or record count shown before/after the download
5. Open the downloaded CSV and count the records

**Expected Result:**

The confirmation message or export summary should accurately reflect the number of records exported (e.g., "Exported 25 employees").

**Actual Result:**

The export confirmation briefly showed "0 records" before completing. The downloaded file contained all employee records correctly. The count display was misleading.

**Screenshots:** `screenshots/BUG_014_export_count_mismatch.png`

**Impact:**

Medium. Users might question the integrity of the export and re-run it multiple times, creating unnecessary load. The actual data in the file is correct, but the misleading count erodes trust in the feature.

**Suggested Fix:**

Fix the export summary logic to reflect the actual count of records written to the export file, not a pre-filter count that may be uninitialized.

---

*End of Bug Report*

---

## Bug Status Definitions

| Status | Meaning |
|---|---|
| Open | Bug has been reported and is awaiting fix |
| In Progress | Developer is actively working on it |
| Fixed | Fix has been applied, awaiting re-test |
| Closed | Verified fixed and closed |
| Rejected | Not a valid bug (by design or misidentified) |
| Deferred | Acknowledged but postponed to a future release |
