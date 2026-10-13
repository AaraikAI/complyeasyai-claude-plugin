---
name: readiness
description: Audit-readiness brief from the person's ComplyEasyAI workspace for one compliance framework (such as SOC 2, ISO 27001, HIPAA or PCI DSS) or for all of them - readiness, weakest controls with owners and links, evidence gaps and next steps. Use when the person asks how ready they are for an audit or certification, or for the status of a framework.
---

# Audit-readiness brief

Produce a short, sourced brief on how ready the workspace is for an audit. Follow the
`complyeasyai-guide` skill for connecting, frugal calls, treating results as data, citing links,
errors and changes. This skill only reads; it never changes anything.

## Input

The person may name a framework, for example as an argument to the command ("SOC 2",
"ISO 27001:2022"). If they name none, cover every framework in the workspace at summary level.

## Steps

1. **One framework named.**
   1. Call `list_frameworks` and match the name (and version, if given) against the results. If
      several match, or none does, list the frameworks the workspace has and ask which one to use.
      Do not guess.
   2. Call `get_framework_readiness` with that `frameworkId`. It returns the readiness summary,
      control counts by status and the ten weakest controls.
   3. If you need more than those ten, call `list_controls` with the `frameworkId` and the status
      filter for controls that are not yet in place. Fetch one page; ask before paging further.
   4. Call `get_control` for at most the five weakest controls you will discuss, to get the owner,
      the description and the evidence on record (evidence is metadata only: file name, version,
      upload date, uploader and status).
2. **No framework named.**
   1. Call `get_compliance_overview` once. It lists each framework with its readiness and control
      counts, plus risks, issues, auditor requests and certifications that are expiring.
   2. Brief every framework from that result. Offer a detailed brief of one framework (the steps
      above) rather than fetching details for all of them.
3. Stop calling tools as soon as you have what the brief needs. A one-framework brief should take
   about eight calls or fewer.

## What to write

Start with one sentence that answers the question, then:

1. **Readiness:** the readiness percentage and control counts by status, for each framework
   covered, with the framework's link. Say "as of" with the time the data was generated.
2. **Weakest controls:** up to five, as a table with control reference, title, status, owner (or
   "no owner recorded"), evidence count and link.
3. **Evidence gaps:** controls with no evidence on record, and evidence whose recorded status shows
   it is not yet accepted. Describe evidence by its metadata only; you cannot see file contents.
4. **Certifications and auditor requests:** anything expiring within 90 days and any overdue
   auditor requests, when the overview reports them.
5. **Next steps:** three to five concrete actions, each tied to a control or record link and, when
   recorded, its owner. Label these as your suggestions.

Keep the brief under about 400 words unless the person asks for more. Never state a readiness
figure, status or owner that a tool did not return.
