# MeraTrade — Expense Claim & Approval System

**Business Analyst · Independent Portfolio Project** · Oct 2026

A Business Analysis case study on an internal system where employees submit expense claims, managers approve them, and Finance reviews, exports and records payment. It covers the whole path from a claim being created to a payment being recorded.

> [!NOTE]
> MeraTrade Distribution is a fictional company and all people and data are invented. I have not interviewed any stakeholder, built the system or run any test. The documents are complete for portfolio purposes but have **not** been approved as a business baseline. Where a decision was needed to finish the case study, it is marked as a BA recommendation.

**Short on time?** Read the [Case Study](docs/01-case-study.md) (about 9 pages), then look at the [wireframes](#screens-and-diagrams) and the [SRS](docs/03-srs.md).

## Overview

- **Organisation:** a distribution company with about 400 employees in Da Nang, Ha Noi and Ho Chi Minh City. Sales staff travel often and claim many expenses.
- **Question:** How can employees see where a claim is, apply the expense policy consistently, avoid paying the same receipt twice, and reduce Finance's manual work?
- **Output:** case study, elicitation plan, SRS, and a product backlog with user stories, acceptance criteria and a delivery plan.

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
- mapped each user story one to one to a functional requirement
- planned the interviews that would check my assumptions, and listed the open questions

## Key design decisions

Each decision has options, a choice, a trade-off and the question that would confirm it ([Case Study §5](docs/01-case-study.md#5-solution-options-and-key-decisions), [SRS Appendix A](docs/03-srs.md#appendix-a-decision-log)).

| Decision | What I chose | Why |
|---|---|---|
| Build or buy | Fit-gap one or two existing expense products first; build only if a Must requirement cannot be met | Faster start with a proven workflow. The SRS stays neutral, so it works for both paths. |
| Claim status vs. import result | Two separate fields: claim status and export status. An unknown import result keeps the claim in *Awaiting Confirmation*. | Exporting a file does not mean accounting has booked it. Without this, Finance could pay a claim that was never booked. |
| Duplicate receipts | Warn, let the employee confirm with "Submit anyway", then Finance decides on each flagged line | A match is not proof of fraud. Two identical taxi fares in one day are normal. |
| Accounting interface | CSV file imported by Finance, with the result recorded per claim | The accounting software's import template and API are unknown. |
| Own claims | Nobody approves, verifies, exports, records the import result for, or pays their own claim. The System Administrator has no Finance permissions. *(BA recommendation)* | Recording "Imported" opens the way to payment. It needs a second person. |

## Requirements

| Item | Count |
|---|---|
| Functional requirements | 16 (14 Must, 2 Should) |
| Non-functional requirements | 8 (6 Must, 2 Should) |
| Business rules | 12 |
| Use cases | 10 |
| User stories | 16, matching FR-01 to FR-16 one to one |
| Acceptance criteria | 74 (Given / When / Then) |
| Open questions | 22 (20 open, 2 settled for the case study by a BA recommendation) |

Each business rule is written once in the SRS and referenced by its ID. Some checks cannot be done in UAT. For example, refusing requests sent outside the screens, or two people exporting the same claim at the same moment, need a technical check. [SRS chapter 8](docs/03-srs.md#8-testing-requirements) lists them instead of claiming full coverage.

## Screens and diagrams

[![Claim form wireframe: blocking issues, flags and route preview](assets/wireframes/claim-form-state-a.png)](assets/wireframes/claim-form-state-a.png)

*Claim form after the first Submit: a missing receipt blocks submission, a duplicate warning and an over-limit flag are shown on the line, and the route is previewed ([SRS §3.3](docs/03-srs.md#33-gui-requirements)).*

[![Finance wireframe: batches awaiting import result](assets/wireframes/export-batches-awaiting-result.png)](assets/wireframes/export-batches-awaiting-result.png)

*Finance screen after generating a file: results are recorded per claim, and the officer's own claim has no result option.*

[![Activity diagram from claim to payment](assets/diagrams/activity-diagram.png)](assets/diagrams/activity-diagram.png)

*Main flow from creating a claim to recording payment. Select an image to open it at full size.*

All diagrams and wireframes are in [`assets/`](assets): system context, use cases, activity, claim states, logical ERD and seven screens.

## Validation approach

- Every user story has acceptance criteria in Given / When / Then form, 74 in total. They are the basis for UAT test cases.
- The SRS describes how the requirements would be verified, by UAT and by technical checks from IT/QA ([SRS §8](docs/03-srs.md#8-testing-requirements)).
- Open questions and the interview plan show which assumptions must be confirmed before the requirements can be baselined.
- No test has been run.

## Tools and techniques

- **Tools:** Word, Excel, draw.io for diagrams, and wireframes drawn as SVG that can be imported into Figma
- **Techniques:** SRS writing (shall statements with IDs and MoSCoW priorities), business rules, use case specifications, As-Is / To-Be flow, gap analysis, build-or-buy options analysis, state and data modelling, user stories with Given / When / Then criteria, elicitation planning and open-question tracking

## Repository structure

```
.
├── README.md                  Project overview (this page)
├── docs/                      Documents in Markdown, readable on GitHub
│   ├── 01-case-study.md
│   ├── 02-elicitation-plan.md
│   ├── 03-srs.md
│   └── 04-product-backlog-and-delivery-plan.md
├── assets/
│   ├── diagrams/              Context, use case, activity, state and ERD
│   └── wireframes/            Seven screens
└── source-files/              Original Word files
```

## How to explore the artifacts

| # | Document | What to look at |
|---|---|---|
| 01 | [Case Study](docs/01-case-study.md) | **Start here.** Problem, gaps, process, decisions, example scenarios and limits in about 9 pages |
| 02 | [Elicitation Plan](docs/02-elicitation-plan.md) | Interview plan, questions, assumptions to confirm and baseline measures. A plan only, with no results |
| 03 | [SRS](docs/03-srs.md) | Requirements, business rules, use cases, wireframes, diagrams, accounting export, data model, decision log and open questions |
| 04 | [Product Backlog & Delivery Plan](docs/04-product-backlog-and-delivery-plan.md) | 16 user stories, 74 acceptance criteria and a proposed delivery plan |

The same content is in the original Word files in [`source-files/`](source-files).

## Limitations and conclusion

- The problem, the current process and all rules are assumptions based on common practice. MeraTrade has not confirmed them.
- No interviews were held. The Elicitation Plan only shows how the assumptions would be checked, and its participants would act as proxies for MeraTrade roles.
- The CSV column mapping has not been compared with a real import template, and the case where accounting accepts only part of a claim is not resolved.
- There is no baseline and no target for the success measures, so no improvement is claimed. Acceptance criteria check requirements; they do not prove that the measures will improve.
- Who may record import results, and one system role per employee, are BA recommendations that still need to be confirmed by the CFO, Finance and IT.

The case study shows how I turned an unclear business need into traceable requirements: separating what is known from what is assumed, showing the trade-off behind each decision, and marking which checks need more than UAT.
