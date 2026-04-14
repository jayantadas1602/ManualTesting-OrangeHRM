# Test Cases — Module 03: Employee Management (PIM)

**Module:** Employee Management (PIM — Personal Information Management)  
**Tester:** [Your Name]  
**Execution Date:** March 14–20, 2025  
**Browser:** Chrome 123.0 (primary), Firefox 124.0 (cross-check)  
**Application URL:** https://opensource-demo.orangehrmlive.com  
**Total Test Cases:** 20  
**Pass:** 15 | **Fail:** 4 | **Blocked:** 1

---

## Summary

PIM is one of the most heavily used modules in OrangeHRM — almost everything in the system ties back to the employee record. Testing here was the most involved part of the project. I went through add, search, edit, and delete flows in detail, and also tested some edge cases like uploading unsupported file types and entering special characters in numeric fields.

Worth noting: since the demo resets periodically, I had to create test employees at the beginning of each session before running the edit/delete test cases. I documented this dependency clearly in each affected test case.

Four failures were found — the most notable being that the phone number field accepts alphabetic characters, and that the Employee ID field allows special characters without any validation.

---

## Test Cases

---

### TC_PIM_001 — Navigate to PIM module

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_001 |
| **Title** | Verify PIM module loads correctly from the navigation menu |
| **Module** | Employee Management (PIM) |
| **Priority** | P1 – Critical |
| **Prerequisites** | User is logged in |
| **Test Data** | N/A |

**Steps:**

1. From the Dashboard, click **PIM** in the left navigation menu
2. Observe the page that loads

**Expected Result:** PIM module opens. The Employee List page is displayed by default with a search/filter section at the top and a list of employees below.

**Actual Result:** PIM opened to the Employee List page. Search filters (Employee Name, ID, Employment Status, etc.) and employee list table were visible.

**Status:** ✅ Pass

---

### TC_PIM_002 — Employee list displays existing records

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_002 |
| **Title** | Verify the employee list shows existing employee records |
| **Module** | Employee Management (PIM) |
| **Priority** | P1 – Critical |
| **Prerequisites** | User is on the PIM Employee List page |
| **Test Data** | N/A |

**Steps:**

1. Navigate to PIM → Employee List
2. Observe the list of employees displayed in the table
3. Verify columns are visible: Employee Name, Employee ID, Job Title, Employment Status, Sub Unit, Experience

**Expected Result:** At least some employee records are pre-loaded in the demo. Table columns are correctly labelled and data is populated.

**Actual Result:** Demo environment had several pre-loaded employees. All column headers were correctly displayed. Employee names, IDs, and job titles were visible.

**Status:** ✅ Pass

---

### TC_PIM_003 — Add new employee with valid mandatory data

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_003 |
| **Title** | Verify a new employee can be added with all mandatory fields filled |
| **Module** | Employee Management (PIM) |
| **Priority** | P1 – Critical |
| **Prerequisites** | User is on the PIM module |
| **Test Data** | First Name: `Ravi`, Last Name: `Sharma`, Employee ID: auto-generated |

**Steps:**

1. Navigate to PIM → Add Employee (click the **+ Add** button)
2. Enter `Ravi` in the First Name field
3. Leave Middle Name blank
4. Enter `Sharma` in the Last Name field
5. Note the auto-generated Employee ID
6. Leave the "Create Login Details" toggle off for now
7. Click **Save**

**Expected Result:** Employee record is created. User is redirected to the employee profile page for "Ravi Sharma". A success toast message appears confirming the record was saved.

**Actual Result:** Employee "Ravi Sharma" was created successfully. Redirected to the employee's personal details page. Success toast "Successfully Saved" appeared briefly.

**Status:** ✅ Pass

**Remarks:** Employee ID was auto-generated as a sequential number. The system prevented duplicate auto-generated IDs.

---

### TC_PIM_004 — Add new employee with empty mandatory fields

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_004 |
| **Title** | Verify validation messages appear when mandatory fields are empty |
| **Module** | Employee Management (PIM) |
| **Priority** | P1 – Critical |
| **Prerequisites** | User is on the Add Employee page |
| **Test Data** | All fields empty |

**Steps:**

1. Navigate to PIM → Add Employee
2. Clear both First Name and Last Name fields (if pre-filled)
3. Click **Save** without entering any data

**Expected Result:** Validation messages appear below the empty mandatory fields. Employee is not saved.

**Actual Result:** "Required" validation messages appeared under both First Name and Last Name fields. The record was not saved.

**Status:** ✅ Pass

