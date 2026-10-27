# MeraTrade – Expense Claim & Approval System: BA Case Study

**Business Analyst · Independent Portfolio Project** · Version 4 · 27 Oct 2026

> [!NOTE]
> This is a simulated case study. MeraTrade Distribution, its people and its data are fictional. I have not interviewed any stakeholder, built the system or run any test. The document set is complete for portfolio purposes but has not been approved as a business baseline. Where a decision was needed to finish the case study, it is marked as a BA recommendation.
>
> Values in [square brackets] are examples, not company policy.

---

## 1. Project overview

MeraTrade Distribution is a fictional company that distributes consumer goods to dealers and supermarkets in Vietnam. It has about 400 employees in Da Nang (head office), Ha Noi and Ho Chi Minh City. Sales staff travel a lot, so they have many expenses such as taxis, hotels, meals and client entertainment.

The project proposes an internal system where employees submit a **claim** (a request to be reimbursed for expenses). A claim goes through approval, Finance review, an export file for the accounting software, and finally payment recording.

**Main users**

- **Employee:** submits the claim.
- **Line Manager:** approves at Level 1.
- **Finance Manager:** approves at Level 2 when a claim is above the threshold.
- **Finance Officer:** reviews claims, exports files, records import results and records payments, but never for their own claim.
- **System Administrator:** maintains categories and employee data; has no Finance permissions.

Each employee has one system role. Line Manager is not a system role: it comes from the reporting line.

**My role (BA)**

- Analysed the problem and defined the objectives and the scope of the **MVP** (minimum viable product).
- Wrote the SRS: requirements, business rules, wireframes, diagrams and data.
- Wrote a backlog of 16 user stories with acceptance criteria.
- Designed traceability and test cases for UAT.
- Planned the interviews that would check the assumptions.

Tools: Word, Excel, draw.io (diagrams) and wireframes drawn as SVG that can be imported into Figma.

---

## 2. Problem and objectives

**Problem (assumed).** The current process relies on Excel, e-mail and manual entry by Finance. As a result, employees do not know where their claim is, and policies are applied unevenly. A receipt can be claimed twice without anyone noticing, and Finance spends a lot of time on manual work. MeraTrade has not confirmed these problems.

**Objectives**

1. Employees can see where their claim is.
2. The expense policy is applied consistently.
3. The risk of paying the same expense twice is lower.
4. Finance does less manual work.
5. The monthly expense report is faster to prepare.

How each objective would be measured is in section 8.

---

## 3. Current process and pain points

Both the process and the pain points below are inferred from common practice. MeraTrade has not confirmed them.

| Current step (assumed) | Pain point |
|---|---|
| 1. The employee prepares the claim in an Excel file. | Rules on receipts, limits and deadlines are not checked while the claim is prepared, so many claims are returned. |
| 2. The employee e-mails the claim with receipt photos for the manager to approve. | E-mails get lost, and it is hard to see who approved and when. Employees have to ask where their claim is. |
| 3. The employee hands paper receipts to Finance. | The same receipt can be claimed twice without anyone noticing. |
| 4. Finance checks the claim and types each item into the accounting software. | Slow, and errors are easy when data is typed again. |
| 5. Finance pays outside the system and prepares the monthly report by hand. | The report is manual and takes a lot of time. |

---

## 4. Gaps and proposed process

### Gap analysis

The table links each pain point to the capability the MVP needs. The last column gives the matching requirement in the SRS.

| Pain point | Gap | MVP capability | SRS |
|---|---|---|---|
| Nobody knows where a claim is | No shared place to track claims | Claim status and history; e-mail when action is needed | FR-12, FR-13 |
| Approval e-mails get lost and are hard to trace | No clear approval route and no approval history | Approver chosen automatically by threshold; approve, return or reject in the system | FR-06, FR-07 |
| Policy is applied unevenly | Checks are done by eye, and each person does it differently | Checks on submit, based on one shared set of settings | FR-02, FR-15 |
| A receipt can be paid twice | No step that compares receipts | Duplicate warning; Finance decides on each line | FR-03, FR-08 |
| Finance types data and builds reports by hand | No structured data to move to accounting | CSV export by batch, import-result recording, spending report | FR-09, FR-10, FR-14 |

