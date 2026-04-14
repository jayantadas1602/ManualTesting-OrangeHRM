# Test Cases — Module 04: Leave Management

**Module:** Leave Management  
**Tester:** [Your Name]  
**Execution Date:** March 21–26, 2025  
**Browser:** Chrome 123.0 (primary), Firefox 124.0 (cross-check)  
**Application URL:** https://opensource-demo.orangehrmlive.com  
**Total Test Cases:** 15  
**Pass:** 11 | **Fail:** 3 | **Blocked:** 1

---

## Summary

Leave Management is a module that employees interact with frequently, so getting the validation logic right here matters a lot. I tested the standard apply-leave flow thoroughly along with a range of edge cases — past dates, overlapping applications, and missing fields. Three failures were found, including one where overlapping leave dates weren't validated on the front end and another where the system allowed past-date leave application without any warning. These are both P2 issues that affect real users.

One important note: leave approval notification emails and workflow-based escalation could not be tested since the demo doesn't have email configured. Those cases are marked Blocked.

---

## Test Cases

---

### TC_LVE_001 — Navigate to Leave module

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_001 |
| **Title** | Verify the Leave module is accessible from the navigation menu |
| **Module** | Leave Management |
| **Priority** | P1 – Critical |
| **Prerequisites** | User is logged in |
| **Test Data** | N/A |

**Steps:**

1. From the Dashboard, click **Leave** in the left navigation menu
2. Observe the page that loads

**Expected Result:** Leave module opens. The default view shows the Leave List (or Apply page) with relevant sub-navigation options: Apply, My Leave, Leave List, Assign Leave, Leave Entitlements, Leave Reports.

**Actual Result:** Leave module opened correctly. Sub-menu items were visible: Apply, My Leave List, Leave List, Assign Leave, Leave Entitlements, Leave Reports, Leave Types, Leave Period, Holidays. All options were accessible.

**Status:** ✅ Pass

---

### TC_LVE_002 — Leave types are listed in the system

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_002 |
| **Title** | Verify configured leave types are visible in the Leave Types page |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | User is on the Leave module |
| **Test Data** | N/A |

**Steps:**

1. Navigate to Leave → Leave Types (under the Admin/Config section or from the sub-menu)
2. Observe the list of available leave types

**Expected Result:** Leave types configured in the system are listed — typically CasualLeave, Sick Leave, Annual Leave, Maternity Leave, etc.

**Actual Result:** Leave Types page showed: Annual Leave, Casual Leave, Casual Leave with Pay, Company Leave, Maternity Leave, Medical Leave, No Pay Leave, Personal Leave, Sick Leave. All were in "Active" status.

**Status:** ✅ Pass

---

### TC_LVE_003 — Apply for leave with valid future dates

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_003 |
| **Title** | Verify a leave application can be submitted with valid future dates |
| **Module** | Leave Management |
| **Priority** | P1 – Critical |
| **Prerequisites** | User is logged in. At least one leave type is configured |
| **Test Data** | Leave Type: `Annual Leave`, From Date: next Monday's date, To Date: next Friday's date, Comments: `Family vacation` |

**Steps:**

1. Navigate to Leave → Apply
2. Select `Annual Leave` from the Leave Type dropdown
3. Enter the next Monday's date in the "From" date field using the date picker
4. Enter the following Friday's date in the "To" date field
5. Enter `Family vacation` in the Comment field
6. Click **Apply**

**Expected Result:** Leave application is submitted successfully. A confirmation message appears. The application appears in the My Leave List with status "Pending".

**Actual Result:** Application submitted. "Successfully Saved" toast appeared. The leave entry appeared in My Leave List with status "Pending Approval".

**Status:** ✅ Pass

---

### TC_LVE_004 — Apply for leave with a past date

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_004 |
| **Title** | Verify that applying for leave with a past date triggers a warning or is blocked |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | User is on the Apply Leave page |
| **Test Data** | From Date: a date 10 days in the past, To Date: a date 8 days in the past |

**Steps:**

1. Navigate to Leave → Apply
2. Select any leave type
3. Select a date from the past (e.g., 10 days ago) in the From field
4. Select another past date (e.g., 8 days ago) in the To field
5. Click **Apply**

**Expected Result:** Application is either blocked with a validation message ("Cannot apply leave for past dates") or a clear warning is displayed asking for confirmation before proceeding.

**Actual Result:** The application was submitted without any warning or validation error. A leave application for past dates was created with "Pending Approval" status. No message indicated the dates were in the past.

