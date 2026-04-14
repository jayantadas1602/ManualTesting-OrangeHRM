# Test Cases — Module 01: Login & Authentication

**Module:** Login & Authentication  
**Tester:** [Your Name]  
**Execution Date:** March 10–11, 2025  
**Browser:** Chrome 123.0 (primary), Firefox 124.0 (cross-check)  
**Application URL:** https://opensource-demo.orangehrmlive.com  
**Total Test Cases:** 12  
**Pass:** 9 | **Fail:** 2 | **Blocked:** 1

---

## Summary

The login module was the first area tested. The standard positive and negative flows work correctly for the most part, but there are two notable gaps — no account lockout after repeated failed attempts (a security concern raised as BUG_002) and the forgot password feature can't be fully tested on the demo environment since it relies on a real email server.

One interesting observation: the error messages on login failure are generic ("Invalid credentials"), which is actually good security practice — it doesn't tell an attacker whether the username or password was wrong.

---

## Test Cases

---

### TC_LGN_001 — Valid login with correct credentials

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_001 |
| **Title** | Verify successful login with valid admin credentials |
| **Module** | Login |
| **Priority** | P1 – Critical |
| **Prerequisites** | Browser is open, application URL is loaded |
| **Test Data** | Username: `Admin` Password: `admin123` |

**Steps:**

1. Navigate to https://opensource-demo.orangehrmlive.com
2. Observe the login page loads with Username and Password fields visible
3. Enter `Admin` in the Username field
4. Enter `admin123` in the Password field
5. Click the **Login** button

**Expected Result:** User is successfully logged in and redirected to the Dashboard page. The dashboard displays the OrangeHRM logo, navigation menu, and welcome message.

**Actual Result:** User logged in successfully. Dashboard loaded with navigation menu, widgets, and header with admin username displayed.

**Status:** ✅ Pass

**Remarks:** Login took approximately 1–2 seconds. No delay issues observed.

---

### TC_LGN_002 — Invalid login with wrong password

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_002 |
| **Title** | Verify login fails with correct username and incorrect password |
| **Module** | Login |
| **Priority** | P1 – Critical |
| **Prerequisites** | Browser is on the login page, not logged in |
| **Test Data** | Username: `Admin` Password: `wrongpassword123` |

**Steps:**

1. Navigate to the login page
2. Enter `Admin` in the Username field
3. Enter `wrongpassword123` in the Password field
4. Click the **Login** button

**Expected Result:** Login is rejected. An error message is displayed (e.g., "Invalid credentials"). User remains on the login page.

**Actual Result:** Error message "Invalid credentials" appeared below the login form in red. User was not logged in and remained on the login page.

**Status:** ✅ Pass

**Remarks:** Error message is appropriately generic — does not reveal whether the username or password was incorrect. This is a security best practice.

---

### TC_LGN_003 — Invalid login with wrong username

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_003 |
| **Title** | Verify login fails with incorrect username and correct password |
| **Module** | Login |
| **Priority** | P1 – Critical |
| **Prerequisites** | Browser is on the login page |
| **Test Data** | Username: `wronguser` Password: `admin123` |

**Steps:**

1. Navigate to the login page
2. Enter `wronguser` in the Username field
3. Enter `admin123` in the Password field
4. Click the **Login** button

**Expected Result:** Login is rejected with an error message. User remains on the login page.

**Actual Result:** Error message "Invalid credentials" was displayed. User not logged in.

**Status:** ✅ Pass

**Remarks:** Same generic error as TC_LGN_002 — consistent behaviour.

---

### TC_LGN_004 — Invalid login with both fields incorrect

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_004 |
| **Title** | Verify login fails when both username and password are incorrect |
| **Module** | Login |
| **Priority** | P2 – High |
| **Prerequisites** | Browser is on the login page |
| **Test Data** | Username: `fakeuser` Password: `fakepass` |

**Steps:**

