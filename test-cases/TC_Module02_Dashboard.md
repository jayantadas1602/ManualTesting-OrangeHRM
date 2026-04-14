# Test Cases — Module 02: Dashboard

**Module:** Dashboard  
**Tester:** [Your Name]  
**Execution Date:** March 12–13, 2025  
**Browser:** Chrome 123.0 (primary), Firefox 124.0 (cross-check)  
**Application URL:** https://opensource-demo.orangehrmlive.com  
**Total Test Cases:** 8  
**Pass:** 7 | **Fail:** 1 | **Blocked:** 0

---

## Summary

The Dashboard is the first screen users see after logging in. Testing here focused on verifying that all widgets load, navigation works, and the quick launch panel responds correctly. Most tests passed. One failure was observed with the "Time at Work" widget which displayed an incorrect value under certain conditions — logged as BUG_003.

---

## Test Cases

---

### TC_DSH_001 — Dashboard loads after successful login

| Field | Details |
|---|---|
| **Test Case ID** | TC_DSH_001 |
| **Title** | Verify Dashboard page loads correctly after login |
| **Module** | Dashboard |
| **Priority** | P1 – Critical |
| **Prerequisites** | User has valid admin credentials |
| **Test Data** | Username: `Admin` Password: `admin123` |

**Steps:**

1. Navigate to the login page
2. Enter valid credentials and click Login
3. Observe the page that loads after login

**Expected Result:** The Dashboard page loads successfully. The page title shows "Dashboard". The OrangeHRM logo, left-side navigation menu, and dashboard widgets are all visible. No errors or broken elements are present.

**Actual Result:** Dashboard loaded correctly with the navigation sidebar on the left, header at the top showing "Admin", and widgets including Time at Work, My Actions, Quick Launch, Buzz Latest Posts, and Employees on Leave.

**Status:** ✅ Pass

---

### TC_DSH_002 — Left navigation menu is accessible

| Field | Details |
|---|---|
| **Test Case ID** | TC_DSH_002 |
| **Title** | Verify all main navigation menu items are present and clickable |
| **Module** | Dashboard |
| **Priority** | P1 – Critical |
| **Prerequisites** | User is logged in and on the Dashboard |
| **Test Data** | N/A |

**Steps:**

1. Log in and land on the Dashboard
2. Observe the left-side navigation menu
3. Verify the following menu items are present: Admin, PIM, Leave, Time, Recruitment, My Info, Performance, Dashboard, Directory, Maintenance, Buzz
4. Click on **PIM** — observe navigation
5. Click the browser back or use the menu to return to Dashboard
6. Click on **Leave** — observe navigation
7. Return to Dashboard

**Expected Result:** All expected menu items are visible. Clicking each item navigates to the corresponding module page without errors.

**Actual Result:** All menu items were present. PIM and Leave modules opened correctly. Navigation from menu worked as expected throughout.

**Status:** ✅ Pass

---

### TC_DSH_003 — Quick Launch panel visible and functional

| Field | Details |
|---|---|
| **Test Case ID** | TC_DSH_003 |
| **Title** | Verify Quick Launch panel shows shortcuts and they navigate correctly |
| **Module** | Dashboard |
| **Priority** | P2 – High |
| **Prerequisites** | User is on the Dashboard |
| **Test Data** | N/A |

**Steps:**

1. Locate the "Quick Launch" widget on the Dashboard
2. Verify the following shortcuts are visible: Assign Leave, Leave List, Timesheets, Apply Leave, My Leave, My Timesheets
3. Click on **Assign Leave**
4. Verify the page navigated correctly
5. Return to Dashboard and click **Leave List**
6. Verify that page also loads correctly

**Expected Result:** Quick Launch widget is visible with all standard shortcuts. Clicking each shortcut navigates to the correct page.

**Actual Result:** Quick Launch widget was visible with all six shortcuts. Assign Leave and Leave List both navigated correctly to their respective pages.

**Status:** ✅ Pass

---

### TC_DSH_004 — Time at Work widget displays data

| Field | Details |
|---|---|
| **Test Case ID** | TC_DSH_004 |
| **Title** | Verify Time at Work widget shows current day's work time correctly |
| **Module** | Dashboard |
| **Priority** | P3 – Medium |
| **Prerequisites** | User is on the Dashboard, logged in today |
| **Test Data** | N/A |

