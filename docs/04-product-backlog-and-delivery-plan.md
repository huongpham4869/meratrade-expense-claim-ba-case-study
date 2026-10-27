# Product Backlog & Delivery Plan

*MeraTrade Distribution – Expense Claim & Approval System*

> [!NOTE]
> MeraTrade Distribution is a fictional company and all people and data are invented. Version 4, 27 Oct 2026. This document is complete for portfolio purposes but has **not** been approved as a business baseline. Values in [square brackets] are examples or assumptions, not company policy.

# 1. Introduction

This document holds the product backlog: the user stories with their acceptance criteria, and a proposed delivery plan. Requirement IDs (FR) refer to the SRS; stories US-01 to US-16 match FR-01 to FR-16 one to one. The Validation Workbook traces each story to its test cases. Priorities use MoSCoW to show what the MVP needs, not the build order. Acceptance criteria that depend on an open question in the SRS stay provisional until it is answered. Criteria based on a BA recommendation (SRS Appendix A) say so.

# 2. Product Backlog

*Table 1. Product backlog*

| **ID**    | **User story**                         | **Epic**                     | **Priority** | **SRS** |
|-----------|----------------------------------------|------------------------------|--------------|---------|
| **US-01** | Create a claim with lines and receipts | Submit claims                | Must         | FR-01   |
| **US-02** | Check my claim on submit               | Submit claims                | Must         | FR-02   |
| **US-03** | Duplicate warning                      | Submit claims                | Must         | FR-03   |
| **US-04** | Withdraw or cancel                     | Submit claims                | Should       | FR-04   |
| **US-05** | Correct and resubmit                   | Submit claims                | Must         | FR-05   |
| **US-06** | Automatic approval routing             | Approve claims               | Must         | FR-06   |
| **US-07** | Approve, return or reject              | Approve claims               | Must         | FR-07   |
| **US-08** | Finance review                         | Finance review               | Must         | FR-08   |
| **US-09** | Generate export file                   | Export and payment           | Must         | FR-09   |
| **US-10** | Record import result                   | Export and payment           | Must         | FR-10   |
| **US-11** | Record payment                         | Export and payment           | Must         | FR-11   |
| **US-12** | Claim status and history               | Tracking                     | Must         | FR-12   |
| **US-13** | E-mail notifications                   | Tracking                     | Must         | FR-13   |
| **US-14** | Spending report                        | Administration and reporting | Should       | FR-14   |
| **US-15** | Categories and settings                | Administration and reporting | Must         | FR-15   |
| **US-16** | Employees and departments              | Administration and reporting | Must         | FR-16   |

# 3. User Stories and Acceptance Criteria

## 3.1 US-01: Create a claim with lines and receipts

As an employee, I want to create a claim with several expense lines and receipts, so that I can request reimbursement in one place.

*Table 2. US-01 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                      |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given I am signed in, when I create a claim with two lines, then it is saved as Draft and the total is the sum of the lines. The purpose field can be filled in; whether it is required is open (SRS OQ-21). |
| 2      | Given a Draft claim, when I attach a PDF, JPG or PNG file of up to \[10 MB\] to a line, then the file is shown on that line; a file of another type or a larger file is refused with a message.              |
| 3      | Given my claim is Pending Approval, when I open it, then I cannot edit its lines or attachments.                                                                                                             |
| 4      | Given my claim is Draft or Returned, when I open it, then I can edit the claim, add, edit or remove lines and attach files.                                                                                  |

## 3.2 US-02: Check my claim on submit

As an employee, I want the system to check my claim when I submit it, so that I can fix problems before my manager sees it.

*Table 3. US-02 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                                                                |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given a line above its category's receipt threshold has no file, when I submit, then submission is blocked and the line shows "Receipt required".                                                                                                      |
| 2      | Given my claim has no line, or a line has no category, date, amount or description, when I submit, then submission is blocked and every missing item is shown at the same time.                                                                        |
| 3      | Given a line has an amount that is zero, negative or not a whole number, a future date, or a description longer than \[200\] characters, when I submit, then submission is blocked with a message on that field.                                       |
| 4      | Given a line is above its category limit, or its expense date is more than \[30\] days before its first-submitted date, when I submit, then the line is flagged "Over limit" or "Late" and I must enter a justification before the claim is submitted. |
| 5      | Given a line uses a category that has been deactivated, when I submit, then submission is blocked until I choose an active category.                                                                                                                   |
| 6      | Given a line is at or below its category's receipt threshold and has no file, when I submit, then no receipt is asked for on that line.                                                                                                                |

