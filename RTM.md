# Requirements Traceability Matrix (RTM)

**Project:** OrangeHRM Manual Testing  
**Prepared By:** [Your Name]  
**Date:** April 2, 2025  
**Version:** 1.0

---

## What is an RTM?

A Requirements Traceability Matrix maps each requirement (or expected feature behaviour) to one or more test cases. It ensures every requirement is tested and every test case has a reason to exist. It also helps identify gaps — requirements with no test cases, or test cases with no corresponding requirement.

---

## How to Read This RTM

| Column | Description |
|---|---|
| Req ID | Unique requirement identifier |
| Requirement Description | What the feature/behaviour should do |
| Module | Which module the requirement belongs to |
| Test Case ID(s) | Which test case(s) cover this requirement |
| Test Status | Overall pass/fail/blocked status for coverage |
| Bug ID | If a test case failed, the associated bug |

---

## Module 1 — Login & Authentication

| Req ID | Requirement Description | Test Case ID(s) | Test Status | Bug ID |
|---|---|---|---|---|
| REQ_LGN_01 | System shall allow login with valid credentials | TC_LGN_001 | ✅ Pass | — |
| REQ_LGN_02 | System shall reject login with incorrect password | TC_LGN_002 | ✅ Pass | — |
| REQ_LGN_03 | System shall reject login with incorrect username | TC_LGN_003 | ✅ Pass | — |
| REQ_LGN_04 | System shall reject login when both credentials are wrong | TC_LGN_004 | ✅ Pass | — |
| REQ_LGN_05 | System shall show validation when Username field is empty | TC_LGN_005 | ✅ Pass | — |
| REQ_LGN_06 | System shall show validation when Password field is empty | TC_LGN_006 | ✅ Pass | — |
| REQ_LGN_07 | System shall show validation when both fields are empty | TC_LGN_007 | ✅ Pass | — |
| REQ_LGN_08 | System shall provide a forgot password/reset link | TC_LGN_008 | ✅ Pass | — |
| REQ_LGN_09 | System shall not confirm or deny account existence on password reset | TC_LGN_009 | ❌ Fail | BUG_001 |
| REQ_LGN_10 | System shall implement account lockout after repeated failed attempts | TC_LGN_010 | ❌ Fail | BUG_002 |
| REQ_LGN_11 | System shall protect login form from SQL injection | TC_LGN_011 | ✅ Pass | — |
| REQ_LGN_12 | System shall allow users to log out successfully | TC_LGN_012 | ✅ Pass | — |
| REQ_LGN_13 | System shall send password reset email to valid user | TC_LGN_013 | ⛔ Blocked | — |

---

## Module 2 — Dashboard

| Req ID | Requirement Description | Test Case ID(s) | Test Status | Bug ID |
|---|---|---|---|---|
| REQ_DSH_01 | Dashboard shall load correctly after successful login | TC_DSH_001 | ✅ Pass | — |
| REQ_DSH_02 | Navigation menu shall be present with all module links | TC_DSH_002 | ✅ Pass | — |
| REQ_DSH_03 | Quick Launch panel shall be present and functional | TC_DSH_003 | ✅ Pass | — |
| REQ_DSH_04 | Time at Work widget shall display accurate current session time | TC_DSH_004 | ❌ Fail | BUG_003 |
| REQ_DSH_05 | My Actions panel shall be visible on the dashboard | TC_DSH_005 | ✅ Pass | — |
| REQ_DSH_06 | Profile dropdown shall be accessible from the header | TC_DSH_006 | ✅ Pass | — |
| REQ_DSH_07 | Admin module shall be accessible to admin users | TC_DSH_007 | ✅ Pass | — |
| REQ_DSH_08 | Page title and branding shall be correct | TC_DSH_008 | ✅ Pass | — |

---

## Module 3 — Employee Management (PIM)

