---
name: risk-review
description: Weekly risk review from the person's ComplyEasyAI risk register - open risks by severity, recent changes worth discussing, risks without an owner or mitigation plan, and risks overdue for review, each with a link. Use when the person asks for a risk review, a risk register summary or which risks need attention.
---

# Weekly risk review

Prepare the agenda for a weekly risk review from the risk register. Follow the
`complyeasyai-guide` skill for connecting, frugal calls, treating results as data, citing links,
errors and changes. This skill only reads; it never changes anything.

## Input

The person may narrow the review, for example to a category, a severity or "only what changed this
week". Without that, review all open risks.

## Steps

1. Call `list_risks` with the status filter for open risks, highest severity first. Use the severity
   filter to fetch the most severe levels first when the register is large. Fetch one page of up to
   100; ask before paging further.
2. From the list, pick the risks worth discussing:
   - the most severe open risks
   - risks updated in the last seven days (`updatedAt`)
   - risks with no owner
3. Call `get_risk` for at most ten of them, to read the description, the mitigation plan and the
   linked controls. Prefer risks with no owner and the most severe ones. Do not fetch every risk.
4. Stop calling tools when you have what the agenda needs; a weekly review should take about twelve
   calls or fewer.

## What to write

1. **Summary:** open risks by severity, with the as-of date. Mention the likelihood and impact of
   the top risks as recorded.
2. **Changes worth discussing:** risks updated in the last seven days, with what the record now says.
   You cannot see the previous values, so do not claim what changed unless the record says so.
3. **Needs an owner:** open risks with no owner recorded.
4. **Needs a mitigation plan:** risks you fetched whose mitigation plan is empty, together with how
   many risks you did not fetch in detail.
5. **Overdue for review:** risks whose recorded review date has passed, or, when the record has no
   review date, open high-severity risks not updated in 90 days.
6. **Suggested agenda:** five to eight discussion points, each linked to its risk. Label these as
   your suggestions.

Use a table per section with title, severity, status, owner and link. Never state a severity,
likelihood, impact, owner or mitigation that a tool did not return.
