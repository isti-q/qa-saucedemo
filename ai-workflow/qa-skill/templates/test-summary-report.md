# Test summary report template

Written at the end of testing. It shows what was tested, what was found, and whether the exit criteria in the test plan are met. Scales and IDs are in [SKILL.md](../SKILL.md).

## 1. Summary
What was tested, when, and the overall result in one or two lines.

## 2. Scope vs plan
Anything tested differently from the test plan, and why. If nothing differs, one line: all in-scope features were tested as planned.

## 3. Metrics
The values of the metrics named in the test plan:
- Test execution: planned, executed, passed, failed, blocked.
- Critical-risk coverage: critical risks with at least one executed test, out of all critical risks.
- Defects by severity.

## 4. Defects
The bugs found, with their severity and whether each is fixed or a known issue. For each known issue, say why it stays a known issue.

| Bug ID | Title | Severity | Fixed / Known issue | Why it stays a known issue |
| --- | --- | --- | --- | --- |

## 5. Exit criteria check
Each exit criterion from the test plan, marked met or not met.

| Exit criterion | Met / Not met | Note |
| --- | --- | --- |

## 6. Conclusion
Whether testing is complete and the app is ready, plus the risks that remain.

---

## Example (fictional app: BookNest, an online bookstore)

1. **Summary:** Functional testing of login and search on BookNest (staging), 10–12 Nov 2026. All exit criteria are met; one High bug remains as a known issue.
2. **Scope vs plan:** Cart and checkout were not tested: the staging checkout page was offline during the test window. Login and search were tested as planned.
3. **Metrics:** 12 planned, 11 executed, 10 passed, 1 failed, 1 blocked. Critical-risk coverage: 1/1. Defects: 0 Critical, 1 High, 0 Medium, 0 Low.
4. **Defects:**

| Bug ID | Title | Severity | Fixed / Known issue | Why it stays a known issue |
| --- | --- | --- | --- | --- |
| BUG-001 | Search: no results shown when the title contains an apostrophe | High | Known issue | Demo app: bugs are not fixed |

5. **Exit criteria check** (variant: bugs won't be fixed):

| Exit criterion | Met / Not met | Note |
| --- | --- | --- |
| All Critical-priority test cases executed | Met | 3/3 |
| Every critical product risk covered by at least one executed test | Met | RISK-01 covered by TC-LOGIN-001 to TC-LOGIN-003 |
| All critical/high defects reported, reproduced and documented as known issues | Met | BUG-001 (5/5) |
| Test summary report completed | Met | This report |

6. **Conclusion:** Testing of login and search is complete. Cart and checkout remain untested, so their risks are still open.