| Req ID | Requirement Description | Test Case ID(s) | Test Status | Bug ID |
|---|---|---|---|---|
| REQ_PIM_01 | PIM module shall load with employee list by default | TC_PIM_001 | ✅ Pass | — |
| REQ_PIM_02 | Employee list shall display existing employee records with correct columns | TC_PIM_002 | ✅ Pass | — |
| REQ_PIM_03 | System shall allow adding a new employee with mandatory fields | TC_PIM_003 | ✅ Pass | — |
| REQ_PIM_04 | System shall validate mandatory fields on Add Employee | TC_PIM_004 | ✅ Pass | — |
| REQ_PIM_05 | Employee ID field shall only accept alphanumeric characters | TC_PIM_005 | ❌ Fail | BUG_006 |
| REQ_PIM_06 | System shall support employee search by name | TC_PIM_006 | ✅ Pass | — |
| REQ_PIM_07 | System shall support employee search by Employee ID | TC_PIM_007 | ✅ Pass | — |
| REQ_PIM_08 | System shall show appropriate message when search has no results | TC_PIM_008 | ✅ Pass | — |
| REQ_PIM_09 | System shall filter employees by Employment Status | TC_PIM_009 | ✅ Pass | — |
| REQ_PIM_10 | Reset button shall clear all active search filters | TC_PIM_010 | ✅ Pass | — |
| REQ_PIM_11 | System shall allow editing employee personal information | TC_PIM_011 | ✅ Pass | — |
| REQ_PIM_12 | System shall allow uploading a valid profile photo (JPG/PNG) | TC_PIM_012 | ✅ Pass | — |
| REQ_PIM_13 | System shall reject unsupported file types for profile photo | TC_PIM_013 | ✅ Pass | — |
| REQ_PIM_14 | System shall reject SVG files as employee profile photo | TC_PIM_014 | ❌ Fail | BUG_004 |
| REQ_PIM_15 | Phone number fields shall only accept numeric characters | TC_PIM_015 | ❌ Fail | BUG_012 |
| REQ_PIM_16 | System shall allow adding emergency contacts to employee profile | TC_PIM_016 | ✅ Pass | — |
| REQ_PIM_17 | System shall allow adding dependents to employee profile | TC_PIM_017 | ✅ Pass | — |
| REQ_PIM_18 | System shall allow deleting an employee record with confirmation | TC_PIM_018 | ✅ Pass | — |
| REQ_PIM_19 | System shall allow exporting employee list to CSV/Excel | TC_PIM_019 | ✅ Pass | — |
| REQ_PIM_20 | System shall support bulk employee import via CSV | TC_PIM_020 | ⛔ Blocked | — |

---

## Module 4 — Leave Management

| Req ID | Requirement Description | Test Case ID(s) | Test Status | Bug ID |
|---|---|---|---|---|
| REQ_LVE_01 | Leave module shall be accessible from the navigation menu | TC_LVE_001 | ✅ Pass | — |
| REQ_LVE_02 | Configured leave types shall be listed in the system | TC_LVE_002 | ✅ Pass | — |
| REQ_LVE_03 | System shall allow submitting a leave application with valid future dates | TC_LVE_003 | ✅ Pass | — |
| REQ_LVE_04 | System shall warn when applying leave for past dates | TC_LVE_004 | ❌ Fail | BUG_008 |
| REQ_LVE_05 | System shall reject leave applications where end date is before start date | TC_LVE_005 | ✅ Pass | — |
| REQ_LVE_06 | System shall prevent duplicate/overlapping leave applications | TC_LVE_006 | ❌ Fail | BUG_009 |
| REQ_LVE_07 | System shall allow single-day leave applications | TC_LVE_007 | ✅ Pass | — |
| REQ_LVE_08 | System shall allow cancellation of pending leave applications | TC_LVE_008 | ✅ Pass | — |
| REQ_LVE_09 | Leave list shall support filtering by status and date | TC_LVE_009 | ✅ Pass | — |
| REQ_LVE_10 | System shall validate Leave Type is selected before submitting | TC_LVE_010 | ✅ Pass | — |
| REQ_LVE_11 | System shall validate date fields are not empty before submitting | TC_LVE_011 | ✅ Pass | — |
| REQ_LVE_12 | System shall display leave balance for selected leave type | TC_LVE_012 | ✅ Pass | — |
| REQ_LVE_13 | Apply button shall be disabled when mandatory fields are empty | TC_LVE_013 | ❌ Fail | BUG_013 |
| REQ_LVE_14 | Leave entitlements shall be visible and configurable | TC_LVE_014 | ✅ Pass | — |
| REQ_LVE_15 | System shall notify manager via email on new leave application | TC_LVE_015 | ⛔ Blocked | — |

---

## Coverage Summary

| Module | Total Requirements | Pass | Fail | Blocked | Coverage % |
|---|---|---|---|---|---|
| Login & Authentication | 13 | 9 | 2 | 1 | **85%** |
| Dashboard | 8 | 7 | 1 | 0 | **88%** |
| Employee Management (PIM) | 20 | 15 | 4 | 1 | **95%** |
| Leave Management | 15 | 11 | 3 | 1 | **93%** |
| **Total** | **56** | **42** | **10** | **3** | **~87%** |

> Coverage % = (Pass + Fail) / Total × 100. Blocked cases are excluded from the denominator since they couldn't be executed, not because the requirement isn't covered by a test case.

---

## Untested / Gap Analysis

The following areas were identified as not covered in this test cycle, either because they fall outside the defined scope or were not feasible on the demo environment:

| Area | Reason Not Tested |
|---|---|
| Email-based workflows (reset password, leave notifications) | Demo has no mail server |
| Bulk employee CSV import | Demo configuration limitation |
| Performance under load | Out of scope for manual testing |
| Mobile/responsive UI | Out of scope for this project (separate project) |
| Recruitment module | Out of scope |
| Performance Review module | Out of scope |
| Time & Attendance module | Out of scope |
| Role-based access control (RBAC) | Partially explored but not formally tested |
| Admin configuration settings | Out of scope |

---

*End of RTM*