## 3.3 US-03: Duplicate warning

As an employee, I want to be warned when an expense looks like one already claimed, so that I do not claim it twice by mistake.

*Table 4. US-03 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                                                         |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given a line has the same seller tax code, invoice symbol and invoice number as another line that is not in a Rejected or Cancelled claim, when I submit, then I see a "Potential duplicate" warning that does not show the other claim.        |
| 2      | Given I already have a line with the same date, category and amount in a claim that is not Rejected or Cancelled, when I submit, then the new line is flagged "Potential duplicate".                                                            |
| 3      | Given the only matching line is in a Rejected or Cancelled claim, when I submit, then no warning is shown.                                                                                                                                      |
| 4      | Given a line is missing one of the three invoice details, when I submit, then only the date, category and amount check is applied to it.                                                                                                        |
| 5      | Given the only issue left is a duplicate warning, when I choose "Go back and edit", then nothing is submitted; when I choose "Submit anyway", then the claim is Pending Approval, the flag stays on the line and the history records my choice. |

## 3.4 US-04: Withdraw or cancel

As an employee, I want to withdraw or cancel a claim, so that I can stop a claim I no longer need.

*Table 5. US-04 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                            |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given my claim is Pending Approval, when I withdraw it, then it becomes Draft, earlier approvals no longer count, and an approver who opened it before can no longer approve, return or reject it. |
| 2      | Given my claim is Draft or Returned, when I cancel it, then it becomes Cancelled and cannot be edited or submitted.                                                                                |
| 3      | Given my claim is in Finance Review or a later status, when I open it, then Withdraw and Cancel are not available.                                                                                 |

## 3.5 US-05: Correct and resubmit

As an employee, I want to correct and resubmit a returned claim, so that I do not have to start again.

*Table 6. US-05 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                                                                            |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given my claim is Returned, when I open it, then I see the comment and can edit the lines.                                                                                                                                                                         |
| 2      | Given my claim was returned at Level 2, when I resubmit it and the checks pass, then it is Pending Approval at Level 1 with my line manager as approver.                                                                                                           |
| 3      | Given I raised the total from below to above the threshold, when I resubmit, then the route becomes "Level 1 + Level 2".                                                                                                                                           |
| 4      | Given a line was first submitted within \[30\] days of its expense date, when I resubmit after that, then it is not flagged "Late"; a new line uses the resubmission date, and a changed expense date is checked against the line's original first-submitted date. |
| 5      | Given Finance recorded duplicate decisions and then returned my claim, when I resubmit, then the duplicate check runs again, the earlier decisions no longer apply and the history still shows them.                                                               |

## 3.6 US-06: Automatic approval routing

As an employee, I want my claim to go to the right approver automatically, so that I do not have to chase people by e-mail.

*Table 7. US-06 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                         |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given my claim total is at or below \[5,000,000 VND\], when I submit, then the route is "Level 1 only" and my line manager is the approver.                                     |
| 2      | Given my claim total is above \[5,000,000 VND\], when I submit, then the route is "Level 1 + Level 2" and my line manager approves first.                                       |
| 3      | Given I have no line manager, or my line manager is inactive, when I submit, then submission is blocked and I am told to contact the System Administrator.                      |
| 4      | Given I am the Finance Manager and my claim is above the threshold, when I submit, then Level 2 goes to my line manager, and one approval by that person completes both levels. |

## 3.7 US-07: Approve, return or reject

As a line manager or Finance Manager, I want to see the claims waiting for me and decide on them, so that decisions are quick and recorded.

*Table 8. US-07 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                                                |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given a claim is waiting for me, when I open my approval list, then I see its lines, receipts, flags, justifications and, for a potential duplicate, the matched claim and line.                                                       |
| 2      | Given the route is "Level 1 only", when I approve at Level 1, then the claim moves to Finance Review; given the route is "Level 1 + Level 2", it stays Pending Approval, and the Finance Manager becomes the approver and is e-mailed. |
| 3      | Given a claim is waiting at Level 2 and I am the Finance Manager, when I approve it, then it moves to Finance Review.                                                                                                                  |
| 4      | Given a claim is waiting for me, when I return or reject it without a comment, then the action is not accepted; with a comment, the status becomes Returned or Rejected and the claimant is e-mailed the comment.                      |
| 5      | Given a claim is not assigned to me, when I try to approve it, then the action is refused.                                                                                                                                             |