### Proposed process (To-Be)

![Figure 1. Main flow from creating a claim to recording payment](../assets/diagrams/activity-diagram.png)

*Figure 1. The main flow (SRS Figure 10). Grey italic text is the claim status or export status after that step. R is the point where the claim goes back to step 1.*

Four points to notice in the diagram:

- Every "return" branch (R) goes back to step 1. The employee fixes the claim and resubmits, and approval restarts at Level 1.
- When a claim needs Level 2, the system assigns the Level 2 approver after Level 1 approves and sends an e-mail (step 6).
- The system is not connected to the accounting software. Finance checks the import result and records it; the person recording cannot be the claimant.
- When the import result is not known, Finance records nothing. The claim waits in the status Awaiting Confirmation.

![Figure 2. Claim status lifecycle](../assets/diagrams/claim-state-diagram.png)

*Figure 2. The eight claim statuses (SRS Figure 11).*

| Status | Meaning |
|---|---|
| Draft | Being prepared by the employee. |
| Pending Approval | Waiting for the Level 1 or Level 2 approver. |
| Returned | Sent back for correction. |
| Finance Review | Fully approved, waiting for Finance to review. |
| Finance Verified | Confirmed by Finance, ready for export and payment. |
| Paid | Payment recorded. Final status. |
| Rejected | Rejected. Final status. |
| Cancelled | Cancelled by the employee. Final status. |

---

## 5. Solution options and key decisions

### 5.1 Choosing an approach

I did not assume that a new system must be built. There are three ways to go:

| Option | Strengths | Weaknesses |
|---|---|---|
| Improve Excel and e-mail (standard template, shared folder) | Cheap, can start immediately | Still no status tracking, no duplicate detection, and Finance still types the data |
| Configure an existing expense product | Fast to roll out; common workflow already built | The company must follow the product's way of working; cost, data location and IT approval must be checked |
| Build a custom web app | Fits the company's process | Most time and cost |

**Recommended direction:** run a fit-gap of one or two existing products against the Must requirements first. Build a custom system only if a Must requirement cannot be met.

The SRS is written to be neutral, so it works for both paths. This direction must be reviewed if the accounting software's import template or IT rules out the product option.

I have no cost data, so the comparison is qualitative only.

### 5.2 Four design decisions

**a) Separate the claim status from the accounting import result**

- **Problem:** Booking and payment happen outside the system. If "file exported" is treated as "booked in accounting", Finance could pay a claim that the accounting software has not accepted.
- **Choice:** Two fields: the claim status and the **export status**. When the import result is unknown, the claim is Awaiting Confirmation. It cannot then be exported again, returned or paid.
- **Trade-off:** One more status to explain and test.
- **To confirm:** How the accounting software reports results, and whether it can accept only part of a claim.

**b) Warn about duplicates and let a person decide**

- **Problem:** A match is not necessarily fraud. For example, two taxi rides with the same fare on one day are normal.
- **Choice:** The system matches by invoice number, or by claimant, date, category and amount. On a warning, the employee can go back and edit or choose "Submit anyway".
  - The employee only sees that a match exists, not the other person's claim.
  - Finance decides on each flagged line before verifying the claim.
- **Trade-off:** One more step for the employee, and the system will sometimes warn by mistake.
- **To confirm:** Which details are enough to recognise the same invoice.

**c) Use a CSV file because the import template is unknown**

- **Problem:** I do not know which file template the accounting software needs, or whether it has an API.
- **Choice:** Each batch produces one CSV file, with one row per expense line. The column mapping is clearly marked as an assumption. Finance records the import result for each claim.
- **Trade-off:** Finance still has one manual step: importing the file.
- **To confirm:** The file template, the columns and the formats.

**d) Nobody confirms the import result for their own claim (BA recommendation)**