**Status:** ❌ Fail

**Bug Reference:** BUG_008

**Remarks:** While some organisations do allow backdated leave (e.g., sick leave), the system should at minimum show a confirmation prompt — "You are applying for leave on past dates. Do you want to continue?" This helps prevent accidental backdated applications.

---

### TC_LVE_005 — Apply for leave with end date before start date

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_005 |
| **Title** | Verify validation when end date is earlier than start date |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | User is on the Apply Leave page |
| **Test Data** | From Date: next Friday, To Date: next Monday (To < From) |

**Steps:**

1. Navigate to Leave → Apply
2. Select any leave type
3. Set the From date to next Friday
4. Set the To date to next Monday (which is before the From date chronologically)
5. Click **Apply**

**Expected Result:** Validation error appears: "End date must be after start date" (or similar). Application is not submitted.

**Actual Result:** Validation error appeared: "To date should be after from date." Application was correctly blocked.

**Status:** ✅ Pass

---

### TC_LVE_006 — Apply for leave with overlapping dates

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_006 |
| **Title** | Verify that overlapping leave applications are handled correctly |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | An existing pending/approved leave application exists for a date range |
| **Test Data** | Existing leave: Mon–Fri next week. New application: Wed–Fri same week |

**Steps:**

1. First, submit a leave application for next Monday to Friday (use TC_LVE_003 as a base)
2. Navigate to Leave → Apply again
3. Select the same leave type
4. Enter Wednesday of next week as From Date
5. Enter Friday of next week as To Date (overlapping with the first application)
6. Click **Apply**

**Expected Result:** Application is rejected with a message indicating dates overlap with an existing application.

**Actual Result:** The overlapping application was accepted and submitted without any front-end validation. Both applications for overlapping date ranges were visible in My Leave List. The server-side may handle this eventually, but no immediate feedback was given to the user.

**Status:** ❌ Fail

**Bug Reference:** BUG_009

**Remarks:** This is a critical usability and data integrity issue. Employees should be immediately notified if their new leave request overlaps with an existing one. Without this check, the leave list becomes cluttered and requires manual admin review.

---

### TC_LVE_007 — Apply for single day leave

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_007 |
| **Title** | Verify leave can be applied for a single day (same From and To date) |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | User is on the Apply Leave page |
| **Test Data** | From Date: next Tuesday, To Date: next Tuesday (same date) |

**Steps:**

1. Navigate to Leave → Apply
2. Select a leave type
3. Set both From and To date to the same date (next Tuesday)
4. Click **Apply**

**Expected Result:** Single-day leave application is submitted successfully.

**Actual Result:** Application submitted without issues. Duration showed as "1 day" in the My Leave List.

**Status:** ✅ Pass

---

### TC_LVE_008 — Cancel a pending leave application

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_008 |
| **Title** | Verify an employee can cancel a pending leave application |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | At least one leave application exists in "Pending" status |
| **Test Data** | Use the leave application created in TC_LVE_003 |

**Steps:**

1. Navigate to Leave → My Leave List
2. Locate a leave application with "Pending Approval" status
3. Click on the application to open its details (or look for a Cancel action)
4. Click **Cancel** on the application

**Expected Result:** Leave application status changes to "Cancelled". The application is no longer in Pending status.

**Actual Result:** Cancel action was available. After clicking Cancel, the application status changed to "Cancelled". The leave list updated to show the cancelled status.

**Status:** ✅ Pass

---

### TC_LVE_009 — View leave list with filters

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_009 |
| **Title** | Verify Leave List can be filtered by date range and status |
| **Module** | Leave Management |
| **Priority** | P3 – Medium |
| **Prerequisites** | At least two leave applications exist |
| **Test Data** | Status filter: `Pending` |

**Steps:**

1. Navigate to Leave → My Leave List
2. Locate the Status filter dropdown
3. Select `Pending` from the dropdown
4. Click **Search**

**Expected Result:** Only leave applications with "Pending" status are displayed.

**Actual Result:** Filter worked correctly. Only pending applications were shown. Cancelled/other applications were hidden.

**Status:** ✅ Pass

---

### TC_LVE_010 — Apply for leave without selecting leave type

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_010 |
| **Title** | Verify validation error when Leave Type is not selected |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | User is on the Apply Leave page |
| **Test Data** | Leave Type: *(not selected)*, From/To Date: any valid future dates |

**Steps:**

