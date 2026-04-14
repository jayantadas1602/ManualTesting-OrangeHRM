# Screenshots

This folder contains screenshots taken during test execution, referenced in bug reports.

## Naming Convention

Screenshots follow the format: `BUG_[ID]_[short_description].png`

## Screenshots in This Project

| File | Description | Referenced In |
|---|---|---|
| `BUG_001_forgot_password_invalid_user.png` | Reset Password success shown for non-existent username | BUG_001 |
| `BUG_002_no_lockout_after_10_attempts.png` | Login page accepting 10th failed attempt with no lockout | BUG_002 |
| `BUG_003_time_widget_zero.png` | Time at Work widget showing 00:00 with no explanation | BUG_003 |
| `BUG_004_svg_upload_accepted.png` | SVG file accepted as employee profile photo | BUG_004 |
| `BUG_005_reset_subunit_filter_firefox.png` | Reset not clearing Sub Unit filter correctly on Firefox | BUG_005 |
| `BUG_006_employee_id_special_chars.png` | Employee ID saved with special characters | BUG_006 |
| `BUG_007_duplicate_id_generic_error.png` | Generic error message for duplicate Employee ID | BUG_007 |
| `BUG_008_past_date_leave_accepted.png` | Leave application accepted for past dates without warning | BUG_008 |
| `BUG_009_overlapping_leave_accepted.png` | Two overlapping leave applications in My Leave List | BUG_009 |
| `BUG_010_stale_leave_balance.png` | Leave balance showing old value before page refresh | BUG_010 |
| `BUG_011_widget_positions_not_saved.png` | Dashboard widgets reverting to default after re-login | BUG_011 |
| `BUG_012_phone_accepts_alphabets.png` | Phone number field saved with alphabetic characters | BUG_012 |
| `BUG_013_apply_button_always_enabled.png` | Apply button enabled with all mandatory fields empty | BUG_013 |
| `BUG_014_no_timeout_warning.png` | User redirected to login after idle timeout with no warning | BUG_014 |
| `BUG_015_export_count_mismatch.png` | Export summary showing 0 records vs actual file content | BUG_015 |

---

> **Note:** Screenshots were captured during test execution (March 10–28, 2025) using ShareX on Windows 11, Chrome 123.0. To replicate any screenshot, follow the steps in the corresponding bug report.