- **Problem:** Recording "Imported" opens the way to payment. The earlier rule only stopped people approving, verifying, exporting and paying their own claim. A Finance Officer could still record the import result for their own claim if a colleague had exported the file.
- **Choice:** Only a Finance Officer can record import results, and never for a claim they submitted. The System Administrator has no Finance permissions. Each employee has one system role; if a person ever has several roles, the system refuses an action when permissions conflict.
- **Trade-off:** There must always be at least two Finance Officers, and IT cannot help record results.
- **To confirm:** This is my recommendation to complete the case study. It has not been confirmed by the CFO, Finance or IT (OQ-19, OQ-22).

---

## 6. Requirements and how they are checked

The document set contains:

- **SRS:** 16 functional requirements, 12 business rules and 8 non-functional requirements.
- **Backlog:** 16 user stories with 74 acceptance criteria. Each user story maps to exactly one functional requirement.
- **Validation Workbook:** 22 UAT test cases. Every acceptance criterion is covered by a test case, but no test case has been run.

### 6.1 Example scenarios

| # | Scenario | System response | Test case |
|---|---|---|---|
| 1 | Submit a claim with a total exactly equal to the threshold [5,000,000 VND], then a claim above it. | The first needs Level 1 approval only. The second needs Level 1 and Level 2. | TC-02 |
| 2 | A claim has one line missing a required receipt and another missing category, date and amount. | Submission is blocked and all errors are shown at once, on the lines that have them. | TC-03 |
| 3 | An employee has no Line Manager, or the Line Manager's account is deactivated. | Submission is blocked with a message to contact the System Administrator. | TC-10 |
| 4 | A Finance Officer submits a claim above the threshold, and their Line Manager is also the Finance Manager. | One approval completes both levels, and the history records both. | TC-11 |
| 5 | A claim is returned; the employee changes one line's expense date, adds a new line and resubmits. | The old line's lateness is measured from its own first-submitted date. The new line is measured from the resubmission date. | TC-06 |
| 6 | An employee enters an invoice that duplicates one in another employee's paid claim. | The claimant only sees a warning. The approver sees the matching claim. If Finance chooses "Duplicate", the claim cannot be verified. | TC-08 |
| 7 | Finance has exported a file but does not know whether the accounting software accepted it. | The claim is Awaiting Confirmation: it cannot be exported again, returned or paid. | TC-13 |
| 8 | Two Finance Officers open the export screen. The second, on an outdated screen, exports a claim the first one has just exported. | The claim is only in the first batch. The second officer sees the reason "No longer eligible". | TC-15 |
| 9 | A Finance Officer opens a batch that contains their own claim, exported by a colleague. Then the System Administrator opens the batch list. | There is no result option for the officer's own claim; the colleague records it, and the history records batch, reason, person and time. The System Administrator is refused. | TC-22 |

### 6.2 Traceability for the highest-risk flows

This table traces six high-risk flows only. It does not replace the full RTM in the [Validation Workbook](05-validation-workbook.md).

| Risk | Rule | Expected outcome | Test case |
|---|---|---|---|
| No approver, or one person assigned at both levels | BR-04, BR-05 | A claim without an approver cannot be submitted. One person at both levels does not approve twice, but the history records both levels. | TC-10, TC-11 (waiting for OQ-01) |
| A claim is returned and resubmitted | BR-03, BR-08 | Approval restarts at Level 1. No line is counted late just because of approval waiting time. | TC-06, TC-07 |
| A duplicate warning is wrong | BR-10 | A genuine repeated expense can still be verified after Finance chooses "Not a duplicate". | TC-08, TC-09 |
| The import result is unknown | BR-11, FR-10 | No re-export, return or payment until Finance records the result. | TC-13, TC-14 |
| A claim is exported twice | BR-11 | A claim cannot be in two batches that are awaiting results. | TC-15. This test runs one step at a time; simultaneous actions need an extra technical check. |
| Confirming the import result for one's own claim | BR-05, FR-10 | A claimant cannot record the import result, even if someone else exported the file. The System Administrator has no Finance permissions. | TC-22, TC-17. Requests sent outside the screens need an extra technical check. |

---

## 7. Scope, assumptions and limitations

### Scope