---

### TC_PIM_005 — Employee ID field accepts special characters

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_005 |
| **Title** | Verify that the Employee ID field rejects special characters |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | User is on the Add Employee page |
| **Test Data** | First Name: `Test`, Last Name: `User`, Employee ID: `EMP@#!001` |

**Steps:**

1. Navigate to PIM → Add Employee
2. Enter `Test` in First Name and `User` in Last Name
3. Clear the auto-generated Employee ID
4. Type `EMP@#!001` in the Employee ID field
5. Click **Save**

**Expected Result:** Validation error is shown indicating the Employee ID should only contain alphanumeric characters. Employee is not saved with invalid ID.

**Actual Result:** No validation error appeared for the special characters. The employee was saved with Employee ID `EMP@#!001`. This is a data integrity issue.

**Status:** ❌ Fail

**Bug Reference:** BUG_006

**Remarks:** Employee IDs with special characters can cause downstream issues in reporting and exports. Input should be restricted to alphanumeric characters only.

---

### TC_PIM_006 — Search employee by name

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_006 |
| **Title** | Verify employee search by name returns matching records |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | At least one employee record exists. User is on Employee List page |
| **Test Data** | Search name: first 3 characters of any existing employee's first name |

**Steps:**

1. Navigate to PIM → Employee List
2. In the "Employee Name" search field, type the first 3 letters of a known employee's name (e.g., `Rav` for Ravi Sharma)
3. Click the **Search** button

**Expected Result:** The employee list filters to show only employees whose names match the search term. Employees not matching the search are hidden.

**Actual Result:** Search returned the matching employee "Ravi Sharma". Other employees were filtered out. The search was case-insensitive — both "rav" and "RAV" returned the same result.

**Status:** ✅ Pass

---

### TC_PIM_007 — Search employee by Employee ID

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_007 |
| **Title** | Verify employee search by Employee ID returns the correct record |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | At least one employee exists with a known ID |
| **Test Data** | Employee ID: the auto-generated ID from TC_PIM_003 |

**Steps:**

1. Navigate to PIM → Employee List
2. Enter the Employee ID of the employee created in TC_PIM_003 in the Employee ID search field
3. Click **Search**

**Expected Result:** Only the employee with the matching ID is shown in the results list.

**Actual Result:** Correct employee was returned. Only one row appeared in the results table.

**Status:** ✅ Pass

---

### TC_PIM_008 — Search with no matching results

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_008 |
| **Title** | Verify appropriate message shown when search returns no results |
| **Module** | Employee Management (PIM) |
| **Priority** | P3 – Medium |
| **Prerequisites** | User is on the Employee List page |
| **Test Data** | Employee Name: `ZZZNONEXISTENT` |

**Steps:**

1. Navigate to PIM → Employee List
2. Enter `ZZZNONEXISTENT` in the Employee Name search field
3. Click **Search**

**Expected Result:** An empty state is shown (e.g., "No Records Found") — the table shows no results but the page does not error out.

**Actual Result:** Table displayed "No Records Found" message. Page remained stable. No error thrown.

**Status:** ✅ Pass

---

### TC_PIM_009 — Filter employees by Employment Status

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_009 |
| **Title** | Verify the Employment Status filter returns filtered results |
| **Module** | Employee Management (PIM) |
| **Priority** | P3 – Medium |
| **Prerequisites** | User is on Employee List page with multiple employees |
| **Test Data** | Employment Status: `Active` |

**Steps:**

1. Navigate to PIM → Employee List
2. Click the "Employment Status" dropdown
3. Select **Active**
4. Click **Search**

**Expected Result:** Only employees with Active status are shown in the results.

**Actual Result:** All returned employees had "Full-Time Permanent" or similar active status values. Filter applied correctly.

**Status:** ✅ Pass

---

### TC_PIM_010 — Reset search filters

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_010 |
| **Title** | Verify the Reset button clears all applied filters |
| **Module** | Employee Management (PIM) |
| **Priority** | P3 – Medium |
| **Prerequisites** | A filter has been applied in the Employee List search |
| **Test Data** | Apply any filter first (e.g., Employee Name: `Ravi`) |

**Steps:**

1. Apply a name filter — enter `Ravi` and click Search
2. Verify filtered results are shown
3. Click the **Reset** button
4. Observe the filter fields and result list

**Expected Result:** All filter fields are cleared. The complete employee list is restored.

**Actual Result:** Reset button cleared the Employee Name field and restored the full employee list. Status and other dropdowns also reset to default.

