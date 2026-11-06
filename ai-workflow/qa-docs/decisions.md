# QA Documentation Skill: Decisions

Decisions for how my QA documents (test plan, test design, test case, bug report) are structured across my projects. Each decision records the options I considered, what I chose, and why.

Reference: [QA Documentation Structure Guide](https://claude.ai/artifact/AVJRYXRQXVzB6SZLoXNbnU)

## Decision 1: Test plan

Test plan sections are grouped into tiers. Core sections are always included. Conditional sections are included only when the project needs them.

### Core sections (always included)

1. Introduction
2. Test items: the app, version or build, URL, and features. If the app shows no version, record the test date and test environment instead.
3. Features to be tested (in scope). Each in-scope feature gets a short uppercase feature code (e.g. LOGIN, CART), named once here and used in all test condition and test case IDs, so the IDs stay consistent in every document.
4. Features not to be tested (out of scope)
5. Approach or test strategy
6. Product risks (see "How I'll describe risks")
7. Entry & exit criteria (see below)
8. Test environment: the OS, browser and browser version, page size, and the app environment (e.g. staging or production)
9. Project risks and contingencies
10. Test deliverables
11. Test data requirements
12. Pass/fail criteria (see below)
13. Testing tasks and estimates: rough estimates per task (e.g. hours), not a detailed plan.
14. Schedule / milestones
15. Suspension & resumption criteria (see below)
16. Metrics (see below)

### Conditional sections (include when needed)

| Section | Include when |
| --- | --- |
| Roles and responsibilities | More than one person works on testing |
| Staffing / training needs | More than one person works on testing |
| Approvals / sign-off | Someone must formally accept the plan or the results |
| Identifier & change history | Big project, or a team shares and updates the plan |

### Approach or test strategy

- **Test types:** whether testing will be functional, regression, security, performance or UI/UX. Types not listed go out of scope; non-functional types listed need a measurable threshold.
- **Manual vs automated:** what is tested by hand and what is automated.
- **Techniques:** the test design techniques used (see "How I choose techniques" in the test design). Needed because the test design is optional.
- **Tools** (conditional): include only when using more than a spreadsheet, e.g. Jira, a test management tool or an automation tool.
- **Results:** where test results are recorded: dated columns (default) or run log (when tests are re-run for each release). See the test case decision.

Excluded from the approach:
- Defect management process: covered by the bug report rules (status flow, severity and priority).
- Risk-based depth: priority and the exit criteria already make Critical risks get attention first; depth is left to judgment.

### Pass/fail criteria

- **Pass:** every actual result matches the expected result.
- **Fail:** at least one actual result does not match the expected result.
- **Blocked:** the test cannot be run, e.g. a precondition cannot be met.
- Any non-functional area in scope (e.g. performance) needs a measurable threshold, e.g. "page loads in under N seconds". If no threshold can be set, list the area as out of scope.

### Entry criteria

- Test environment is available and the app is reachable.
- Smoke test passes. The plan names the test account and the flow used.
- Test cases are reviewed against the test design, or against the in-scope features and product risks in the test plan when there is no test design. The plan names who reviews them (self-review on a solo project).
- Test data is ready.

### Exit criteria

- All Critical-priority test cases executed.
- Every critical product risk is covered by at least one executed test.
- Critical risk results, depending on whether bugs will be fixed:
    - **Bugs are fixed by a team:** all tests covering critical risks pass, and there are no open critical/high defects.
    - **Bugs won't be fixed (practice or demo app):** all critical/high defects, including every failed test for a critical risk, are reported, reproduced and documented as known issues.
- Test summary report completed. It must be listed in Test deliverables.

### Defect severity

The exit criteria use a defect severity scale that is separate from the risk level, because risk and bug severity are different: a risk level combines likelihood and impact before testing; severity is the impact of a bug that was actually found. A separate scale also gives clarity for the bug report. This scale is reused in the bug report decisions.

| Severity | Means |
| --- | --- |
| **Critical** | Core task impossible with no workaround, crash, data loss or a security issue |
| **High** | An important feature is broken, but the core task is still possible |
| **Medium** | A feature behaves wrongly, but there is an easy workaround |
| **Low** | Cosmetic issue, typo, minor inconvenience |

### Suspension & resumption criteria

Core, because things like the environment going down or a login failure during testing are inevitable and block the later testing.

- **Suspend** when a blocking issue (environment down, or the smoke test or main flow fails) makes the remaining tests impossible or meaningless.
- **Resume** when the blocker is fixed and the smoke test passes again.

### Metrics

Core, because the exit criteria need these numbers. The plan names the metrics; the test summary report shows their values.

- Test execution: planned, executed, passed, failed, blocked.
- Critical-risk coverage: critical risks with at least one executed test, out of all critical risks.
- Defects by severity.

### How I'll describe risks

- Each risk is written as a failure statement: what fails, and for whom.
- Fields: risk, likelihood, impact, risk level, mitigation (which tests cover it).
- Risk ID format: `RISK-<NN>`, e.g. `RISK-01`. Risks are few and set once in the test plan, and a risk can involve several features.
- Likelihood and impact are each rated High / Medium / Low.
- Risk level is Critical / Moderate / Low, read from the risk matrix below. I chose a matrix because it is easier to read and commonly used in the industry.

| Rating | Impact means | Likelihood means |
| --- | --- | --- |
| **High** | Users can't complete a core task (e.g. log in, pay) | Complex, new or recently changed area, or one with a history of bugs |
| **Medium** | A feature is broken, but there is a workaround | Normal complexity, some changes |
| **Low** | Cosmetic or minor inconvenience | Simple and stable, rarely changes |

**Risk matrix**

| Impact ↓ / Likelihood → | Low | Medium | High |
| --- | --- | --- | --- |
| **High** | Critical | Critical | Critical |
| **Medium** | Low | Moderate | Critical |
| **Low** | Low | Low | Moderate |

Any high-impact risk is Critical, even when it is unlikely: I focus on the impact, because we never know whether it will happen.

Length target: “Max 3 pages; a reviewer should grasp it in 5 minutes.”


## Decision 2: Test design
Test design is separate from the test cases. It is optional on very small projects (e.g. a single feature); then the test conditions and traceability are recorded in the test case file, and the techniques in the test plan's approach section.

Why: test conditions (what to check) stay the same while test cases (how to check) change with the app. On a very small project, the conditions fit in the test case file, so a separate document adds little.

### Core sections (always included)
1. Identifier: the ID of each test condition, which the test cases trace to (format in Rules)
2. Features: the features to be tested. They must match the in-scope features in the test plan.
3. Test conditions: every scenario to be tested, with its test type (functional or non-functional)
4. Test design techniques applied (see "How I choose techniques")
5. Priority: the risk level of the traced risk (Critical / Moderate / Low), because then I don't need a third scale, and the priority can't contradict the test plan.
6. Traceability: Each test condition traces to at least one product risk ID from the test plan, and to a requirement or user story when one exists. This lets me check the exit criterion "every critical risk is covered" and spot any risk that has no test before testing starts.

### Conditional sections (include when needed)

| Section | Include when |
| --- | --- |
| Approach refinements: special handling, such as test data reset or run order | A feature needs special setup, test data or run order |
| Feature pass/fail criteria: a feature passes when all test cases for its Critical conditions pass | Features are accepted or released one at a time |

Why conditional: approach refinements are only needed when a feature has special setup or run order, and feature pass/fail is only needed when features are accepted one at a time. Otherwise, the exit criteria already cover it.

### Rules
- Test condition ID format: `COND-<FEATURE>-<NN>`, e.g. `COND-LOGIN-01`.
- Layout: one table with a row per test condition (columns: Condition ID, Feature, Test condition, Test type, Technique, Priority, Traces to). Up to 5 features: one table for all conditions. More than 5 features: one table per feature, under a heading with the feature name.
- One test condition can have more than one test case. Each test case traces to one test condition.
- The test condition is general; the test case is more specific. For example, the condition says "display an error message when the password is wrong"; the test case gives the exact error message wording, based on the app.

### How I choose techniques
- Equivalence partitioning: when there are a lot of data to test and they could be grouped into classes the app treats the same way. Test one value per class.
- Boundary value analysis: when an input has limits, such as a minimum or maximum length or a number range. Test at, just below and just above each limit.
- Decision table: when the result depends on a combination of conditions, such as which fields are filled or empty.
- State transition: when the app behaves differently depending on its current state, such as logged in or out, or an empty or non-empty cart. Test valid and invalid transitions between states.
- Error guessing: used on almost every functional test case, mostly during exploratory testing.

### To exclude
1. Assumptions section: because I check the real app when I write the test cases. The condition stays general, and the test case gets the exact behavior from the app (see the test case rule "Expected results are checked in the real app, not assumed").


## Decision 3: Test case
### Core sections (always included)
1. ID: `TC-<FEATURE>-<NNN>`, e.g. `TC-LOGIN-001`. Unique for the app, with no duplicates, so a test case can be traced in the future if it is updated into one or several new test cases or deleted. An ID is never reused and never changes, even if the test case is edited or its feature is renamed.
2. Feature name: the feature the test case belongs to
3. Test case name: follows the pattern `[Action] with/when [condition]`, e.g. "Log in with a wrong password". It names what is done, not the result, so the name stays correct if the expected result changes; the feature is already in its own column.
4. Priority: Critical/Moderate/Low, the risk level of the traced condition or risk
5. Type: Positive / Negative / Edge case. Edge case: a test at a limit (boundary) or an unusual case, e.g. maximum length or an empty list. Edge cases are not as important as positive and negative cases: if the limit is important, label the test Positive or Negative; if it needs testing but its impact is not so high, label it Edge case.
6. Precondition: the condition that must be met before the test case can be run
7. Test data: the exact user, inputs and values used in the test
8. Steps: every step needed to run the test case
9. Expected results: the expected result of each step. For example, step 1 has expected result 1. Expected results are checked in the real app, not assumed.
10. Traceability (Traces to): the test condition ID when there is a test design; otherwise, the product risk ID from the test plan.
11. Replaced by: when a test case is split, replaced or deleted, keep its row and write the new test case ID(s), or "Deleted" with the reason. Empty while the test case is active.

### Conditional sections (include when needed)
1. Objective/description: include when the test case name is too short or not informative
2. Environment: include when the tests run on several environments; otherwise it is set once in the test plan.
3. Tags (e.g. smoke, regression): include when automating, or when keeping a smoke or regression set.

### Rules
- Each test case is independent: it does not depend on another test case.
- Priority, Type and Status use dropdowns.
- Format: spreadsheet: a downloadable .xlsx (with dropdowns) plus a .csv copy so viewers can see it directly on GitHub. Export the .csv again whenever the .xlsx changes.

### Test results
Results are kept separate from the test case definition. Use one method per project, not both, so the metrics are counted from one place.

- **Default: dated result columns** in the test case sheet: a new Status + Actual result pair for each run, with the run date in the column header. Good for a development cycle with a few runs.
- **Conditional: Run log sheet** in the same .xlsx, one row per run of one test case. Include when the test cases are re-run for each release (regression), or automated tests run often.

**When to choose:** once, when writing the test plan, before the first run. Ask: will the same test cases be run again for future releases? No → default. Yes → run log. Record the choice in the test plan's approach section. If the project changes later, switch to the run log from that point and note it in the plan.

Each run records:
- Status: Pass / Fail / Blocked
- Actual result: what actually happened, mainly when the test case fails or is blocked

Run log columns: Run date, Test case ID, Status, Actual result, Environment, Tester, Bug ID.

### To exclude
1. Inter-case dependencies: each test case is independent.
2. Author / date: git history covers it.



## Decision 4: Bug report
### Core sections (always included)
1. ID: `BUG-<NNN>`, e.g. `BUG-001`. Bugs can come from anywhere, including outside the QA team, and may not belong to one feature; the linked test case shows the feature.
2. Date: needed because sometimes someone outside the QA team finds the bug
3. Reporter: needed because sometimes someone outside the QA team finds the bug
4. Title/summary: follows the pattern `[Feature]: [what goes wrong] when [condition]`
5. Actual result: what happens when the bug occurs, as observed during testing (not after the fix)
6. Environment: the OS, browser and browser version, page size, and the app environment (e.g. staging or production)
7. Precondition: the conditions needed before reproducing the bug, such as the user account or test data to use
8. Steps to reproduce: the steps that make the bug happen
9. Expected result: one expected result for the bug itself. Unlike a test case, where each step has its own expected result, a bug can have several steps to reproduce but only one expected result.
10. Severity: Critical/High/Medium/Low (the defect severity scale from Decision 1)
11. Attachments/evidence: evidence link
12. Reproducibility: how many times the bug happened out of the attempts, e.g. 5/5, 3/5 or 1/10. If the bug doesn't happen every time, try at least 5 times and record the count.
13. Status: New → Open → Fixed → Retest → Closed. If the retest fails: Retest → Reopened → Fixed → Retest, until it passes. If the bug won't be fixed: Open → Known issue (see "Status flow").

### Status flow

| Status | Means |
| --- | --- |
| **New** | Just reported, not yet confirmed |
| **Open** | Confirmed, waiting for a fix |
| **Fixed** | The developer says it's fixed |
| **Retest** | QA is checking the fix |
| **Closed** | The fix is confirmed by the retest |
| **Reopened** | The retest failed, so it goes back to the developer |
| **Known issue** | The bug won't be fixed, for example because its severity is Low |


### Conditional sections (include when needed)
1. Impact or risk assessment: include when severity is Critical or High, or when the business effect isn't obvious from the title
2. Root cause/corrective action: include when bugs are fixed and the developer shares the cause
3. Priority: High / Medium / Low. Include when there are many bugs; if there are only a few, severity is enough. Priority can be set by someone other than QA, e.g. the project manager; QA sets the severity.
4. Linked test case: the test case ID. Include when the bug was found by a test case.

### Rules
- Format: spreadsheet (same as the test cases): a downloadable .xlsx plus a .csv copy for GitHub.


## Decision 5: Test summary report
Why: the exit criteria require a completed test summary report, and the metrics named in the test plan need a place for their values.

### Sections (always included)
1. Summary: what was tested, when, and the overall result
2. Scope vs plan: anything tested differently from the plan, and why. If nothing differs, one line saying all in-scope features were tested as planned.
3. Metrics: the values of the metrics named in the test plan
4. Defects: the bugs found, whether each is fixed or a known issue, and why it stays a known issue
5. Exit criteria check: each exit criterion, marked met or not met
6. Conclusion: whether testing is complete and the app is ready, plus the risks that remain