1. Navigate to the login page
2. Enter `fakeuser` in Username
3. Enter `fakepass` in Password
4. Click **Login**

**Expected Result:** Login rejected. Error message shown. User stays on login page.

**Actual Result:** Behaved as expected. Same "Invalid credentials" message shown.

**Status:** ✅ Pass

---

### TC_LGN_005 — Login with empty Username field

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_005 |
| **Title** | Verify validation error when username is left empty |
| **Module** | Login |
| **Priority** | P2 – High |
| **Prerequisites** | Browser is on the login page |
| **Test Data** | Username: *(empty)* Password: `admin123` |

**Steps:**

1. Navigate to the login page
2. Leave the Username field blank
3. Enter `admin123` in the Password field
4. Click the **Login** button

**Expected Result:** Validation error displayed below the Username field (e.g., "Required"). Login should not proceed.

**Actual Result:** Validation message "Required" appeared below the Username field. Login did not proceed.

**Status:** ✅ Pass

---

### TC_LGN_006 — Login with empty Password field

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_006 |
| **Title** | Verify validation error when password is left empty |
| **Module** | Login |
| **Priority** | P2 – High |
| **Prerequisites** | Browser is on the login page |
| **Test Data** | Username: `Admin` Password: *(empty)* |

**Steps:**

1. Navigate to the login page
2. Enter `Admin` in the Username field
3. Leave the Password field blank
4. Click the **Login** button

**Expected Result:** Validation message "Required" shown below the Password field. Login does not proceed.

**Actual Result:** As expected. Validation triggered. Login blocked.

**Status:** ✅ Pass

---

### TC_LGN_007 — Login with both fields empty

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_007 |
| **Title** | Verify validation errors when both fields are empty |
| **Module** | Login |
| **Priority** | P2 – High |
| **Prerequisites** | Browser is on the login page |
| **Test Data** | Username: *(empty)* Password: *(empty)* |

**Steps:**

1. Navigate to the login page
2. Leave both fields empty
3. Click the **Login** button

**Expected Result:** Validation errors displayed under both fields. Login does not proceed.

**Actual Result:** Both "Required" messages displayed simultaneously under each field.

**Status:** ✅ Pass

---

### TC_LGN_008 — Forgot password link is present and navigates correctly

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_008 |
| **Title** | Verify "Forgot your password?" link is visible and functional |
| **Module** | Login |
| **Priority** | P3 – Medium |
| **Prerequisites** | Browser is on the login page |
| **Test Data** | N/A |

**Steps:**

1. Navigate to the login page
2. Locate the "Forgot your password?" link below the login form
3. Click the link

**Expected Result:** User is navigated to a password reset page where they can enter their username to receive a reset link.

**Actual Result:** Clicking the link navigated to the "Reset Password" page. A Username field was presented with a "Reset Password" button.

**Status:** ✅ Pass

**Remarks:** End-to-end password reset flow could not be verified since the demo does not send real emails. See TC_LGN_009 for partial validation.

---

### TC_LGN_009 — Forgot password flow with unregistered email

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_009 |
| **Title** | Verify forgot password with unregistered username shows appropriate message |
| **Module** | Login |
| **Priority** | P3 – Medium |
| **Prerequisites** | User is on the "Reset Password" page |
| **Test Data** | Username: `unknownuser99` |

**Steps:**

1. Navigate to the Reset Password page via the "Forgot your password?" link
2. Enter `unknownuser99` in the Username field
3. Click **Reset Password**

**Expected Result:** System should show a message indicating either that the user was not found, or a generic success message ("If this account exists, a reset link has been sent") — the latter being more secure.

**Actual Result:** A success-style message "Reset Password link sent successfully" was displayed even for a non-existent username. This is misleading — there is no visual distinction between a valid and invalid username submission.

**Status:** ❌ Fail

**Bug Reference:** BUG_001

**Remarks:** This is a low-severity issue, but worth noting for UX improvement. A better approach would be to silently process the request without confirming or denying whether the username exists.