**Status:** ✅ Pass

---

### TC_PIM_011 — Edit employee personal information

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_011 |
| **Title** | Verify employee personal details can be updated and saved |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | An employee record exists. User is on that employee's profile |
| **Test Data** | Driver's License: `DL-MH-2024-001234`, Date of Birth: `15-Jun-1990`, Gender: Male |

**Steps:**

1. Open the profile of the employee created in TC_PIM_003 (Ravi Sharma)
2. Click on the **Personal Details** tab
3. Enter `DL-MH-2024-001234` in the Driver's License Number field
4. Select `15-Jun-1990` as Date of Birth using the date picker
5. Select `Male` from the Gender dropdown
6. Select `Indian` as Nationality (if field exists)
7. Click **Save**

**Expected Result:** Personal details are updated successfully. A success toast message appears.

**Actual Result:** All fields accepted the values. Clicked Save and a "Successfully Updated" toast appeared. Refreshed the page — all values were retained.

**Status:** ✅ Pass

---

### TC_PIM_012 — Upload valid profile photo

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_012 |
| **Title** | Verify a valid JPG/PNG image can be uploaded as employee photo |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | Employee profile is open. A JPG image under 1MB is available |
| **Test Data** | File: `profile_photo.jpg`, Size: ~150KB, Format: JPEG |

**Steps:**

1. Open the employee profile (Ravi Sharma)
2. Click on the profile photo placeholder/icon at the top of the profile
3. Click **Change Photo** or the edit icon on the photo
4. Select a valid JPG file from the local machine
5. Confirm the upload

**Expected Result:** Photo uploads successfully. The employee's profile now displays the selected image. A success message is shown.

**Actual Result:** Photo upload was successful. The image appeared in the profile photo area. Success toast shown.

**Status:** ✅ Pass

---

### TC_PIM_013 — Upload invalid file type as profile photo

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_013 |
| **Title** | Verify that uploading an unsupported file type as photo is rejected |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | Employee profile is open. A .txt or .pdf file is available |
| **Test Data** | File: `document.txt` |

**Steps:**

1. Open any employee profile
2. Click to change the profile photo
3. Select a `.txt` file instead of an image
4. Attempt to upload

**Expected Result:** Application shows an error: file type not supported. The upload is rejected and the existing photo is retained.

**Actual Result:** An error message appeared: "File type not allowed. Allowed types: jpg, jpeg, png, gif." Upload was correctly rejected.

**Status:** ✅ Pass

---

### TC_PIM_014 — Upload SVG file as profile photo

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_014 |
| **Title** | Verify SVG file upload is rejected for profile photo |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | Employee profile is open. An SVG file is available |
| **Test Data** | File: `icon.svg` |

**Steps:**

1. Open any employee profile
2. Attempt to upload an `.svg` file as the profile photo

**Expected Result:** SVG should be rejected since it is a vector format and can contain executable code (XSS risk).

**Actual Result:** The `.svg` file was accepted and uploaded without any warning. The image rendered as a blank grey area since SVG rendering in this context was incomplete — but the file was accepted by the system.

**Status:** ❌ Fail

**Bug Reference:** BUG_004

**Remarks:** SVG files can contain embedded JavaScript and should never be accepted as image uploads. This is a potential security risk. The allowed file types list should explicitly exclude `.svg`.

---

### TC_PIM_015 — Phone number field accepts alphabets

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_015 |
| **Title** | Verify phone number field only accepts numeric input |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | Employee profile is open, on the Contact Details tab |
| **Test Data** | Work Phone: `ABCD1234EF` |

**Steps:**

1. Open an employee profile
2. Navigate to the **Contact Details** tab
3. Enter `ABCD1234EF` in the Work Phone field
4. Click **Save**

**Expected Result:** Validation error appears — "Please enter a valid phone number" or similar. Alphabetic characters should not be accepted in a phone number field.

**Actual Result:** The field accepted the alphabetic characters. No validation error was triggered. The record was saved with `ABCD1234EF` as the phone number.

**Status:** ❌ Fail

**Bug Reference:** BUG_012

**Remarks:** This is a data quality issue. Phone number fields should enforce numeric-only input (with optional formatting for +, -, and parentheses). Storing alphabets as a phone number can break any downstream system that tries to process or dial these numbers.

---

### TC_PIM_016 — Add emergency contact

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_016 |
| **Title** | Verify emergency contact can be added to an employee profile |
| **Module** | Employee Management (PIM) |
| **Priority** | P3 – Medium |
| **Prerequisites** | Employee profile is open |
| **Test Data** | Name: `Sunita Sharma`, Relationship: `Spouse`, Work Phone: `9876543210` |

