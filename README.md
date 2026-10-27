# MeraTrade — Expense Claim & Approval System

**Business Analyst · Independent Portfolio Project** · Oct 2026

A Business Analysis case study on an internal system where employees submit expense claims, managers approve them, and Finance reviews, exports and records payment. It covers the whole path from a claim being created to a payment being recorded.

> [!NOTE]
> MeraTrade Distribution is a fictional company and all people and data are invented. I have not interviewed any stakeholder, built the system or run any test. The documents are complete for portfolio purposes but have **not** been approved as a business baseline. Where a decision was needed to finish the case study, it is marked as a BA recommendation.

**Short on time?** Read the [Case Study](docs/01-case-study.md) (about 9 pages), then look at the [wireframes](#screens-and-diagrams) and the [Validation Workbook](docs/05-validation-workbook.md).

## Overview

- **Organisation:** a distribution company with about 400 employees in Da Nang, Ha Noi and Ho Chi Minh City. Sales staff travel often and claim many expenses.
- **Question:** How can employees see where a claim is, apply the expense policy consistently, avoid paying the same receipt twice, and reduce Finance's manual work?
- **Output:** case study, elicitation plan, SRS, product backlog with delivery plan, and a validation workbook with a traceability matrix and UAT test cases.

## Business problem and objectives

**Assumed current state.** Claims are prepared in Excel, approved by e-mail and checked against paper receipts. Finance then types each item into the accounting software and builds the monthly report by hand. These problems are assumptions based on common practice; MeraTrade has not confirmed them.

The proposed system has five objectives ([SRS §2.1.3](docs/03-srs.md)):

1. Employees can see where their claim is.
2. The expense policy is applied consistently.
3. The risk of paying the same expense twice is lower.
4. Finance does less manual work.
5. The monthly expense report is faster to prepare.

| In the MVP | Out of scope |
|---|---|
| Claim submission with checks, one- or two-level approval by amount, duplicate warning, Finance review, CSV export to accounting, recording import results and payments, status tracking, e-mail notifications, a basic spending report, and maintenance of categories, settings and employees | Money transfers, tax calculation, cash advances, corporate cards, foreign currencies, OCR, API integration and a mobile app |

## My role

This is an independent portfolio project. It is not client work and not part of my employment. I:

- analysed the problem and defined the objectives and the scope of the MVP
- wrote the SRS: requirements, business rules, wireframes, diagrams, data model and the accounting export interface
- wrote 16 user stories with 74 acceptance criteria in Given / When / Then form
- designed the requirements traceability matrix (RTM) and 22 UAT test cases
- planned the interviews that would check my assumptions, and listed the open questions
- wrote a simulated change request (CR-01) and assessed its impact across the documents

## Key design decisions

Each decision has options, a choice, a trade-off and the question that would confirm it ([Case Study §5](docs/01-case-study.md#5-solution-options-and-key-decisions), [SRS Appendix A](docs/03-srs.md#appendix-a-decision-log)).

| Decision | What I chose | Why |
|---|---|---|
| Build or buy | Fit-gap one or two existing expense products first; build only if a Must requirement cannot be met | Faster start with a proven workflow. The SRS stays neutral, so it works for both paths. |
| Claim status vs. import result | Two separate fields: claim status and export status. An unknown import result keeps the claim in *Awaiting Confirmation*. | Exporting a file does not mean accounting has booked it. Without this, Finance could pay a claim that was never booked. |
| Duplicate receipts | Warn, let the employee confirm with "Submit anyway", then Finance decides on each flagged line | A match is not proof of fraud. Two identical taxi fares in one day are normal. |
| Accounting interface | CSV file imported by Finance, with the result recorded per claim | The accounting software's import template and API are unknown. |
| Own claims | Nobody approves, verifies, exports, records the import result for, or pays their own claim. The System Administrator has no Finance permissions. *(BA recommendation)* | Recording "Imported" opens the way to payment. It needs a second person. |

## Requirements and traceability

| Item | Count |
|---|---|
| Functional requirements | 16 (14 Must, 2 Should) |
| Non-functional requirements | 8 (6 Must, 2 Should) |
| Business rules | 12 |
| Use cases | 10 |
| User stories | 16, matching FR-01 to FR-16 one to one |
| Acceptance criteria | 74 |
| UAT test cases | 22 (designed, **not executed**) |
| Open questions | 22 (20 open, 2 settled for the case study by a BA recommendation) |

The [RTM](docs/05-validation-workbook.md#2-requirements-traceability-matrix-rtm) links each requirement to its business rules, open questions, user story and test cases, and states what kind of check it needs:

| Coverage | Requirements |
|---|---|
| UAT | 15 |
| UAT + technical check (by IT/QA) | 6 |
| Technical check only | 2 |
| Blocked by an open question | 1 |

One trace from the RTM:

| Risk | Requirement | Business rule | Test case |
|---|---|---|---|
| The import result is not known yet, so the claim could be re-exported or paid | [FR-10](docs/03-srs.md) Record the import result | BR-11 Export eligibility | TC-13, TC-14: the claim stays in Awaiting Confirmation and cannot be exported again, returned or paid |

Some checks cannot be done in UAT. For example, refusing requests sent outside the screens, or two people exporting the same claim at the same moment, need a technical check. The workbook marks these instead of claiming full coverage.

## Screens and diagrams

[![Claim form wireframe: blocking issues, flags and route preview](assets/wireframes/claim-form-state-a.png)](assets/wireframes/claim-form-state-a.png)

*Claim form after the first Submit: a missing receipt blocks submission, a duplicate warning and an over-limit flag are shown on the line, and the route is previewed ([SRS §3.3](docs/03-srs.md#33-gui-requirements)).*

[![Finance wireframe: batches awaiting import result](assets/wireframes/export-batches-awaiting-result.png)](assets/wireframes/export-batches-awaiting-result.png)

*Finance screen after generating a file: results are recorded per claim, and the officer's own claim has no result option.*

[![Activity diagram from claim to payment](assets/diagrams/activity-diagram.png)](assets/diagrams/activity-diagram.png)

*Main flow from creating a claim to recording payment. Select an image to open it at full size.*

All diagrams and wireframes are in [`assets/`](assets): system context, use cases, activity, claim states, logical ERD and seven screens.

## Validation approach

- Every acceptance criterion is covered by at least one test case, and every test case names the criteria it checks.
- The test data uses fictional employees, departments and example policy settings ([Validation Workbook §4](docs/05-validation-workbook.md#4-test-data)).
- Business-level test cases cover the high-risk flows: approval thresholds, return and resubmission, duplicate decisions, unknown import results, outdated export screens and self-confirmation.
- CR-01 shows how a change request would be assessed: it is a requirement change, not a configuration change, so 15 items in the SRS, backlog, diagrams and test cases would need updating and 5 test cases re-running. It is simulated and **not approved**.

## Tools and techniques

- **Tools:** Word, Excel, draw.io for diagrams, and wireframes drawn as SVG that can be imported into Figma
- **Techniques:** SRS writing (shall statements with IDs and MoSCoW priorities), business rules, use case specifications, As-Is / To-Be flow, gap analysis, build-or-buy options analysis, state and data modelling, user stories with Given / When / Then criteria, requirements traceability, UAT test design, impact analysis of a change request, elicitation planning and open-question tracking

## Repository structure

```
.
├── README.md                  Project overview (this page)
├── docs/                      Documents in Markdown, readable on GitHub
│   ├── 01-case-study.md
│   ├── 02-elicitation-plan.md
│   ├── 03-srs.md
│   ├── 04-product-backlog-and-delivery-plan.md
│   └── 05-validation-workbook.md
├── assets/
│   ├── diagrams/              Context, use case, activity, state and ERD
│   └── wireframes/            Seven screens
└── source-files/              Original Word and Excel files
```

## How to explore the artifacts

| # | Document | What to look at |
|---|---|---|
| 01 | [Case Study](docs/01-case-study.md) | **Start here.** Problem, gaps, process, decisions, example scenarios and limits in about 9 pages |
| 02 | [Elicitation Plan](docs/02-elicitation-plan.md) | Interview plan, questions, assumptions to confirm and baseline measures. A plan only, with no results |
| 03 | [SRS](docs/03-srs.md) | Requirements, business rules, use cases, wireframes, diagrams, accounting export, data model, decision log and open questions |
| 04 | [Product Backlog & Delivery Plan](docs/04-product-backlog-and-delivery-plan.md) | 16 user stories, 74 acceptance criteria and a proposed delivery plan |
| 05 | [Validation Workbook](docs/05-validation-workbook.md) | RTM, 22 test cases, test data and the CR-01 impact analysis |

The same content is in the original Word and Excel files in [`source-files/`](source-files).

## Limitations and conclusion

- The problem, the current process and all rules are assumptions based on common practice. MeraTrade has not confirmed them.
- No interviews were held. The Elicitation Plan only shows how the assumptions would be checked, and its participants would act as proxies for MeraTrade roles.
- The CSV column mapping has not been compared with a real import template, and the case where accounting accepts only part of a claim is not resolved.
- There is no baseline and no target for the success measures, so no improvement is claimed. Test cases check requirements; they do not prove that the measures will improve.
- Who may record import results, and one system role per employee, are BA recommendations that still need to be confirmed by the CFO, Finance and IT.

The case study shows how I turned an unclear business need into traceable requirements: separating what is known from what is assumed, showing the trade-off behind each decision, and marking which checks need more than UAT.