---

### TC_LGN_010 — Account lockout after multiple failed login attempts

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_010 |
| **Title** | Verify account gets locked after repeated failed login attempts |
| **Module** | Login |
| **Priority** | P1 – Critical |
| **Prerequisites** | Browser is on the login page |
| **Test Data** | Username: `Admin` Password: `wrongpass` (repeated 10 times) |

**Steps:**

1. Navigate to the login page
2. Enter `Admin` as username and `wrongpass` as password
3. Click Login — note the error message
4. Repeat steps 2–3 a total of 10 times
5. Observe whether any lockout mechanism activates (CAPTCHA, temporary block, warning message)

**Expected Result:** After a defined number of failed attempts (typically 3–5), the account should be temporarily locked or a CAPTCHA should be triggered to prevent brute-force attacks.

**Actual Result:** No lockout occurred after 10 consecutive failed attempts. Login continued to accept attempts without any rate limiting, CAPTCHA, or warning.

**Status:** ❌ Fail

**Bug Reference:** BUG_002

**Remarks:** This is a **Critical** security gap. Without account lockout or rate limiting, the login page is vulnerable to brute-force attacks. This should be addressed as a high priority.

---

### TC_LGN_011 — SQL injection attempt in username field

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_011 |
| **Title** | Verify application is protected against basic SQL injection in login |
| **Module** | Login |
| **Priority** | P2 – High |
| **Prerequisites** | Browser is on the login page |
| **Test Data** | Username: `' OR '1'='1` Password: `anything` |

**Steps:**

1. Navigate to the login page
2. Enter `' OR '1'='1` in the Username field
3. Enter any value in the Password field
4. Click **Login**

**Expected Result:** Application rejects the input. No unauthorized access is granted. An "Invalid credentials" error is shown or the input is sanitised.

**Actual Result:** Application returned "Invalid credentials" without any server-side error or unauthorized access. SQL injection attempt was handled correctly.

**Status:** ✅ Pass

**Remarks:** Application appears to use parameterised queries or an ORM, which protects against basic SQL injection. Good.

---

### TC_LGN_012 — Logout functionality

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_012 |
| **Title** | Verify user can successfully log out from the application |
| **Module** | Login |
| **Priority** | P1 – Critical |
| **Prerequisites** | User is logged in as Admin |
| **Test Data** | N/A |

**Steps:**

1. Log in with valid credentials (Admin / admin123)
2. Observe the top-right corner of the screen for the user profile dropdown
3. Click on the profile/avatar icon (displays "Admin")
4. Click **Logout** from the dropdown menu
5. Observe what happens

**Expected Result:** User is logged out and redirected to the login page. The back button should not allow the user to navigate back to the authenticated pages.

**Actual Result:** User was logged out and redirected to the login page. Pressing the back button in the browser did not reveal protected pages — the login page was displayed again.

**Status:** ✅ Pass

**Remarks:** Session termination on logout is correctly implemented.

---

### TC_LGN_013 — [BLOCKED] Password reset email delivery

| Field | Details |
|---|---|
| **Test Case ID** | TC_LGN_013 |
| **Title** | Verify password reset email is received after reset request |
| **Module** | Login |
| **Priority** | P2 – High |
| **Prerequisites** | User has a valid account with a configured email address |
| **Test Data** | Username: `Admin` |

**Steps:**

1. Navigate to the Reset Password page
2. Enter `Admin` as the username
3. Click **Reset Password**
4. Check the registered email inbox for a reset link

**Expected Result:** An email containing a password reset link is received within 5 minutes.

**Actual Result:** ⛔ Blocked — the demo environment does not have a configured email server. The reset email cannot be received or verified.

**Status:** ⛔ Blocked

**Remarks:** This test case is blocked due to a known demo environment limitation. In a production environment, this would be tested end-to-end with a real inbox.

---

*End of Login Module Test Cases*