**Steps:**

1. Open the employee profile (Ravi Sharma)
2. Click on the **Emergency Contacts** tab
3. Click the **+ Add** button
4. Enter `Sunita Sharma` in the Name field
5. Enter `Spouse` as Relationship
6. Enter `9876543210` in the Work Phone field
7. Click **Save**

**Expected Result:** Emergency contact is saved. The new contact appears in the emergency contact list under the tab.

**Actual Result:** Emergency contact was added successfully. "Successfully Saved" toast appeared. Contact was visible in the list.

**Status:** ✅ Pass

---

### TC_PIM_017 — Add dependent

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_017 |
| **Title** | Verify a dependent can be added to an employee record |
| **Module** | Employee Management (PIM) |
| **Priority** | P3 – Medium |
| **Prerequisites** | Employee profile is open |
| **Test Data** | Name: `Arjun Sharma`, Relationship: `Child`, Date of Birth: `10-Mar-2015` |

**Steps:**

1. Open an employee profile
2. Navigate to the **Dependents** tab
3. Click **+ Add**
4. Enter `Arjun Sharma` as Name
5. Select `Child` as Relationship
6. Enter `10-Mar-2015` as Date of Birth
7. Click **Save**

**Expected Result:** Dependent record is saved and appears in the dependents list.

**Actual Result:** Dependent was added successfully. Record appeared in the dependents table.

**Status:** ✅ Pass

---

### TC_PIM_018 — Delete an employee record

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_018 |
| **Title** | Verify an employee record can be deleted successfully |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | A test employee exists that can be deleted (not production critical) |
| **Test Data** | Employee: `Test DeleteUser` (create a throwaway record before this test) |

**Steps:**

1. Create a throwaway employee: First Name `Test`, Last Name `DeleteUser`
2. Navigate to PIM → Employee List
3. Search for `Test DeleteUser`
4. Check the checkbox next to the employee's row
5. Click the **Delete Selected** button
6. Confirm the deletion in the confirmation dialog

**Expected Result:** A confirmation dialog appears before deletion. After confirmation, the employee is removed from the list. A success message is shown.

**Actual Result:** Confirmation dialog appeared with "Are you sure?" message. After clicking "Yes, Delete", the employee was removed. "Successfully Deleted" toast appeared. Employee no longer appeared in search results.

**Status:** ✅ Pass

**Remarks:** Deletion was permanent with no undo option. In a real project, I would raise a suggestion to implement soft-delete or a recycle bin for employee records.

---

### TC_PIM_019 — Export employee list

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_019 |
| **Title** | Verify the Export function downloads employee data correctly |
| **Module** | Employee Management (PIM) |
| **Priority** | P3 – Medium |
| **Prerequisites** | User is on the Employee List page with at least one employee |
| **Test Data** | N/A |

**Steps:**

1. Navigate to PIM → Employee List
2. Do not apply any filters (export all)
3. Click the **Export** button (or the CSV/Excel download icon if available)
4. Open the downloaded file

**Expected Result:** A CSV or Excel file is downloaded. The file contains employee data with correct column headers and populated rows.

**Actual Result:** A CSV file was downloaded. The file opened in Excel and contained columns: Employee Name, Employee ID, Job Title, Employment Status, Sub Unit. Data matched what was visible on screen.

**Status:** ✅ Pass

---

### TC_PIM_020 — [BLOCKED] Bulk import employees via CSV

| Field | Details |
|---|---|
| **Test Case ID** | TC_PIM_020 |
| **Title** | Verify employees can be bulk imported via CSV upload |
| **Module** | Employee Management (PIM) |
| **Priority** | P2 – High |
| **Prerequisites** | Admin access to PIM configuration |
| **Test Data** | A properly formatted CSV file with employee records |

**Steps:**

1. Navigate to the PIM configuration area
2. Locate the import/bulk upload option
3. Upload a CSV file with multiple employee records
4. Confirm the import

**Expected Result:** All valid employee records from the CSV are imported. An import summary shows success/failure counts.

**Actual Result:** ⛔ Blocked — the CSV import feature in OrangeHRM requires specific configuration that is not available in the public demo. The import option was found in the menu but produced an error when a file was uploaded.

**Status:** ⛔ Blocked

**Remarks:** This would be tested in a locally installed or properly configured OrangeHRM instance.

---

*End of Employee Management (PIM) Module Test Cases*