## 3.8 US-08: Finance review

As a Finance Officer, I want to check claims, decide on potential duplicates and verify, return or reject them, so that only valid expenses are paid.

*Table 9. US-08 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                                                                 |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given claims are in Finance Review, when I open the Finance list, then I see each claim with its claimant, total and flags.                                                                                                                             |
| 2      | Given a line is flagged as a potential duplicate, when I try to verify without a decision on it, then verification is blocked.                                                                                                                          |
| 3      | Given I record "Not a duplicate" on every flagged line, when I verify, then the claim is Finance Verified with export status Not Exported.                                                                                                              |
| 4      | Given I record "Duplicate" on a line, when I choose the next action, then Verify is not available and I can only return or reject the claim with a comment.                                                                                             |
| 5      | Given a Finance Verified claim is Awaiting Confirmation or Exported, then Return is not available; given it is Not Exported or Export Failed, when I return it with a comment, then it becomes Returned and its export status is reset to Not Exported. |
| 6      | Given a claim is my own, when I open it, then I cannot record duplicate decisions on it or verify, return or reject it; another Finance Officer can.                                                                                                    |

## 3.9 US-09: Generate export file

As a Finance Officer, I want to export verified claims to a file, so that I do not have to re-type them in the accounting software.

*Table 10. US-09 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given I open the export screen, then only Finance Verified claims with export status Not Exported or Export Failed are listed, and my own claims are not.                                                                                           |
| 2      | Given I select three eligible claims, when I generate the file, then one CSV file has one row per expense line (SRS §6.2) and the three claims are Awaiting Confirmation with the batch ID.                                                         |
| 3      | Given one selected claim has a category with no GL account code and another a department with no cost center code, when I generate the file, then both are left out with their reasons and stay Not Exported, and the other claims are in the file. |
| 4      | Given another Finance Officer exported one of my selected claims after I opened the screen, when I generate my file, then that claim is left out as "No longer eligible"; if no selected claim is still eligible, no batch is created.              |
| 5      | Given the file cannot be generated, when I select Generate, then an error is shown, no batch is created and no export status changes.                                                                                                               |
| 6      | Given the claimant of a verified claim has been deactivated, when I generate the file, then the claim is included like any other.                                                                                                                   |

## 3.10 US-10: Record import result

As a Finance Officer, I want to record the import result of each exported claim, so that I know which claims are booked and which need fixing.

*Table 11. US-10 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                                                      |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given a batch has claims Awaiting Confirmation, when I open the batch list, then the batch is shown as needing a result.                                                                                                                     |
| 2      | Given a claim is Awaiting Confirmation, when I record "Imported", then its export status becomes Exported.                                                                                                                                   |
| 3      | Given a claim is Awaiting Confirmation, when I record "Rejected by accounting" or "Not imported", then a reason is required, the export status becomes Export Failed and the claim can be exported again in a new batch.                     |
| 4      | Given I do not know the result yet, when I leave it empty, then the claim stays Awaiting Confirmation and cannot be exported again, returned or paid.                                                                                        |
| 5      | Given my download failed, when I download the batch file again, then I get the same file and batch ID, with no new batch and no status change.                                                                                               |
| 6      | Given a claim I submitted is in a batch that another Finance Officer exported, when I open the batch, then that claim has no result options and I cannot record its result; another Finance Officer can (BA recommendation, SRS Appendix A). |
| 7      | Given I record a result, then the claim history shows the batch ID, the result, the reason if any, my name and the date and time.                                                                                                            |
| 8      | Given a user whose system role is not Finance Officer, including the System Administrator, when they open the batch list or a batch link, then access is refused and they cannot record any import result.                                   |

## 3.11 US-11: Record payment

As a Finance Officer, I want to record payment only for exported claims, so that the claim status matches what was really paid.

*Table 12. US-11 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                            |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given a Finance Verified claim with export status Exported, when I enter the payment date and reference, then the claim becomes Paid and the claimant is e-mailed. |
| 2      | Given the export status is Not Exported, Awaiting Confirmation or Export Failed, when I open the claim, then Record payment is not available.                      |
| 3      | Given the payment date or the reference is empty, when I confirm, then the payment is not saved.                                                                   |
| 4      | Given the claim is my own, then Record payment is not available to me; another Finance Officer can record it.                                                      |
| 5      | Given the claim is already Paid, when I record payment again from a page opened earlier, then the action is refused and no second payment is recorded.             |

