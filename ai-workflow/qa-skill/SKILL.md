---
name: qa-docs
description: Use when writing or reviewing a test plan, test design, test cases, or bug reports for a software QA project, so every document follows one structure, one set of scales and one traceability chain from risk to bug.
---

# QA docs

Four QA documents that link by ID: **product risk → test condition → test case → bug report**. Each template lists its sections in order, with core sections (always included) and conditional sections (included only when their "include when" trigger applies).

## Before writing

If the app name, environment, test accounts or feature list aren't in the project context, ask before writing. Every section downstream depends on them, so a guess here makes the whole document wrong.

## Which template

| Task | Template |
| --- | --- |
| Set scope, product risks, entry/exit criteria | [templates/test-plan.md](templates/test-plan.md) |
| Turn in-scope features and risks into test conditions | [templates/test-design.md](templates/test-design.md) (optional on very small projects) |
| Write step-by-step tests (spreadsheet) | [templates/test-case.md](templates/test-case.md); start from `templates/test-case.xlsx` |
| Report a defect (spreadsheet) | [templates/bug-report.md](templates/bug-report.md); start from `templates/bug-report.xlsx` |
| Report the result at the end of testing | [templates/test-summary-report.md](templates/test-summary-report.md) |

Write them in this order: each document traces to the one before it.

## Quality rules

- **Never invent UI elements, messages or behavior.** Write only what the project context or the real app shows.
- **Mark anything not verified in the real app as "Unverified".**
- Expected results are checked in the real app, not assumed.
- Product risks are failure statements: what fails, and for whom.
- Test conditions are general; test cases are specific (e.g. the exact error message wording, taken from the app).
- Each test case is independent: it does not depend on another test case.
- Any non-functional area in scope needs a measurable threshold. If none can be set, list it as out of scope.
- Test results are kept separate from the test case definition.
- Spreadsheets are kept as .xlsx (working file) plus a .csv copy for viewing on GitHub. Export the .csv again whenever the .xlsx changes.
- Exit criteria use one of two variants: bugs are fixed by a team, or bugs won't be fixed (practice or demo app).

When reviewing a document, check it against its template and these rules: missing core sections, conditional sections without their trigger, broken traceability, and the wrong scale.

## Traceability and IDs

| Item | ID | Traces to |
| --- | --- | --- |
| Product risk | `RISK-<NN>`, e.g. `RISK-01` | — |
| Test condition | `COND-<FEATURE>-<NN>`, e.g. `COND-LOGIN-01` | At least one product risk ID; plus a requirement or user story when one exists |
| Test case | `TC-<FEATURE>-<NNN>`, e.g. `TC-LOGIN-001` | One test condition ID; or the product risk ID when there is no test design |
| Bug report | `BUG-<NNN>`, e.g. `BUG-001` | The test case ID, when the bug was found by a test case |

`<FEATURE>` is the feature code named for each in-scope feature in the test plan (e.g. LOGIN, CART); every document uses the same code. One test condition can have more than one test case. IDs are never reused and never change. A test case that is split, replaced or deleted keeps its row, with "Replaced by" filled in.

## Scales

**Risk level** (test plan). Rate likelihood and impact High / Medium / Low, then read the level from the matrix:

| Rating | Impact means | Likelihood means |
| --- | --- | --- |
| **High** | Users can't complete a core task (e.g. log in, pay) | Complex, new or recently changed area, or one with a history of bugs |
| **Medium** | A feature is broken, but there is a workaround | Normal complexity, some changes |
| **Low** | Cosmetic or minor inconvenience | Simple and stable, rarely changes |

| Impact ↓ / Likelihood → | Low | Medium | High |
| --- | --- | --- | --- |
| **High** | Critical | Critical | Critical |
| **Medium** | Low | Moderate | Critical |
| **Low** | Low | Low | Moderate |

**Priority** (test conditions and test cases): the risk level of the traced risk: Critical / Moderate / Low.

**Defect severity** (bug reports and exit criteria), separate from risk level:

| Severity | Means |
| --- | --- |
| **Critical** | Core task impossible with no workaround, crash, data loss or a security issue |
| **High** | An important feature is broken, but the core task is still possible |
| **Medium** | A feature behaves wrongly, but there is an easy workaround |
| **Low** | Cosmetic issue, typo, minor inconvenience |

**Bug priority** (conditional: include when there are many bugs; if there are only a few, severity is enough): High / Medium / Low. It can be set by someone other than QA, e.g. the project manager. QA sets the severity.

**Test result:** Pass (every actual result matches the expected result) / Fail (at least one does not) / Blocked (the test cannot be run, e.g. a precondition cannot be met).

**Bug status:** New → Open → Fixed → Retest → Closed. Retest fails → Reopened → Fixed → Retest. Won't be fixed → Known issue. Definitions are in [templates/bug-report.md](templates/bug-report.md).
