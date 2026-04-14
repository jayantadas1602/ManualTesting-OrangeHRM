# Test Plan — OrangeHRM Manual Testing Project

**Document Version:** 1.2  
**Prepared By:** [Your Name]  
**Reviewed By:** Self-review  
**Date Created:** March 1, 2025  
**Last Updated:** March 8, 2025  
**Status:** Approved

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Test Objectives](#2-test-objectives)
3. [Scope](#3-scope)
4. [Test Approach](#4-test-approach)
5. [Test Environment](#5-test-environment)
6. [Entry and Exit Criteria](#6-entry-and-exit-criteria)
7. [Test Schedule](#7-test-schedule)
8. [Test Deliverables](#8-test-deliverables)
9. [Risk and Mitigation](#9-risk-and-mitigation)
10. [Assumptions and Dependencies](#10-assumptions-and-dependencies)
11. [Defect Management](#11-defect-management)

---

## 1. Introduction

### 1.1 Purpose

This Test Plan describes the approach, scope, resources, and schedule for testing the OrangeHRM open-source Human Resource Management demo application. It is intended to guide the test execution process and ensure consistent, repeatable coverage across the modules identified as in-scope.

### 1.2 Application Overview

OrangeHRM is a web-based HR management system that allows organisations to manage employee data, attendance, leave, recruitment, and performance. The demo version (https://opensource-demo.orangehrmlive.com) is publicly accessible and serves as a functional representation of the product for testing and evaluation purposes.

The demo environment resets periodically (approximately every hour), which means any data added during a test session may not persist. This has been accounted for in test case design — particularly in modules where test execution order matters.

### 1.3 References

- OrangeHRM Official Documentation: https://www.orangehrm.com/hr-software-features/
- IEEE 829 Standard for Software Test Documentation (reference only)
- Application URL: https://opensource-demo.orangehrmlive.com

---

## 2. Test Objectives

The primary objectives of this testing effort are:

- Validate that all critical functional workflows in the identified modules work as expected
- Identify and document defects that impact usability, security, or data integrity
- Verify that the application handles invalid inputs and edge cases gracefully
- Ensure core navigation and UI elements are present and functional
- Provide documented evidence of test coverage via RTM

---

## 3. Scope

### 3.1 In Scope

The following modules and features will be tested:

**Module 1 — Login & Authentication**
- Valid and invalid login attempts
- Empty field validation
- Forgot password link
- Logout functionality
- Basic security checks (SQL injection, input sanitisation)

**Module 2 — Dashboard**
- Dashboard load and widget visibility after login
- Quick launch navigation
- Time at Work widget
- My Actions panel
- Admin access and profile dropdown

**Module 3 — Employee Management (PIM)**
- Employee list view
- Add new employee (mandatory and optional fields)
- Search and filter employees
- Edit employee personal information
- Upload employee photograph
- Delete employee record
- Emergency contacts and dependents
- Export functionality

**Module 4 — Leave Management**
- Leave type visibility
- Apply for leave (valid and invalid scenarios)
- Leave balance check
- Cancel applied leave
- Leave list view
- Leave entitlement configuration

### 3.2 Out of Scope

The following areas are explicitly excluded from this test cycle:

- Performance and load testing
- Mobile / responsive layout testing
- Integration with third-party payroll systems
- Recruitment module
- Performance Review module
- Time & Attendance module
- Actual email notifications (not testable on demo environment)
- Admin system configuration
- API-level testing (covered in a separate project)
- Any modules behind a paid upgrade

---

## 4. Test Approach

### 4.1 Testing Types

| Type | Applied? | Notes |
|---|---|---|
| Functional Testing | Yes | Core focus of this project |
| Boundary Value Analysis | Yes | Applied to date fields, character limits |
| Equivalence Partitioning | Yes | Used for login and form inputs |
| Negative Testing | Yes | Invalid inputs, missing mandatory fields |
| Exploratory Testing | Yes | Done during initial app walkthrough |
| UI / Sanity Testing | Yes | Navigation, element visibility |
| Regression Testing | Partial | Re-ran affected cases after env reset |
| Security Testing | Partial | Basic SQL injection and XSS checks only |

### 4.2 Test Case Design

Test cases were written following this structure:
- **Test Case ID** — Unique identifier per module (e.g., TC_LGN_001)
- **Title** — Short description of what is being tested
- **Prerequisites** — What needs to be true before the test runs
- **Test Steps** — Clear, numbered, executable steps
- **Test Data** — Input values used
- **Expected Result** — What the application should do
- **Actual Result** — What it actually did
- **Status** — Pass / Fail / Blocked / N/A
- **Remarks** — Any observations, environment notes, or bug IDs

### 4.3 Priority Levels

| Priority | Definition |
|---|---|
| P1 – Critical | Core workflow, must work. If fails, blocks further testing |
| P2 – High | Important feature. Failure significantly impacts the user |
| P3 – Medium | Functional but not on the critical path |
| P4 – Low | Minor issue, cosmetic or edge case |

---

## 5. Test Environment

### 5.1 Hardware

| Component | Specification |
|---|---|
| Machine | Dell Inspiron 15, 16GB RAM, i5-12th Gen |
| OS (Primary) | Windows 11 Home |
| OS (Secondary) | macOS Ventura 13.4 |
| Screen Resolution | 1920 × 1080 |

### 5.2 Software

| Software | Version |
|---|---|
| Google Chrome | 123.0.6312.86 |
| Mozilla Firefox | 124.0.1 |
| Application Version | OrangeHRM 5.x (Demo, latest) |

### 5.3 Test Accounts

| Account | Username | Password | Role |
|---|---|---|---|
| Admin | Admin | admin123 | System Administrator |
| Note | Demo resets periodically — any created test data may be lost | | |

---

## 6. Entry and Exit Criteria

### 6.1 Entry Criteria

Testing will begin when all of the following conditions are met:

- Test Plan is reviewed and approved
- Test cases are written and reviewed
- Application is accessible at the demo URL
- Admin credentials are verified to be working
- Test environment details are documented

### 6.2 Exit Criteria

Testing will be considered complete when:

- All in-scope test cases have been executed at least once
- All P1 and P2 defects are reported and tracked
- Test execution summary is updated with final pass/fail counts
- Bug Report is finalised with status for each defect
- RTM is populated and reviewed

---

## 7. Test Schedule

| Phase | Activity | Start Date | End Date |
|---|---|---|---|
| Phase 1 | Application exploration and walkthrough | Mar 1, 2025 | Mar 3, 2025 |
| Phase 2 | Test Plan creation | Mar 4, 2025 | Mar 6, 2025 |
| Phase 3 | Test case writing | Mar 7, 2025 | Mar 9, 2025 |
| Phase 4 | Test execution – Login & Dashboard | Mar 10, 2025 | Mar 13, 2025 |
| Phase 5 | Test execution – Employee Management | Mar 14, 2025 | Mar 20, 2025 |
| Phase 6 | Test execution – Leave Management | Mar 21, 2025 | Mar 26, 2025 |
| Phase 7 | Bug reporting and documentation | Mar 10, 2025 | Mar 28, 2025 |
| Phase 8 | RTM, final review, report prep | Mar 28, 2025 | Apr 2, 2025 |

---

## 8. Test Deliverables

| Deliverable | Location |
|---|---|
| Test Plan (this document) | Test_Plan.md |
| Test Cases – Login | test-cases/TC_Module01_Login.md |
| Test Cases – Dashboard | test-cases/TC_Module02_Dashboard.md |
| Test Cases – Employee Management | test-cases/TC_Module03_Employee_Management.md |
| Test Cases – Leave Management | test-cases/TC_Module04_Leave_Management.md |
| Bug Report | bug-reports/Bug_Report.md |
| Requirements Traceability Matrix | RTM.md |
| Screenshots | screenshots/ |

---

## 9. Risk and Mitigation

| # | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| 1 | Demo environment resets every hour, losing test data | High | Medium | Re-create test data at start of each session. Note reset impact in test remarks |
| 2 | Demo may be down or slow due to shared public access | Medium | High | Test during off-peak hours. Re-schedule if unavailable |
| 3 | Email-dependent features not verifiable on demo | High | Low | Mark as Blocked with reason. Outline expected behaviour based on UI labels |
| 4 | UI changes between demo versions | Low | Medium | Document exact version/date of testing. Re-check if significant changes observed |
| 5 | Inconsistent browser behaviour | Medium | Low | Test on both Chrome and Firefox. Document differences where they exist |

---

## 10. Assumptions and Dependencies

**Assumptions:**
- The demo application is a representative functional version of OrangeHRM
- Admin credentials (Admin / admin123) will remain valid throughout the testing period
- No back-end database access is available or required
- Email notifications are out of scope since the demo does not send real emails
- All testing will be performed manually — no automated tools in this project

**Dependencies:**
- Internet access to reach the demo URL
- OrangeHRM demo server uptime (maintained by OrangeHRM)
- A stable browser without extensions that interfere with form inputs

---

## 11. Defect Management

### 11.1 Defect Lifecycle

```
New → Assigned → In Progress → Fixed → Re-test → Closed
                                     ↓
                                  Rejected (if not a valid defect)
```

### 11.2 Severity Definitions

| Severity | Definition | Example |
|---|---|---|
| Critical | Application crashes or core feature completely broken | Login not working at all |
| High | Major feature broken, no workaround available | Cannot add employee |
| Medium | Feature partially broken or workaround exists | Search returns wrong results |
| Low | Cosmetic issue or minor inconvenience | Alignment off by a few pixels |

### 11.3 Priority Definitions

Priority reflects how urgently the fix is needed, independent of severity. A low-severity cosmetic bug on the login page might still be P2 if it affects brand perception.

### 11.4 Bug Tracking

In this portfolio project, bugs are tracked in the [Bug Report](./bug-reports/Bug_Report.md) file. In a real project, these would be raised in JIRA or a similar tool, with the same fields maintained.

---

*End of Test Plan*