## 3.12 US-12: Claim status and history

As an employee, I want to see my claim's status, approver and history, so that I do not have to ask Finance.

*Table 13. US-12 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given I have claims in different statuses, when I open My Claims, then I see each claim's status, total, current approver and, for Finance Verified claims, the export status.                      |
| 2      | Given a claim was returned and resubmitted, when I open its history, then I see each action with user, date, time and comment.                                                                      |
| 3      | Given any user views a claim's history, then the entries cannot be edited or deleted.                                                                                                               |
| 4      | Given I am not the claimant, an approver of the claim, a Finance Officer or the Finance Manager, when I open the claim by its link, then access is refused; this includes the System Administrator. |
| 5      | Given a claim is Paid, when I open it, then I see export status Exported and the batch ID.                                                                                                          |

## 3.13 US-13: E-mail notifications

As a claimant or approver, I want an e-mail when a claim needs my action or changes, so that nothing waits unnoticed. *(Must · FR-13)*

*Table 14. US-13 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                  |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given a claim is assigned to me as approver, then I receive an e-mail with the claim ID and a link.                                                      |
| 2      | Given my claim is returned, rejected or paid, then I receive an e-mail with the comment or the payment date.                                             |
| 3      | Given the e-mail service fails after an approval, then the approval stays saved, the claim waits for the next approver and the failure is logged for IT. |

## 3.14 US-14: Spending report

As a Finance Manager, I want a simple spending report, so that I can follow spending without building Excel files by hand.

*Table 15. US-14 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                                                                |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given claims exist in several departments, when I filter by expense month and department, then I see line totals by category for Finance Review, Finance Verified and Paid claims, and I can add Pending Approval and Returned claims. |
| 2      | Given a claim has lines in two months, then each line is counted in the month of its expense date; Draft, Rejected and Cancelled claims are never counted.                                                                             |
| 3      | Given a report is on screen, when I select Download, then I get a CSV file with the same figures.                                                                                                                                      |

## 3.15 US-15: Categories and settings

As a System Administrator, I want to maintain categories, limits, the deadline and the approval threshold, so that policy changes need no development work.

*Table 16. US-15 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                 |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given I create a category with a GL account code, receipt threshold and limit, then employees can choose it on new lines.                               |
| 2      | Given I change the Level 2 threshold, then claims submitted or resubmitted afterwards use the new value, and claims already submitted keep their route. |
| 3      | Given I deactivate a category, then it cannot be chosen on new lines, and lines of claims already submitted keep it.                                    |

## 3.16 US-16: Employees and departments

As a System Administrator, I want to maintain employees, departments and line managers, so that claims go to the right approver.

*Table 17. US-16 acceptance criteria*

| **AC** | **Given / When / Then**                                                                                                                                                                      |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | Given I set employee B's line manager to employee A, when B submits a claim, then A is the Level 1 approver; claims B submitted before the change keep their approver.                       |
| 2      | Given I deactivate an employee, then they cannot sign in or be assigned as an approver, and their claims already submitted do not change.                                                    |
| 3      | Given I edit an employee, when I set the system role, then the employee has exactly one system role, and the System Administrator role adds no access to claims, batches or Finance actions. |

# 4. Delivery Plan

*Table 18. Proposed delivery stages*

| **Stage**                   | **Main BA work**                                                                                                                                                                                                                                   | **Output**                                      |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| **1. Confirm requirements** | Run the interviews in the Elicitation Plan. Get the real accounting import template. Confirm the BA recommendations and the open questions marked “Baseline” in SRS Appendix B. Fit-gap one or two expense products against the Must requirements. | Updated SRS; build-or-buy decision              |
| **2. Design**               | Product: configuration and the import file. Custom build: screens and data design with the team.                                                                                                                                                   | Agreed configuration or design; refined backlog |
| **3. Build**                | Clarify stories for the team. Check the CSV file with Finance using test data.                                                                                                                                                                     | Working increments, Must stories first          |
| **4. Test and UAT**         | Run UAT with claimants, approvers and Finance. Agree the technical checks with IT/QA (SRS chapter 8). Track defects and change requests.                                                                                                           | UAT sign-off                                    |
| **5. Release and support**  | Go-live checklist. Support during the first weeks. Collect feedback for Should stories and future scope.                                                                                                                                           | System in use; list of follow-up changes        |