- **In the MVP:**
  - Submitting claims, with checks on submit.
  - One- or two-level approval based on a threshold.
  - Duplicate warnings.
  - Finance review, CSV export and recording the import result.
  - Payment recording.
  - Claim status tracking, e-mail notifications and a basic spending report.
- **Out of scope:** money transfers, tax calculation, cash advances, corporate cards, foreign currencies, OCR, API integration and a mobile app.
- **Later:**
  - Cover approvers for absences.
  - Reminders.
  - Re-routing when a line manager changes.
  - Handling claims of employees who leave.
  - Correcting a claim after it has been booked in accounting.

### Main assumptions

- The accounting software can import CSV files and accepts or rejects a whole claim at once.
- Finance pays outside the system, and only after the claim has been booked.
- The System Administrator enters employee and Line Manager data from HR data.
- The first release only needs to work in a desktop browser.
- Each employee has one system role; only a Finance Officer records import results, never for their own claim; the System Administrator has no Finance permissions (BA recommendation).

### Limitations

- I have not interviewed anyone. The [Elicitation Plan](02-elicitation-plan.md) is only a plan.
- The CSV column mapping is an assumption and has not been checked against a real import template.
- The case where the accounting software accepts only part of a claim is not resolved.
- CR-01 in the Validation Workbook is a simulated change request and has not been approved.

### Most important open questions

| Question | Why it matters | Who to ask |
|---|---|---|
| Who approves the claims of the Finance Manager and senior managers? When one person holds both levels, is one approval enough? (OQ-01) | It decides the approval route and the independence of Level 2. The General Director has no Line Manager in the data. | Managers, Finance |
| Which file template does the accounting software need, how does it report results, and can it accept part of a claim? (OQ-02) | It decides the field mapping and how import results are recorded. | Finance, IT |
| Does Finance pay before or after booking in accounting? (OQ-03) | The rule "record payment only when Exported" depends on it. | Finance |
| Who updates Line Manager data, and what happens to the claims of people who leave? Withdraw is Should: should it become Must? (OQ-08) | It affects the approval route and the priority of one user story. | Finance, HR |
| Do sales staff need to submit claims from a phone? (OQ-12) | The MVP only supports a desktop browser. | Employees, managers |
| May one person take two steps on someone else's claim, for example approve and then verify? May a System Administrator be an approver? (OQ-19) | The BA recommendation stops people confirming their own claims but not one person controlling two steps on another person's claim. | CFO, Finance, IT |

All 22 questions are in [SRS Appendix B](03-srs.md#appendix-b-open-questions). 20 are Open; OQ-19 is partly settled and OQ-22 is settled for the case study by a BA recommendation. Both still need confirmation in a real project.

---

## 8. Expected outcomes and how to measure them

| Expected outcome | Proposed measure (to be measured) |
|---|---|
| Employees can see where their claim is | Status enquiries per month; days from first submission to payment |
| The policy is applied consistently | Share of claims returned at least once |
| Duplicate receipts are found early | Duplicates found before payment compared with after payment |
| Finance does less manual work | Finance time to review and book one claim |
| The monthly report is faster | Time to prepare the monthly expense report |

The table only lists expected outcomes and proposed measures:

- **There is no baseline and no target yet.** A target should only be set after the current state is measured. The Elicitation Plan describes how to measure it.
- **There are no measured results.** Real results can only be measured after the system is in use.
- **Test cases do not prove that the measures will improve.** They only check that the system does what the requirements say.

---

## Detailed documents

| Document | Content |
|---|---|
| [02 Elicitation Plan](02-elicitation-plan.md) | Interview plan, questions, assumptions to confirm and baseline measures. |
| [03 SRS](03-srs.md) | The full specification: process, requirements, business rules, wireframes, accounting export, data, decisions and open questions. |
| [04 Product Backlog & Delivery Plan](04-product-backlog-and-delivery-plan.md) | 16 user stories, acceptance criteria and a proposed delivery plan. |
| [05 Validation Workbook](05-validation-workbook.md) | RTM, test cases, test data and the impact analysis of CR-01. |
