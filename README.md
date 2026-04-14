# Manual Testing Project — OrangeHRM

> A complete manual testing documentation suite for the OrangeHRM Human Resource Management System demo application. Covers test planning, test case design, bug reporting, and requirements traceability across four core modules.

---

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Test Cases](https://img.shields.io/badge/Test%20Cases-55-blue)
![Passed](https://img.shields.io/badge/Passed-42-brightgreen)
![Failed](https://img.shields.io/badge/Failed-10-red)
![Blocked](https://img.shields.io/badge/Blocked-3-yellow)
![Bugs](https://img.shields.io/badge/Bugs%20Reported-15-critical)
![Coverage](https://img.shields.io/badge/Coverage-87%25-blue)

---

## Application Under Test

| Detail | Info |
|---|---|
| **Application** | OrangeHRM Open Source |
| **URL** | https://opensource-demo.orangehrmlive.com |
| **Version** | OrangeHRM 5.x (Demo) |
| **Credentials** | Admin / admin123 |
| **Type** | Web-based HRM System |

---

## Project Objective

The goal of this project was to validate the functional behaviour of the OrangeHRM demo application by designing and executing manual test cases for the most business-critical modules. The testing focused on verifying that core HR workflows behave correctly under both normal and edge-case conditions.

This project was done as part of my QA portfolio to demonstrate my ability to:
- Understand an application end-to-end before writing a single test case
- Write clear, reproducible test cases that any tester can follow
- Identify and document defects with enough context for developers to reproduce them
- Map test coverage back to requirements using a Traceability Matrix

---

## Modules Tested

| # | Module | Test Cases | Pass | Fail | Blocked |
|---|---|---|---|---|---|
| 1 | Login & Authentication | 12 | 9 | 2 | 1 |
| 2 | Dashboard | 8 | 7 | 1 | 0 |
| 3 | Employee Management (PIM) | 20 | 15 | 4 | 1 |
| 4 | Leave Management | 15 | 11 | 3 | 1 |
| **Total** | | **55** | **42** | **10** | **3** |

---

## Bug Summary

| Severity | Count |
|---|---|
| Critical | 2 |
| High | 5 |
| Medium | 6 |
| Low | 2 |
| **Total** | **15** |

---

## Documents

| Document | Description |
|---|---|
| [Test Plan](./Test_Plan.md) | Project scope, strategy, schedule, risks, and entry/exit criteria |
| [Test Cases – Login](./test-cases/TC_Module01_Login.md) | 12 test cases for authentication flows |
| [Test Cases – Dashboard](./test-cases/TC_Module02_Dashboard.md) | 8 test cases for the main dashboard |
| [Test Cases – Employee Management](./test-cases/TC_Module03_Employee_Management.md) | 20 test cases for PIM module |
| [Test Cases – Leave Management](./test-cases/TC_Module04_Leave_Management.md) | 15 test cases for leave workflows |
| [Bug Report](./bug-reports/Bug_Report.md) | All 15 defects with steps, severity, and status |
| [RTM](./RTM.md) | Requirements Traceability Matrix |

---

## Tools Used

| Tool | Purpose |
|---|---|
| Browser (Chrome 123, Firefox 124) | Test execution |
| Google Sheets | Test case tracking |
| ShareX | Screenshots and screen recording |
| JIRA (simulated) | Bug ID reference format |
| Markdown | Documentation |

---

## Test Environment

- **OS:** Windows 11 (primary), macOS Ventura (cross-browser check)
- **Browsers:** Chrome 123.0, Firefox 124.0
- **Network:** Standard broadband (no VPN)
- **Screen Resolution:** 1920×1080
- **Device:** Desktop

---

## How to Navigate This Repo

1. Start with the **[Test Plan](./Test_Plan.md)** to understand the scope and strategy
2. Review **test cases** module by module in the `test-cases/` folder
3. Cross-reference failures with the **[Bug Report](./bug-reports/Bug_Report.md)**
4. Check the **[RTM](./RTM.md)** to verify coverage against requirements

---

## Key Observations

- OrangeHRM demo resets data every hour, which affected a few test cases. I handled this by re-running those cases fresh and noting it in the test case remarks.
- The application behaves slightly differently on Firefox vs Chrome for certain date-picker interactions — both environments were documented separately where they diverged.
- 3 test cases were marked **Blocked** due to demo environment restrictions (email-dependent features like password reset and leave notifications cannot be validated on the public demo).
- 2 bugs were marked **Critical** — one for missing account lockout after repeated failed logins (security concern) and one for missing front-end validation on overlapping leave dates.

---

## About

**Author:** Jayanta Das  
**Role:** QA Engineer (Manual + Automation)  
**LinkedIn:** [linkedin.com/in/your-profile](www.linkedin.com/in/jayanta99)  
**GitHub:** [github.com/your-username]([https://github.com](https://github.com/jayantadas1602))  
**Testing Period:** March 10 – March 28, 2025