1. Navigate to Leave → Apply
2. Leave the "Leave Type" field as its default (unselected)
3. Enter valid dates in From and To fields
4. Click **Apply**

**Expected Result:** Validation error appears: "Leave Type is required." Application is not submitted.

**Actual Result:** Validation error "Required" appeared under the Leave Type field. Application did not proceed.

**Status:** ✅ Pass

---

### TC_LVE_011 — Apply for leave without entering dates

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_011 |
| **Title** | Verify validation error when both date fields are empty |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | User is on the Apply Leave page |
| **Test Data** | Leave Type: `Annual Leave`, From/To: *(empty)* |

**Steps:**

1. Navigate to Leave → Apply
2. Select `Annual Leave`
3. Leave both From and To date fields empty
4. Click **Apply**

**Expected Result:** Validation errors appear for both empty date fields. Application is not submitted.

**Actual Result:** "Required" appeared under both date fields. Application did not proceed.

**Status:** ✅ Pass

---

### TC_LVE_012 — Leave balance check

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_012 |
| **Title** | Verify leave balance is displayed correctly for each leave type |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | Leave entitlement has been configured for the logged-in user |
| **Test Data** | N/A |

**Steps:**

1. Navigate to Leave → Apply
2. Select `Annual Leave` from the Leave Type dropdown
3. Observe the "Balance" field that appears after selecting the leave type
4. Note the available leave balance shown

**Expected Result:** The available leave balance for the selected leave type is displayed below or near the leave type field.

**Actual Result:** After selecting Annual Leave, the balance was shown as a number (e.g., "14.00 Day(s)"). This updated when a different leave type was selected.

**Status:** ✅ Pass

---

### TC_LVE_013 — Apply leave button remains clickable with empty form

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_013 |
| **Title** | Verify the Apply button does not remain enabled when mandatory fields are empty |
| **Module** | Leave Management |
| **Priority** | P3 – Medium |
| **Prerequisites** | User is on the Apply Leave page, all fields empty |
| **Test Data** | All fields empty |

**Steps:**

1. Navigate to Leave → Apply
2. Do not fill in any fields
3. Observe whether the **Apply** button is enabled or disabled
4. Click the Apply button

**Expected Result:** Ideally, the Apply button should be disabled (greyed out) until mandatory fields are filled. At a minimum, clicking it should show validation errors.

**Actual Result:** The Apply button remained active (not greyed out) even with no fields filled. Clicking it triggered validation messages — functionally correct, but from a UX standpoint, disabling the button proactively would be a cleaner approach.

**Status:** ❌ Fail

**Bug Reference:** BUG_013

**Remarks:** Minor UX issue. The button should be disabled until minimum required fields (Leave Type and dates) are filled. This reduces the chance of users clicking Apply and then being confused by multiple error messages. Severity: Low.

---

### TC_LVE_014 — View Leave Entitlements

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_014 |
| **Title** | Verify the Leave Entitlements page shows configured entitlements |
| **Module** | Leave Management |
| **Priority** | P3 – Medium |
| **Prerequisites** | User has access to Leave Entitlements |
| **Test Data** | N/A |

**Steps:**

1. Navigate to Leave → Leave Entitlements
2. Observe the entitlements listed

**Expected Result:** Entitlements page shows employee names, leave types, and allocated days for the current leave period.

**Actual Result:** Leave Entitlements page loaded correctly. Search filters were present. Entitlements for demo users were visible.

**Status:** ✅ Pass

---

### TC_LVE_015 — [BLOCKED] Leave approval email notification

| Field | Details |
|---|---|
| **Test Case ID** | TC_LVE_015 |
| **Title** | Verify the leave manager receives an email notification when leave is applied |
| **Module** | Leave Management |
| **Priority** | P2 – High |
| **Prerequisites** | Employee applies for leave. A reporting manager is configured with a valid email |
| **Test Data** | Leave application submitted by any employee |

**Steps:**

1. Apply for leave as an employee
2. Log in as the reporting manager / admin
3. Check the manager's email inbox for a leave notification

**Expected Result:** Manager receives an email notification with details of the leave application.

**Actual Result:** ⛔ Blocked — the demo environment does not have a mail server configured. Email notifications cannot be received or verified in this setup.

**Status:** ⛔ Blocked

**Remarks:** This would require a locally configured OrangeHRM with an SMTP server. The UI shows options for email configuration under Admin → Configuration → Email Configuration, but this cannot be set up on the public demo.

---

*End of Leave Management Module Test Cases*