**Steps:**

1. Land on the Dashboard after login
2. Locate the "Time at Work" widget
3. Observe the time displayed
4. Wait 2–3 minutes and refresh the page
5. Check if the displayed time has updated

**Expected Result:** The Time at Work widget shows the time elapsed since the current punch-in. After refreshing, the time should increment accordingly.

**Actual Result:** The widget displayed "00:00" even though the user had been logged in for several minutes. After a page refresh, the count remained at zero. This appears to be a display bug tied to the punch-in feature not being triggered on demo login.

**Status:** ❌ Fail

**Bug Reference:** BUG_003

**Remarks:** This may be expected behaviour if no punch-in has been recorded for the session. However, there is no indicator or instruction for the user on the widget itself. Either the widget should display a meaningful message like "No attendance recorded today" or it should auto-track from login time. Current state is confusing.

---

### TC_DSH_005 — My Actions widget is present

| Field | Details |
|---|---|
| **Test Case ID** | TC_DSH_005 |
| **Title** | Verify My Actions widget is visible on Dashboard |
| **Module** | Dashboard |
| **Priority** | P3 – Medium |
| **Prerequisites** | User is on the Dashboard |
| **Test Data** | N/A |

**Steps:**

1. Land on the Dashboard
2. Locate the "My Actions" widget
3. Observe its contents

**Expected Result:** The My Actions widget is visible and displays pending actions (leave requests to approve, etc.) or shows a "No pending actions" state if none exist.

**Actual Result:** My Actions widget was visible and displayed "No Pending Actions" — this is the correct empty state for a fresh demo environment.

**Status:** ✅ Pass

---

### TC_DSH_006 — Profile dropdown menu is accessible

| Field | Details |
|---|---|
| **Test Case ID** | TC_DSH_006 |
| **Title** | Verify user profile dropdown in header works correctly |
| **Module** | Dashboard |
| **Priority** | P2 – High |
| **Prerequisites** | User is logged in as Admin |
| **Test Data** | N/A |

**Steps:**

1. Look for the user profile area in the top-right corner of the header (shows "Admin")
2. Click on the profile/avatar icon
3. Observe the dropdown menu options
4. Verify options present: About, Support, Change Password, Logout

**Expected Result:** Clicking the profile dropdown reveals a menu with options including About, Support, Change Password, and Logout. Each option should be clickable.

**Actual Result:** Profile dropdown appeared with: About, Support, Change Password, and Logout. All options were visible and responding to clicks.

**Status:** ✅ Pass

---

### TC_DSH_007 — Admin module is accessible from navigation

| Field | Details |
|---|---|
| **Test Case ID** | TC_DSH_007 |
| **Title** | Verify Admin menu item opens the Administration module |
| **Module** | Dashboard |
| **Priority** | P2 – High |
| **Prerequisites** | User is logged in as Admin |
| **Test Data** | N/A |

**Steps:**

1. From the Dashboard, click **Admin** in the left navigation menu
2. Observe the page that opens
3. Verify the sub-menu items are present: User Management, Job, Organisation, Qualifications, Nationalities, Configuration

**Expected Result:** Admin module opens. Sub-menu items for admin configuration are visible. The first page (User Management) loads correctly.

**Actual Result:** Admin module opened correctly. User Management page loaded with a list of system users. All sub-menu categories were present.

**Status:** ✅ Pass

---

### TC_DSH_008 — Dashboard page title and branding

| Field | Details |
|---|---|
| **Test Case ID** | TC_DSH_008 |
| **Title** | Verify browser tab title and page branding are correct |
| **Module** | Dashboard |
| **Priority** | P4 – Low |
| **Prerequisites** | User is logged in and on the Dashboard |
| **Test Data** | N/A |

**Steps:**

1. After logging in, observe the browser tab title
2. Observe the OrangeHRM logo displayed in the top-left of the page
3. Verify the header text says "Dashboard"

**Expected Result:** Browser tab title reflects the application name. OrangeHRM logo is visible. Page heading shows "Dashboard".

**Actual Result:** Browser tab showed "OrangeHRM". Logo was visible in the left sidebar. Page heading showed "Dashboard" in the main content area.

**Status:** ✅ Pass

---

*End of Dashboard Module Test Cases*
