# Bug report template

Format: spreadsheet, one row per bug, columns in this order. Severity, Status and Priority use dropdowns. Start from [bug-report.xlsx](bug-report.xlsx); [bug-report.csv](bug-report.csv) is the same columns for viewing on GitHub (export it again whenever the .xlsx changes). Scales and IDs are in [SKILL.md](../SKILL.md).

## Core columns (always included)

| # | Column | What goes in it |
| --- | --- | --- |
| 1 | ID | `BUG-<NNN>`, e.g. `BUG-001` |
| 2 | Date | When the bug was found; needed because sometimes someone outside the QA team finds the bug |
| 3 | Reporter | Who found the bug; needed for the same reason |
| 4 | Title/summary | Pattern: `[Feature]: [what goes wrong] when [condition]` |
| 5 | Actual result | What happens when the bug occurs, as observed during testing (not after the fix) |
| 6 | Environment | The OS, browser and browser version, page size, and the app environment (e.g. staging or production) |
| 7 | Precondition | The conditions needed before reproducing the bug, such as the user account or test data to use |
| 8 | Steps to reproduce | The steps that make the bug happen |
| 9 | Expected result | One expected result for the bug itself (unlike a test case, where each step has its own) |
| 10 | Severity | Critical / High / Medium / Low (defect severity scale) |
| 11 | Attachments/evidence | Evidence link |
| 12 | Reproducibility | How many times the bug happened out of the attempts, e.g. 5/5, 3/5 or 1/10. If it doesn't happen every time, try at least 5 times |
| 13 | Status | See the status flow below |

## Status flow

New → Open → Fixed → Retest → Closed. If the retest fails: Retest → Reopened → Fixed → Retest, until it passes. If the bug won't be fixed: Open → Known issue.

| Status | Means |
| --- | --- |
| **New** | Just reported, not yet confirmed |
| **Open** | Confirmed, waiting for a fix |
| **Fixed** | The developer says it's fixed |
| **Retest** | QA is checking the fix |
| **Closed** | The fix is confirmed by the retest |
| **Reopened** | The retest failed, so it goes back to the developer |
| **Known issue** | The bug won't be fixed, for example because its severity is Low |

## Conditional columns (include when needed)

| Column | What goes in it | Include when |
| --- | --- | --- |
| Impact or risk assessment | The business effect of the bug | Severity is Critical or High, or the business effect isn't obvious from the title |
| Root cause/corrective action | Why the bug happened and what was fixed | Bugs are fixed and the developer shares the cause |
| Priority | How urgently to fix it: High / Medium / Low. Can be set by someone other than QA, e.g. the project manager | There are many bugs; if there are only a few, severity is enough |
| Linked test case | The test case ID | The bug was found by a test case |

---

## Example (fictional app: BookNest, an online bookstore)

| Column | Value |
| --- | --- |
| ID | BUG-001 |
| Date | 2026-11-12 |
| Reporter | QA tester |
| Title/summary | Search: no results shown when the title contains an apostrophe |
| Actual result | Searching `Charlotte's Garden` shows "0 results"; the book is in the catalog |
| Environment | Windows 11, Chrome 130, 1366×768, staging |
| Precondition | Logged in as `reader01`; the book `Charlotte's Garden` exists in the catalog |
| Steps to reproduce | 1. Open the search page<br>2. Type `Charlotte's Garden`<br>3. Press Enter |
| Expected result | The book `Charlotte's Garden` appears in the results |
| Severity | High |
| Attachments/evidence | Evidence link (screenshot) |
| Reproducibility | 5/5 |
| Status | Known issue |
| Linked test case | TC-SEARCH-001 |
