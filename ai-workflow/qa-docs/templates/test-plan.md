# Test plan template

Length target: max 3 pages; a reviewer should grasp it in 5 minutes. Scales and IDs are in [SKILL.md](../SKILL.md).

## Core sections (always included)

### 1. Introduction
What the plan covers and who it is for.

### 2. Test items
The app, version or build, URL, and features. If the app shows no version, record the test date and test environment instead.

### 3. Features to be tested (in scope)
The features this plan covers, each with its feature code. Each in-scope feature gets a short uppercase feature code (e.g. LOGIN, CART), named once here and used in all test condition and test case IDs, so the IDs stay consistent in every document.

### 4. Features not to be tested (out of scope)
The features left out, and why. Include any non-functional area with no measurable threshold.

### 5. Approach or test strategy
- **Test types:** whether testing will be functional, regression, security, performance or UI/UX. Types not listed go out of scope; non-functional types listed need a measurable threshold.
- **Manual vs automated:** what is tested by hand and what is automated.
- **Techniques:** the test design techniques used (see "How I choose techniques" in the test design). Needed because the test design is optional.
- **Tools** (conditional): include only when using more than a spreadsheet, e.g. Jira, a test management tool or an automation tool.
- **Results:** where test results are recorded: dated columns (default) or run log (when tests are re-run for each release). See the test case template.

### 6. Product risks
Each risk as a failure statement (what fails, and for whom), with likelihood, impact, risk level and mitigation (which tests cover it).

| Risk ID (`RISK-<NN>`) | Risk | Likelihood | Impact | Risk level | Mitigation |
| --- | --- | --- | --- | --- | --- |

### 7. Entry & exit criteria
**Entry criteria**
- Test environment is available and the app is reachable.
- Smoke test passes. Name the test account and the flow used.
- Test cases are reviewed against the test design, or against the in-scope features and product risks in the test plan when there is no test design. Name who reviews them (self-review on a solo project).
- Test data is ready.

**Exit criteria**
- All Critical-priority test cases executed.
- Every critical product risk is covered by at least one executed test.
- Critical risk results. Use one variant:
    - **Bugs are fixed by a team:** all tests covering critical risks pass, and there are no open critical/high defects.
    - **Bugs won't be fixed (practice or demo app):** all critical/high defects, including every failed test for a critical risk, are reported, reproduced and documented as known issues.
- Test summary report completed (listed in Test deliverables).

### 8. Test environment
The OS, browser and browser version, page size, and the app environment (e.g. staging or production).

### 9. Project risks and contingencies
Threats to the testing work itself, and the backup plan for each.

### 10. Test deliverables
The documents testing will produce. Must include the test summary report.

### 11. Test data requirements
The test accounts and data needed.

### 12. Pass/fail criteria
- **Pass:** every actual result matches the expected result.
- **Fail:** at least one actual result does not match the expected result.
- **Blocked:** the test cannot be run, e.g. a precondition cannot be met.
- Thresholds for any non-functional area in scope, e.g. "page loads in under N seconds".

### 13. Testing tasks and estimates
Rough estimate per task (e.g. hours), not a detailed plan.

### 14. Schedule / milestones
The sequence of testing work and its key dates.

### 15. Suspension & resumption criteria
- **Suspend** when a blocking issue (environment down, or the smoke test or main flow fails) makes the remaining tests impossible or meaningless.
- **Resume** when the blocker is fixed and the smoke test passes again.

### 16. Metrics
Named here; values go in the test summary report.
- Test execution: planned, executed, passed, failed, blocked.
- Critical-risk coverage: critical risks with at least one executed test, out of all critical risks.
- Defects by severity.

## Conditional sections (include when needed)

| Section | What goes in it | Include when |
| --- | --- | --- |
| Roles and responsibilities | Who does what in testing | More than one person works on testing |
| Staffing / training needs | Skills or people the testing needs | More than one person works on testing |
| Approvals / sign-off | Who accepts the plan or the results | Someone must formally accept the plan or the results |
| Identifier & change history | Plan version and what changed | Big project, or a team shares and updates the plan |

---

## Example (fictional app: BookNest, an online bookstore)

1. **Introduction:** Functional testing of the BookNest web store, for the QA reviewer.
2. **Test items:** BookNest web app, no version shown; tested 2026-11-10 on the environment in section 8. URL: `https://booknest.example`. Features: login, search, cart, checkout.
3. **In scope:** Login (`LOGIN`), Search (`SEARCH`), Cart (`CART`), Checkout (`CHECKOUT`).
4. **Out of scope:** Payment provider pages (third party); performance (no threshold set).
5. **Approach:** Test types: functional and UI/UX. Manual testing; no automation yet. Techniques: equivalence partitioning and boundary value analysis. Results: dated columns (single test cycle). (No tools section: spreadsheet only.)
6. **Product risks:**

| Risk ID (`RISK-<NN>`) | Risk | Likelihood | Impact | Risk level | Mitigation |
| --- | --- | --- | --- | --- | --- |
| RISK-01 | A registered customer can't log in | Medium | High | Critical | Login test cases |
| RISK-02 | Search returns no results for a book title that exists | Medium | Medium | Moderate | Search test cases |

7. **Entry & exit criteria:** as listed above, using the "bugs won't be fixed" variant (demo app). Smoke test: log in with `reader01`.
8. **Test environment:** Windows 11, Chrome 130, 1366×768, staging.
9. **Project risks:** The demo site may go offline. Contingency: continue writing test cases and retest when it is back.
10. **Test deliverables:** Test plan, test design, test cases, bug reports, test summary report.
11. **Test data:** Test account `reader01`; one book title that exists in the catalog.
12. **Pass/fail criteria:** as listed above; no non-functional thresholds (performance is out of scope).
13. **Tasks and estimates:** Test design ~3 h; test cases ~4 h; execution ~3 h; bug reports ~2 h.
14. **Schedule:** Test design → test cases → execution → summary report, by 2026-11-20.
15. **Suspension & resumption:** as listed above; main flow = login and search.
16. **Metrics:** as listed above.
