# Bug Report — OrangeHRM Manual Testing Project

**Project:** OrangeHRM Manual Testing  
**Reported By:** [Jayanta Das]       
**Total Bugs:** 7  
**Critical:** 1 | **High:** 1 | **Medium:** 3 | **Low:** 2  
**Application URL:** https://opensource-demo.orangehrmlive.com  
**Environment:** Chrome 123.0 / Windows 11

---

## Bug Summary Table

| Bug ID | Title | Module | Severity | Priority | Status |
|---|---|---|---|---|---|
| BUG_001 | Forgot password shows success for non-existent username | Login | Medium | P3 | Open |
| BUG_002 | No account lockout after repeated failed login attempts | Login | Critical | P1 | Open |
| BUG_003 | Time at Work widget shows zero without any indicator | Dashboard | Low | P4 | Open |
| BUG_004 | Employee ID field accepts special characters | PIM | High | P2 | Open |
| BUG_005 | Duplicate employee ID error message not descriptive | PIM | Medium | P3 | Open |
| BUG_006 | Dashboard widget arrangement not preserved across sessions | Dashboard | Low | P4 | Open |
| BUG_007 | No session timeout warning before auto logout | General | Medium | P3 | Open |


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

### BUG_004

**Bug ID:** BUG_004  
**Title:** Employee ID field accepts special characters without validation  
**Module:** PIM – Employee Management  
**Severity:** High  
**Priority:** P2 – High  
**Reported By:** [Jayanta Das]  
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

**Screenshots:** `screenshots/BUG_004_employee_id_special_chars.png`

**Impact:**

High data integrity impact. Special characters in IDs can break CSV exports, database queries, URL parameters, and third-party integrations that use the Employee ID as a key.

**Suggested Fix:**

Add a regex validator on the Employee ID field: `^[a-zA-Z0-9-]*$` (allow alphanumeric and hyphen only). Show an inline validation error if the input doesn't match.

---

### BUG_005

**Bug ID:** BUG_005  
**Title:** Duplicate Employee ID error message is not descriptive  
**Module:** PIM – Employee Management  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]  
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

**Screenshots:** `screenshots/BUG_005_duplicate_id_generic_error.png`

**Impact:**

Low–Medium. Minor UX issue, not a functionality failure. The error does prevent the duplicate from being saved.

**Suggested Fix:**

Improve the error message to include the ID that's conflicting: "Employee ID '0001' is already assigned. Please use a different ID."

---

### BUG_006

**Bug ID:** BUG_006 
**Title:** Dashboard widget arrangement not preserved after logout and re-login  
**Module:** Dashboard  
**Severity:** Low  
**Priority:** P4 – Low  
**Reported By:** [Jayanta Das]   
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

**Screenshots:** `screenshots/BUG_006_widget_positions_not_saved.png`

**Impact:**

Low. Cosmetic/preference issue. Doesn't affect core functionality.

**Suggested Fix:**

Save widget positions to the user's profile or browser localStorage when they are rearranged. Reload saved positions on login.

---

### BUG_007

**Bug ID:** BUG_007
**Title:** No session timeout warning before automatic logout  
**Module:** General / Security  
**Severity:** Medium  
**Priority:** P3 – Medium  
**Reported By:** [Jayanta Das]    
**Status:** Open  
**Related Test Case:** N/A (found during exploratory session)  
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

**Screenshots:** `screenshots/BUG_007_no_timeout_warning.png`

**Impact:**

Medium. Loss of unsaved work is frustrating for users filling in long forms (like detailed employee records). Could reduce data quality if users rush through forms to avoid timeouts.

**Suggested Fix:**

Implement a session expiry warning modal with a countdown timer. Include a "Keep me logged in" option that refreshes the session token.

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
