# Test case template

Format: spreadsheet, one row per test case, columns in this order. Priority, Type and Status use dropdowns. Start from [test-case.xlsx](test-case.xlsx); [test-case.csv](test-case.csv) is the same columns for viewing on GitHub (export it again whenever the .xlsx changes). Scales and IDs are in [SKILL.md](../SKILL.md).

## Core columns (always included)

| # | Column | What goes in it |
| --- | --- | --- |
| 1 | ID | `TC-<FEATURE>-<NNN>`, e.g. `TC-LOGIN-001`. Unique for the app; never reused and never changed |
| 2 | Feature name | The feature the test case belongs to |
| 3 | Test case name | Pattern: `[Action] with/when [condition]`, e.g. "Log in with a wrong password" |
| 4 | Priority | Critical / Moderate / Low: the risk level of the traced condition or risk |
| 5 | Type | Positive / Negative / Edge case. Edge case: a test at a limit (boundary) or an unusual case, e.g. maximum length or an empty list. If the limit is important, label the test Positive or Negative; use Edge case when it needs testing but its impact is not so high |
| 6 | Precondition | The condition that must be met before the test case can be run |
| 7 | Test data | The exact user, inputs and values used in the test |
| 8 | Steps | Every step needed to run the test case |
| 9 | Expected results | The expected result of each step (step 1 → expected result 1), checked in the real app, not assumed |
| 10 | Traces to | The test condition ID when there is a test design; otherwise, the product risk ID from the test plan |
| 11 | Replaced by | When the test case is split, replaced or deleted: keep the row and write the new test case ID(s), or "Deleted" with the reason. Empty while active |

## Conditional columns (include when needed)

| Column | What goes in it | Include when |
| --- | --- | --- |
| Objective/description | What the test case proves | The test case name is too short or not informative |
| Environment | Where the test runs | The tests run on several environments; otherwise it is set once in the test plan |
| Tags | e.g. smoke, regression | Automating, or keeping a smoke or regression set |

## Test results

Kept separate from the test case definition. Use one method per project, not both.

**When to choose:** once, when writing the test plan, before the first run. Will the same test cases be run again for future releases? No → dated columns. Yes → run log. Record the choice in the test plan's approach section; if the project changes later, switch to the run log from that point and note it in the plan.

**Default: dated result columns** in the *Test cases* sheet, a new pair for each run:

| Column | What goes in it |
| --- | --- |
| Status (run date) | Pass / Fail / Blocked |
| Actual result (run date) | What actually happened, mainly when the test case fails or is blocked |

**Conditional: Run log** sheet in the same file (include when the test cases are re-run for each release, or automated tests run often), one row per run of one test case. GitHub view: [test-case-run-log.csv](test-case-run-log.csv).

| Column | What goes in it |
| --- | --- |
| Run date | When the test case was run |
| Test case ID | The test case that was run |
| Status | Pass / Fail / Blocked |
| Actual result | What actually happened, mainly when the test case fails or is blocked |
| Environment | The environment of this run (e.g. browser version, staging or production) |
| Tester | Who ran it |
| Bug ID | The bug report for a failure |

---

## Example (fictional app: BookNest, an online bookstore)

| ID | Feature name | Test case name | Priority | Type | Precondition | Test data | Steps | Expected results | Traces to | Replaced by | Status 2026-11-12 | Actual result 2026-11-12 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TC-LOGIN-001 | Login | Log in with a wrong password | Critical | Negative | Logged out; on the login page | Email: `reader01@booknest.example`; password: `wrong-pass` | 1. Enter the email<br>2. Enter the wrong password<br>3. Click Log in | 1. Email is shown in the field<br>2. Password is masked<br>3. Error message "Incorrect email or password" is shown and the user stays on the login page *(message wording: Unverified)* | COND-LOGIN-02 | | Pass | |
