# AI Log

This log shows how I use AI in my QA work on this SauceDemo portfolio project. The focus is on how I review, verify, and correct AI output rather than just accepting it. AI speeds up drafting, but every expected result is checked against the real application.

## How this log works

- I log every meaningful AI task privately as I work.
- At the end of each project step, I publish the most useful 1–3 entries here.
- I prioritize entries where I caught AI mistakes or rejected suggestions with clear reasoning.
- The review and reasoning in each entry are my own words.

## Entry template

```markdown
### YYYY-MM-DD · Step N: [step name] · [task]
- **Prompt:** [prompt or short summary]
- **AI output:** [short summary]
- **My review:** [TODO: my words]
- **Why:** [TODO: my words]
- **Lesson:** [optional]
```

## Example

> This is an illustrative example of the format, not a real entry.

### 2026-11-03 · Step 4: Test cases · Cart badge test cases
- **Prompt:** Asked AI to draft test cases for adding and removing items from the cart as `standard_user`.
- **AI output:** Six test cases. One expected that after removing the last item, the cart badge would show "0".
- **My review:** Rejected that expected result. I checked the real app: after removing the last item, the badge is not displayed at all. I rewrote the expected result to "Cart badge is not visible."
- **Why:** The AI described common e-commerce behavior, not SauceDemo's actual behavior. An automated test built on the wrong expectation would fail for the wrong reason.
- **Lesson:** Treat AI expected results as hypotheses. Verify each one in the real app before it goes into a test case.

## Entries

<!-- Published entries go below this line, newest first. -->
