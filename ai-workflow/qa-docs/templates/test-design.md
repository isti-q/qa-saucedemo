# Test design template

Test design is separate from the test cases. It is optional on very small projects (e.g. a single feature); then the test conditions and traceability are recorded in the test case file, and the techniques in the test plan's approach section. Scales and IDs are in [SKILL.md](../SKILL.md).

## Core sections (always included)

### 1. Identifier
The ID of each test condition, which the test cases trace to. Format: `COND-<FEATURE>-<NN>`.

### 2. Features
The features to be tested. They must match the in-scope features in the test plan, using the same feature codes.

### 3. Test conditions
Every scenario to be tested, with its test type (functional or non-functional). Keep each condition general; the test cases add the specific details. One condition can have more than one test case.

### 4. Test design techniques applied
The technique used for each condition. Choose it this way:
- **Equivalence partitioning:** when there is a lot of data to test and it can be grouped into classes the app treats the same way. Test one value per class.
- **Boundary value analysis:** when an input has limits, such as a minimum or maximum length or a number range. Test at, just below and just above each limit.
- **Decision table:** when the result depends on a combination of conditions, such as which fields are filled or empty.
- **State transition:** when the app behaves differently depending on its current state, such as logged in or out, or an empty or non-empty cart. Test valid and invalid transitions between states.
- **Error guessing:** used on almost every functional test case, mostly during exploratory testing.

### 5. Priority
The risk level of the traced risk: Critical / Moderate / Low.

### 6. Traceability
At least one product risk ID from the test plan, plus a requirement or user story when one exists.

**Layout:** up to 5 features: one table for all conditions. More than 5 features: one table per feature, under a heading with the feature name.

| Condition ID | Feature | Test condition | Test type | Technique | Priority | Traces to |
| --- | --- | --- | --- | --- | --- | --- |

## Conditional sections (include when needed)

| Section | What goes in it | Include when |
| --- | --- | --- |
| Approach refinements | Special handling, such as test data reset or run order | A feature needs special setup, test data or run order |
| Feature pass/fail criteria | A feature passes when all test cases for its Critical conditions pass | Features are accepted or released one at a time |

---

## Example (fictional app: BookNest, an online bookstore)

**Features:** Login, Search

| Condition ID | Feature | Test condition | Test type | Technique | Priority | Traces to |
| --- | --- | --- | --- | --- | --- | --- |
| COND-LOGIN-01 | Login | Log in with a valid email and password | Functional | Equivalence partitioning | Critical | RISK-01 |
| COND-LOGIN-02 | Login | Display an error message when the password is wrong | Functional | Equivalence partitioning | Critical | RISK-01 |
| COND-SEARCH-01 | Search | Search with a title at the maximum length the search field accepts | Functional | Boundary value analysis | Moderate | RISK-02 |
