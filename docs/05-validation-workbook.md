# Validation Workbook – Traceability and Test Cases

*MeraTrade Distribution – Expense Claim & Approval System*

> [!NOTE]
> This page is the Markdown view of the Excel workbook `MeraTrade_Validation_Workbook.xlsx` (Version 4, 27 Oct 2026). **No test has been run:** every test case has the status "Not executed". MeraTrade is a fictional company and all names and values are test data.

## 1. How to read it

| Topic | Explanation |
|---|---|
| Status | No test has been run. Every test case is "Not executed" |
| How to read it | Requirement (SRS) → business rules → user story (Product Backlog) → test cases. Stories US-01 to US-16 match FR-01 to FR-16. A test case names the acceptance criteria it checks, for example "US-02 · AC 1". |
| RTM | One row per requirement with its business rules, the open questions that could change it, its user story, test cases and the kind of check designed (see Coverage below). Rules and open questions are read from the SRS. |
| Test Cases | Business-level test cases for UAT, with preconditions, steps and expected results. |
| Test Data | Fictional employees, departments and the example settings used by the test cases. |
| CR-01 | A simulated change request and its impact on the documents. Not approved and not applied. |
| Coverage | UAT: the test cases check the requirement. UAT + technical check: UAT checks what users see, and a technical check by IT/QA is also needed. Technical check: checked by IT/QA outside UAT. Blocked by open question: cannot be tested until the question is answered. |
| BA recommendation | Who may record import results follows a BA recommendation in SRS Appendix A: only a Finance Officer, never for their own claim, and the System Administrator role gives no Finance permissions. It is not a stakeholder decision. TC-17 and TC-22 check it; they must be reviewed if SRS OQ-19 or OQ-22 is answered differently. |
| Source text | Requirement and rule text is in the SRS; acceptance criteria text is in the Product Backlog. This workbook uses their IDs. |

## 2. Requirements Traceability Matrix (RTM)

One row per requirement. "Coverage" shows which kind of check is designed, not whether it has passed.

| Measure | Count |
|---|---|
| Requirements | 24 (16 functional, 8 non-functional) |
| Coverage: UAT | 15 |
| Coverage: UAT + technical check | 6 |
| Coverage: technical check | 2 |
| Coverage: blocked by open question | 1 |
| Test cases designed | 22 |
| Test cases executed | 0 |

| Req ID | Type | Requirement | Priority | Objective | Business rules | Open questions | User story | Test cases | Coverage | Note |
|---|---|---|---|---|---|---|---|---|---|---|
| FR-01 | Functional | Create and edit a claim | Must | Status visibility | BR-01, BR-02, BR-07 | OQ-05, OQ-14, OQ-21 | US-01 | TC-01, TC-04 | UAT |  |
| FR-02 | Functional | Check the claim on submit | Must | Consistent policy | BR-01, BR-02, BR-03, BR-09 | OQ-05, OQ-14, OQ-21 | US-02 | TC-01, TC-03, TC-04, TC-05, TC-19 | UAT |  |
| FR-03 | Functional | Warn about potential duplicates | Must | Lower duplicate risk | BR-10 | OQ-04, OQ-13, OQ-20 | US-03 | TC-08, TC-09 | UAT |  |
| FR-04 | Functional | Withdraw or cancel | Should (OQ-08) | Status visibility | BR-07 | OQ-08 | US-04 | TC-18 | UAT |  |
| FR-05 | Functional | Correct and resubmit | Must | Consistent policy | BR-03, BR-08, BR-10 | OQ-05, OQ-07, OQ-13 | US-05 | TC-06, TC-07, TC-08 | UAT |  |
| FR-06 | Functional | Set the approval route | Must | Status visibility; consistent policy | BR-04, BR-05, BR-09 | OQ-01, OQ-06, OQ-14 | US-06 | TC-01, TC-02, TC-10, TC-11 | UAT |  |
| FR-07 | Functional | Approve, return or reject | Must | Status visibility | BR-05, BR-06 | OQ-01, OQ-19, OQ-20 | US-07 | TC-01, TC-02, TC-05, TC-07, TC-08, TC-17 | UAT |  |
| FR-08 | Functional | Finance review | Must | Lower duplicate risk; less Finance effort | BR-05, BR-06, BR-10 | OQ-19, OQ-20 | US-08 | TC-01, TC-08, TC-09, TC-13, TC-14, TC-16, TC-17 | UAT |  |
| FR-09 | Functional | Generate an export batch | Must | Less Finance effort | BR-05, BR-11 | OQ-02, OQ-15 | US-09 | TC-01, TC-12, TC-14, TC-15, TC-21 | UAT + technical check | TC-21 forces a file-generation failure. All-or-nothing saving of batch, file, statuses and history needs a technical test (NFR-04). |
| FR-10 | Functional | Record the import result | Must | Less Finance effort | BR-05, BR-11 | OQ-02, OQ-19, OQ-22 | US-10 | TC-01, TC-13, TC-14, TC-15, TC-17, TC-22 | UAT + technical check | TC-22 and TC-17 check the screens. Refusal of batch and import-result requests sent outside the screens, by the claimant or the System Administrator, needs a technical check (NFR-01). |
| FR-11 | Functional | Record payment | Must | Status visibility | BR-05, BR-12 | OQ-03 | US-11 | TC-01, TC-13, TC-14, TC-16 | UAT |  |
| FR-12 | Functional | Claim status and history | Must | Status visibility | – | OQ-18 | US-12 | TC-07, TC-16, TC-17, TC-18, TC-22 | UAT |  |
| FR-13 | Functional | E-mail notifications | Must | Status visibility | BR-06 | – | US-13 | TC-01, TC-02, TC-07, TC-16, TC-21 | UAT |  |
| FR-14 | Functional | Spending report | Should | Faster reporting | – | OQ-11 | US-14 | TC-20 | UAT |  |
| FR-15 | Functional | Maintain categories and settings | Must | Consistent policy | BR-01, BR-09 | OQ-14 | US-15 | TC-19 | UAT |  |
| FR-16 | Functional | Maintain employees and departments | Must | Status visibility | BR-05, BR-11 | OQ-08, OQ-22 | US-16 | TC-10, TC-17 | UAT |  |
| NFR-01 | Non-functional | Access control by role; requests outside the screens refused | Must | – | – | – | – | TC-12, TC-16, TC-17, TC-22 | UAT + technical check | UAT checks the screens only. Refusal of requests sent outside the screens needs a technical check by IT/QA. |
| NFR-02 | Non-functional | Sign-in with the company account (single sign-on) | Must | – | – | – | – | – | Technical check | Checked by IT when single sign-on is set up. |
| NFR-03 | Non-functional | History cannot be edited or deleted | Must | – | – | – | – | TC-17 | UAT + technical check | UAT checks that the screens offer no edit or delete. Protection of stored history needs a technical check. |
| NFR-04 | Non-functional | Outdated or repeated actions refused; records saved together | Must | – | – | – | – | TC-15, TC-16, TC-18 | UAT + technical check | UAT repeats actions one after another. Simultaneous requests and all-or-nothing saving need a technical test. |
| NFR-05 | Non-functional | Attachments: PDF, JPG or PNG up to [10 MB] | Must | – | – | – | – | TC-04 | UAT |  |
| NFR-06 | Non-functional | Messages next to the field; Chrome and Edge on desktop | Should | – | – | OQ-12 | – | TC-03 | UAT + technical check | Browser checks on current Chrome and Edge by QA. |
| NFR-07 | Non-functional | Lists and details open within [3 seconds] | Should | – | – | OQ-16 | – | – | Technical check | Performance check by IT/QA once the target and measurement are agreed. |
| NFR-08 | Non-functional | Retention as required by the accounting-record policy | Must | – | – | OQ-09 | – | – | Blocked by open question | The retention period is not known (SRS OQ-09). |

## 3. Test cases (UAT)

Business-level test cases with preconditions, steps and expected results. They use the illustrative data in section 4. Status stays "Not executed" until a real test is run.

| TC | Title | Priority | Status |
|---|---|---|---|
| TC-01 | Happy path below the threshold: submit to Paid | High | Not executed |
| TC-02 | Approval route at and above the threshold | High | Not executed |
| TC-03 | Missing receipt and missing data block submission | High | Not executed |
| TC-04 | Invalid values and files are refused | Medium | Not executed |
| TC-05 | Over-limit and late lines need a justification | Medium | Not executed |
| TC-06 | Late check after a return | Medium | Not executed |
| TC-07 | Return, reject and resubmit | High | Not executed |
| TC-08 | Duplicate warning, Finance decision and resubmission | High | Not executed |
| TC-09 | Duplicate check rules | Medium | Not executed |
| TC-10 | Approver taken from line-manager data | High | Not executed |
| TC-11 | Own claim re-routed; one person at both levels (provisional, SRS OQ-01) | High | Not executed |
| TC-12 | Export file content and claims left out | High | Not executed |
| TC-13 | Import result not known yet | High | Not executed |
| TC-14 | Rejected by accounting or not imported | High | Not executed |
| TC-15 | Outdated export screen and download again | High | Not executed |
| TC-16 | Payment rules | High | Not executed |
| TC-17 | Access by role and history protection | High | Not executed |
| TC-18 | Withdraw, cancel and My Claims | Medium | Not executed |
| TC-19 | Settings changes and category deactivation | Medium | Not executed |
| TC-20 | Spending report | Low | Not executed |
| TC-21 | Technical failures leave the data correct | Low | Not executed |
| TC-22 | Import result: own claim, traceability and System Administrator (BA recommendation) | High | Not executed |

### TC-01: Happy path below the threshold: submit to Paid

**Priority:** High · **Status:** Not executed

**Checks:** US-01 · AC 1, 3; US-02 · AC 6; US-06 · AC 1; US-07 · AC 2; US-08 · AC 3; US-09 · AC 2; US-10 · AC 2; US-11 · AC 1; US-13 · AC 1, 2

**Preconditions and data:** E-1001 signed in. Settings as in the test data (section 4).

**Steps**

1. E-1001 creates a claim "Taxi to customer – Hai Chau" with two Taxi lines dated 15/10/2026: 150,000 VND "Taxi to customer" and 120,000 VND "Taxi back to office". No receipts. Submits.
2. E-1001 opens the claim and tries to edit a line.
3. E-0501 approves.
4. E-0301 verifies.
5. E-0301 exports the claim and opens the file.
6. E-0301 records "Imported".
7. E-0301 records payment: 16/10/2026, reference FT2610160001.

**Expected result**

1. Pending Approval, route "Level 1 only", total 270,000 VND; no receipt is asked for, because both lines are below the Taxi receipt threshold. E-0501 gets an e-mail with the claim ID and a link.
2. The lines cannot be edited.
3. Finance Review.
4. Finance Verified; export status Not Exported.
5. Awaiting Confirmation with a batch ID. The file has 2 rows with AccountCode 6418 and CostCenter CC-SDN.
6. Exported.
7. Paid. E-1001 gets an e-mail with the payment date.

### TC-02: Approval route at and above the threshold

**Priority:** High · **Status:** Not executed

**Checks:** US-06 · AC 1, 2; US-07 · AC 2, 3; US-13 · AC 1

**Preconditions and data:** E-1001 signed in. Level 2 threshold 5,000,000 VND. Receipts attached to every line.

**Steps**

1. E-1001 submits claim A: four Hotel lines, 01/10 to 04/10/2026, 1,250,000 VND each (total 5,000,000 VND).
2. E-1001 submits claim B: three Hotel lines, 07/10 to 09/10/2026, 1,400,000 VND each, and one Client entertainment line, 09/10/2026, 2,000,000 VND (total 6,200,000 VND).
3. E-0501 approves claim B.
4. E-0201 approves claim B.

**Expected result**

1. Route "Level 1 only": a total equal to the threshold is not above it. Approver E-0501.
2. Route "Level 1 + Level 2". Approver E-0501.
3. Still Pending Approval; current level 2; approver E-0201, who gets an e-mail.
4. Finance Review.

### TC-03: Missing receipt and missing data block submission

**Priority:** High · **Status:** Not executed

**Checks:** US-02 · AC 1, 2

**Preconditions and data:** E-1001 signed in. Today is 16/10/2026.

**Steps**

1. E-1001 creates a claim with three lines: (1) Meals, 15/10/2026, 350,000 VND, "Dinner with dealer", no receipt; (2) Taxi, 15/10/2026, 80,000 VND, "Taxi to dealer"; (3) only the description "Parking". Submits.
2. E-1001 creates a claim with no lines and submits it.
3. In the first claim, E-1001 deletes line 3, attaches a receipt to line 1 and submits.

**Expected result**

1. Blocked; the claim stays Draft. Line 1 shows "Receipt required"; line 3 shows messages on category, date and amount. All issues appear together, next to their lines.
2. Blocked. A message says that at least one line is needed.
3. Pending Approval; total 430,000 VND.

### TC-04: Invalid values and files are refused

**Priority:** Medium · **Status:** Not executed

**Checks:** US-01 · AC 2, 4; US-02 · AC 2, 3

**Preconditions and data:** E-1001 has a Draft claim with one Meals line: 15/10/2026, 300,000 VND, "Lunch with dealer". Today is 16/10/2026.

**Steps**

1. Attach a JPG of 2 MB and a PDF of exactly 10 MB to the Meals line.
2. Attach a DOCX file of 1 MB, then a PNG of 10.5 MB.
3. Add six lines: Taxi 0 VND; Taxi -50,000 VND; Taxi 45,500.5 VND; Taxi dated 17/10/2026; Office supplies 150,000 VND with no description; Office supplies 150,000 VND with a 201-character description. Submit.

**Expected result**

1. Both files are shown on the line.
2. Both files are refused with a message.
3. Blocked. Messages on the amount (three lines), the date (one line) and the description (two lines), all shown at once.

### TC-05: Over-limit and late lines need a justification

**Priority:** Medium · **Status:** Not executed

**Checks:** US-02 · AC 4; US-07 · AC 1

**Preconditions and data:** E-1001 signed in. Today is 16/10/2026.

**Steps**

1. E-1001 submits a claim: line 1 Hotel, 14/10/2026, 1,700,000 VND, "Hotel Quy Nhon, 1 night", receipt attached; line 2 Taxi, 10/09/2026, 120,000 VND, "Taxi to dealer". No justification.
2. E-1001 enters a justification on both lines and submits.
3. E-0501 opens the approval list and the claim.

**Expected result**

1. Blocked. Line 1 is flagged "Over limit" (limit 1,500,000 VND) and line 2 "Late" (36 days); both ask for a justification.
2. Pending Approval, route "Level 1 only" (total 1,820,000 VND); both flags stay.
3. E-0501 sees the claim, both flags and both justifications.

### TC-06: Late check after a return

**Priority:** Medium · **Status:** Not executed

**Checks:** US-05 · AC 4

**Preconditions and data:** Deadline 30 days. Claim L of E-1001 was first submitted on 05/10/2026 and returned by E-0501 on 14/10/2026 with "Line 2: the date is wrong." Line 1: Taxi, 10/09/2026, 120,000 VND (25 days, not Late). Line 2: Meals, 01/09/2026, 150,000 VND, flagged Late with a justification. Today is 16/10/2026.

**Steps**

1. E-1001 changes line 2's date to 12/09/2026, adds line 3: Taxi, 12/09/2026, 90,000 VND, "Taxi back to office", with no justification, and resubmits.
2. E-1001 enters a justification on line 3 and resubmits.

**Expected result**

1. Blocked. Line 3 is "Late" (34 days to its own first submission on 16/10/2026). Line 2 is no longer Late (23 days to its original first submission on 05/10/2026). Line 1 is not Late (25 days to 05/10/2026, although 36 days have passed since).
2. Pending Approval at Level 1; approver E-0501.

### TC-07: Return, reject and resubmit

**Priority:** High · **Status:** Not executed

**Checks:** US-05 · AC 1, 2, 3; US-07 · AC 4; US-12 · AC 2; US-13 · AC 2

**Preconditions and data:** Claim B of E-1001 is at Level 2 with approver E-0201 (as after TC-02 step 3). Claim R of E-1001 is Pending Approval at Level 1, route "Level 1 only": two Hotel lines, 01/10 and 02/10/2026, 1,300,000 VND each, receipts attached. Claim T of E-1003 is Pending Approval at Level 1: one Meals line, 12/10/2026, 400,000 VND, receipt attached.

**Steps**

1. E-0201 selects Return on claim B without a comment, then returns it with "Line 4: please add the client name and number of guests."
2. E-1001 opens claim B, adds the details to line 4 and resubmits.
3. E-0501 returns claim R with "Please add the hotel nights of 03/10 and 04/10." E-1001 adds two Hotel lines (03/10 and 04/10/2026, 1,300,000 VND each, receipts attached) and resubmits.
4. E-0501 rejects claim T without a comment, then with "Personal meal, not a business expense."
5. E-1001 opens the history of claim B.

**Expected result**

1. Without a comment: not accepted. With a comment: Returned; E-1001 gets an e-mail with the comment.
2. The comment is shown and the lines can be edited. After resubmission: Pending Approval at Level 1, approver E-0501; the route is still "Level 1 + Level 2".
3. After resubmission the route is recalculated to "Level 1 + Level 2" (total 5,200,000 VND); current level 1.
4. Without a comment: not accepted. With a comment: Rejected; E-1003 gets an e-mail with the comment; the claim can no longer be edited or resubmitted.
5. Each action is listed with user, date, time and comment.

### TC-08: Duplicate warning, Finance decision and resubmission

**Priority:** High · **Status:** Not executed

**Checks:** US-03 · AC 1, 5; US-07 · AC 1; US-08 · AC 1, 2, 4; US-05 · AC 5

**Preconditions and data:** Paid claim EC-2026-00005 of E-1001 has line 1 with seller tax code 0401234567, invoice symbol 1C26TAA and invoice number 0000123.

**Steps**

1. E-1003 creates a claim with one Meals line, 12/10/2026, 450,000 VND, receipt attached, with the same three invoice details, and submits.
2. E-1003 selects "Go back and edit".
3. E-1003 submits again and selects "Submit anyway".
4. E-0501 opens the claim and approves it.
5. E-0301 opens the Finance list, opens the claim and tries to verify.
6. E-0301 records "Duplicate" on the line. E-0301 returns the claim without a comment, then with "This invoice was already claimed. Please explain or remove the line."
7. E-1003 adds an explanation to the description and resubmits with "Submit anyway". E-0501 approves again. E-0301 opens the claim.

**Expected result**

1. A "Potential duplicate" warning that does not show E-1001's claim. Nothing is submitted yet.
2. The claim stays Draft; the history has no submission; E-0501 gets no e-mail.
3. Pending Approval; the flag stays on the line; the history records the choice.
4. E-0501 sees the flag and the matched claim EC-2026-00005, line 1.
5. The list shows the claim with claimant, total and flag. Verification is blocked until the line has a decision.
6. Verify is not available. Return without a comment is not accepted; with a comment the claim is Returned and E-1003 gets the comment.
7. The line is flagged again and has no decision; the earlier "Duplicate" decision is still in the history.

### TC-09: Duplicate check rules

**Priority:** Medium · **Status:** Not executed

**Checks:** US-03 · AC 2, 3, 4; US-08 · AC 3

**Preconditions and data:** E-1001 has claim X1 (Pending Approval) with a Taxi line, 08/10/2026, 180,000 VND, no invoice details, and Rejected claim X2 with a Meals line, 09/10/2026, 250,000 VND, invoice 0309876543 / 1C26TBB / 0000456. Paid claim EC-2026-00005 has invoice 0401234567 / 1C26TAA / 0000123.

**Steps**

1. E-1001 creates claim Y, with receipts where needed: (1) Taxi, 08/10/2026, 180,000 VND; (2) Meals, 09/10/2026, 250,000 VND, with X2's invoice details; (3) Meals, 11/10/2026, 320,000 VND, with seller tax code 0401234567 and symbol 1C26TAA but no invoice number. Submits and selects "Submit anyway".
2. E-0501 approves claim Y.
3. E-0301 records "Not a duplicate" on line 1 and verifies.

**Expected result**

1. Only line 1 is flagged (same claimant, date, category and amount as X1). Line 2 is not flagged because X2 is Rejected. Line 3 is not flagged because the invoice check needs all three details.
2. Finance Review.
3. Finance Verified; export status Not Exported.

### TC-10: Approver taken from line-manager data

**Priority:** High · **Status:** Not executed

**Checks:** US-06 · AC 3; US-16 · AC 1

**Preconditions and data:** E-1002 has no line manager. E-1003 has claim Q, Pending Approval at Level 1 with E-0501.

**Steps**

1. E-1002 submits a claim: Taxi, 15/10/2026, 100,000 VND.
2. E-0401 changes E-1003's line manager to E-0101. E-1003 submits a new claim: Office supplies, 15/10/2026, 500,000 VND, receipt attached.
3. E-0401 deactivates E-0501. E-1001 submits a claim: Taxi, 15/10/2026, 100,000 VND.
4. Clean-up: reset E-1003's line manager to E-0501 and reactivate E-0501.

**Expected result**

1. Blocked, with a message to contact the System Administrator.
2. Claim Q still waits for E-0501 (the route was set at submission). The new claim goes to E-0101.
3. Blocked with the same message, because the line manager is inactive.
4. –

### TC-11: Own claim re-routed; one person at both levels (provisional, SRS OQ-01)

**Priority:** High · **Status:** Not executed

**Checks:** US-06 · AC 4

**Preconditions and data:** E-0201 (Finance Manager) has line manager E-0101. E-0301 has line manager E-0201. Receipts attached to every line.

**Steps**

1. E-0201 submits four Hotel lines, 06/10 to 09/10/2026, 1,500,000 VND each (total 6,000,000 VND).
2. E-0101 approves once.
3. E-0301 submits the same kind of claim (total 6,000,000 VND).
4. E-0201 approves once.

**Expected result**

1. Route "Level 1 + Level 2". Both levels go to E-0101 (Level 2 is re-routed away from E-0201).
2. Finance Review. The history shows one approval by E-0101 for both levels.
3. Level 1 and Level 2 are both E-0201 (line manager and Finance Manager).
4. Finance Review; no second approval is asked. The history shows one approval by E-0201 for both levels.

### TC-12: Export file content and claims left out

**Priority:** High · **Status:** Not executed

**Checks:** US-09 · AC 1, 2, 3, 6

**Preconditions and data:** Finance Verified claims with export status Not Exported: 12A of E-1001 with a Training fees line (no GL account code); 12B of E-0201 (Finance department) with a Taxi line, 100,000 VND, verified by E-0302; 12C of E-1001 with two lines: Taxi, 06/10/2026, 95,000 VND, "Taxi to dealer" and Office supplies, 07/10/2026, 160,000 VND, approved by E-0501 on 14/10/2026 and verified by E-0301 on 15/10/2026; 12D of E-1003 with one Taxi line (E-1003 has since been deactivated); 12E, an own claim of E-0301. The cost center code of Finance is cleared before the test.

**Steps**

1. E-0301 opens the export screen.
2. E-0301 selects 12A, 12B, 12C and 12D and generates the file.
3. E-0301 opens the CSV file.
4. Clean-up: restore CC-FIN and reactivate E-1003.

**Expected result**

1. 12A to 12D are listed; 12E is not.
2. 12A is left out: "Category has no GL account code". 12B is left out: "Department has no cost center code". Both stay Not Exported. One batch is saved with 12C and 12D, both Awaiting Confirmation.
3. One header row and three data rows. 12C rows: DocRef = claim ID, DocLine 1 and 2, EmployeeCode E-1001, TxnDate 06/10/2026 and 07/10/2026, AccountCode 6418 and 6428, CostCenter CC-SDN, Amount 95000 and 160000, ApprovalRef E-0501 14/10/2026, VerifiedBy E-0301. 12D is included although E-1003 is inactive.
4. –

### TC-13: Import result not known yet

**Priority:** High · **Status:** Not executed

**Checks:** US-10 · AC 1, 4; US-08 · AC 5; US-11 · AC 2

**Preconditions and data:** Claim B2 of E-1001 is Finance Verified and Awaiting Confirmation in batch EXP-20261014-01. No result has been recorded.

**Steps**

1. E-0301 opens the export screen.
2. E-0301 opens claim B2.
3. E-0301 opens the batch list.

**Expected result**

1. B2 is not listed and cannot be added to a new file.
2. Record payment and Return are not available.
3. EXP-20261014-01 is shown as needing a result.

### TC-14: Rejected by accounting or not imported

**Priority:** High · **Status:** Not executed

**Checks:** US-10 · AC 3; US-11 · AC 2; US-08 · AC 5; US-09 · AC 1

**Preconditions and data:** Claims R1 and R2 of E-1003 are Finance Verified and Awaiting Confirmation. R1 is in batch EXP-20261014-01; accounting rejected it because the cost center was entered as "SALES-DN". R2 is in batch EXP-20261013-01, which was never imported.

**Steps**

1. E-0301 records "Rejected by accounting" for R1 without a reason, then with "Cost center SALES-DN not found".
2. E-0301 records "Not imported" for R2 with "File EXP-20261013-01 was not imported".
3. E-0301 opens R1 and R2.
4. E-0401 corrects the cost center of Sales Da Nang to CC-SDN. E-0301 exports R1 again.
5. E-0301 returns R2 with "Please check the hotel invoice."

**Expected result**

1. Without a reason: not saved. With a reason: R1 is Export Failed; the claim stays Finance Verified; the history shows the result, reason, user and time.
2. R2 is Export Failed.
3. Record payment is not available on either claim; Return is available.
4. R1 is listed as eligible. A new batch is saved and R1 is Awaiting Confirmation in it. The history shows both batches.
5. R2 is Returned and its export status is reset to Not Exported. E-1003 gets the comment.

### TC-15: Outdated export screen and download again

**Priority:** High · **Status:** Not executed

**Checks:** US-09 · AC 4; US-10 · AC 5

**Preconditions and data:** Claims M and N of E-1001 are Finance Verified with export status Not Exported. The steps run one after another, not at the same moment.

**Steps**

1. E-0301 and E-0302 open the export screen.
2. E-0302 exports claim M.
3. Without refreshing, E-0301 selects only M and generates a file.
4. Without refreshing, E-0301 selects M and N, generates a file and cancels the download.
5. E-0301 downloads the batch file again from the batch list.

**Expected result**

1. Both see M and N.
2. Batch 1 with M; M is Awaiting Confirmation.
3. No batch is saved. E-0301 is told that no selected claim is eligible (M: "No longer eligible").
4. Batch 2 with N only; M is left out as "No longer eligible".
5. The same file with the same batch ID; no new batch and no status change.

### TC-16: Payment rules

**Priority:** High · **Status:** Not executed

**Checks:** US-11 · AC 1, 3, 4, 5; US-12 · AC 5; US-08 · AC 5; US-13 · AC 2

**Preconditions and data:** Claim P1 of E-1001 is Finance Verified and Exported in batch EXP-20261014-01, not paid. Claim P2 of E-0301 is Finance Verified and Exported (verified and exported by E-0302).

**Steps**

1. E-0301 opens P1.
2. E-0301 records payment without a date, then without a reference.
3. E-0301 records payment: 16/10/2026, FT2610160001.
4. From a page opened before step 3, E-0301 records payment again.
5. E-1001 opens P1.
6. E-0301 opens P2.

**Expected result**

1. Return is not available; Record payment is.
2. Not saved; a message on the missing field each time.
3. Paid. E-1001 gets an e-mail with the payment date.
4. Refused. The history shows one payment, and E-1001 gets one e-mail only.
5. Paid; export status Exported with batch EXP-20261014-01.
6. Record payment is not available to E-0301; E-0302 can record it.

### TC-17: Access by role and history protection

**Priority:** High · **Status:** Not executed

**Checks:** US-07 · AC 5; US-08 · AC 6; US-10 · AC 8; US-12 · AC 3, 4; US-16 · AC 2, 3

**Preconditions and data:** Claim P of E-1001 is Pending Approval at Level 1 with E-0501. Claim F of E-0301 is in Finance Review and has one line flagged as a potential duplicate. These steps check the screens only.

**Steps**

1. E-1003 opens claim P by its link.
2. E-0101 opens claim P and tries to approve it.
3. E-0401 opens claim P.
4. E-1001 opens the history of claim P and tries to edit or delete an entry.
5. E-0301 opens claim F.
6. E-0401 opens the employee record of E-0301 and then the Finance batch list by its link.
7. E-0401 deactivates E-1003; E-1003 tries to sign in. Clean-up: reactivate E-1003.

**Expected result**

1. Access refused.
2. Access and approval refused: E-0101 is not E-1001's line manager.
3. Access refused (System Administrator).
4. No edit or delete option.
5. No duplicate decision, Verify, Return or Reject is available; E-0302 can act on the claim.
6. The record shows exactly one system role (Finance Officer). The batch list is refused: the System Administrator role gives no Finance access.
7. Sign-in refused; E-1003's submitted claims do not change.

### TC-18: Withdraw, cancel and My Claims

**Priority:** Medium · **Status:** Not executed

**Checks:** US-04 · AC 1, 2, 3; US-12 · AC 1

**Preconditions and data:** Claims of E-1001: W1 Pending Approval at Level 2 (approved at Level 1 by E-0501; approver E-0201); W2 Pending Approval at Level 1 (E-0501); W3 Draft; W4 Returned; W5 Finance Review; W6 Finance Verified, Awaiting Confirmation.

**Steps**

1. E-0501 opens W2. E-1001 then withdraws W2.
2. On the page opened in step 1, E-0501 selects Approve.
3. E-1001 withdraws W1, then submits it again without changes.
4. E-1001 cancels W3 and W4.
5. E-1001 opens W5.
6. E-1001 opens My Claims.

**Expected result**

1. W2 is Draft; the history shows the withdrawal.
2. Refused; no approval is recorded.
3. After withdrawal: Draft. After resubmission: Pending Approval at Level 1 with E-0501; the earlier Level 1 approval no longer counts.
4. Both are Cancelled and cannot be edited or submitted.
5. Withdraw and Cancel are not available.
6. Each claim shows its status and total; W1 shows approver E-0501; W6 shows export status Awaiting Confirmation.

### TC-19: Settings changes and category deactivation

**Priority:** Medium · **Status:** Not executed

**Checks:** US-15 · AC 1, 2, 3; US-02 · AC 5

**Preconditions and data:** Level 2 threshold 5,000,000 VND. Claim S1 of E-1003 (four Hotel lines, 01/10 to 04/10/2026, 1,000,000 VND each, total 4,000,000 VND) is Pending Approval with route "Level 1 only".

**Steps**

1. E-0401 changes the Level 2 threshold to 3,000,000 VND.
2. E-1003 submits claim S2: four Hotel lines, 06/10 to 09/10/2026, 1,000,000 VND each (total 4,000,000 VND).
3. E-0501 approves S1.
4. E-0401 creates category "Parking" (GL 6418, receipt above 200,000 VND, no limit). E-1003 submits a claim with a Parking line (15/10/2026, 50,000 VND). E-1001 saves a Draft with a Parking line (15/10/2026, 30,000 VND, "Parking at warehouse").
5. E-0401 deactivates Parking. E-1001 starts a new claim, then submits the Draft. E-1003 opens the submitted Parking claim.
6. Clean-up: reset the threshold to 5,000,000 VND.

**Expected result**

1. The new value is saved.
2. Route "Level 1 + Level 2".
3. S1 moves to Finance Review; no Level 2 step is added.
4. Parking can be chosen; both claims are saved.
5. Parking is not offered on the new claim. The Draft is blocked with a message that its category is no longer available. E-1003's submitted claim still shows Parking.
6. –

### TC-20: Spending report

**Priority:** Low · **Status:** Not executed

**Checks:** US-14 · AC 1, 2, 3

**Preconditions and data:** Reset the test environment to the test data in section 4, then load only: K1 of E-1001, Paid: Taxi 28/09/2026 150,000 VND and Meals 02/10/2026 300,000 VND. K2 of E-1001, Pending Approval: Taxi 06/10/2026 100,000 VND. K3 of E-1001, Draft: Taxi 07/10/2026 50,000 VND. K4 of E-0201 (Finance), Finance Verified: Taxi 08/10/2026 200,000 VND. K5 of E-1003, Rejected: Meals 05/10/2026 250,000 VND.

**Steps**

1. E-0201 opens the report for expense month 10/2026, all departments, default statuses.
2. E-0201 adds Pending Approval to the status filter.
3. E-0201 selects Download.
4. E-0201 changes the month to 09/2026 (default statuses).

**Expected result**

1. Sales Da Nang – Meals while travelling 300,000 VND; Finance – Taxi and local transport 200,000 VND. Not counted: K1 line 1 (September), K2, K3 and K5.
2. Sales Da Nang – Taxi and local transport 100,000 VND is added.
3. A CSV file with the same figures as on screen.
4. Sales Da Nang – Taxi and local transport 150,000 VND (K1 line 1).

### TC-21: Technical failures leave the data correct

**Priority:** Low · **Status:** Not executed

**Checks:** US-09 · AC 5; US-13 · AC 3

**Preconditions and data:** The test team can force a failure in the test environment (method agreed with IT/QA). (a) Two Finance Verified claims of E-1001 and E-1003 with export status Not Exported. (b) Claim J of E-1001 is Pending Approval at Level 1, route "Level 1 + Level 2" (four Hotel lines, 1,450,000 VND each).

**Steps**

1. With file generation failing, E-0301 selects both claims and generates the file.
2. E-0301 opens the batch list and both claims.
3. With e-mail sending failing, E-0501 approves claim J.
4. IT checks the e-mail failure log. E-0201 opens the approval list.

**Expected result**

1. An error message; no file is offered.
2. No new batch; both claims are still Not Exported.
3. The approval is saved; claim J is at Level 2 with approver E-0201.
4. The log shows the failed e-mail for claim J; claim J is in E-0201's approval list.

### TC-22: Import result: own claim, traceability and System Administrator (BA recommendation)

**Priority:** High · **Status:** Not executed

**Checks:** US-10 · AC 6, 7, 8; US-12 · AC 2

**Preconditions and data:** Batch EXP-20261015-01 was exported by E-0302 and holds two Finance Verified claims, both Awaiting Confirmation: G of E-0301 (Finance Officer) and H of E-1001. In the accounting software, G was imported and H was rejected because the employee code was not recognised (simulated). These steps check the screens only.

**Steps**

1. E-0301 opens the batch list and batch EXP-20261015-01.
2. E-0302 opens the same batch, records "Imported" for G, records "Rejected by accounting" for H with the reason "Employee code not recognised", and saves.
3. E-0301 opens claim G and its history.
4. E-1001 opens claim H and its history.
5. E-0401 (System Administrator) opens the batch list by its link.

**Expected result**

1. G is shown without result options, with a message that another Finance Officer records its result. H has result options.
2. G is Exported and H is Export Failed; both stay Finance Verified.
3. G shows export status Exported. Its history shows batch EXP-20261015-01, result Imported, user E-0302 and the date and time; no result is recorded by E-0301.
4. H shows export status Export Failed. Its history shows the export in EXP-20261015-01 and the result "Rejected by accounting" with the reason, user E-0302 and the date and time.
5. Access refused; no result can be recorded.

## 4. Test data

Fictional employees, departments and the example settings used by the test cases.

### Employees

| Employee ID | Name | Department | System role | Job title | Line manager | Used for |
|---|---|---|---|---|---|---|
| E-1001 | Nguyen Van An | Sales Da Nang | Employee | Sales Executive | E-0501 | Main claimant |
| E-1003 | Hoang Van Minh | Sales Da Nang | Employee | Sales Executive | E-0501 | Second claimant; duplicate, access and deactivation tests |
| E-1002 | Bui Thi Lan | Sales Ha Noi | Employee | Sales Executive | (none - on purpose) | No line manager: submission must be blocked (TC-10) |
| E-0501 | Tran Thi Binh | Sales Da Nang | Employee | Sales Team Leader | E-0101 | Line manager of E-1001 and E-1003 (Level 1 approver) |
| E-0201 | Le Minh Chau | Finance | Finance Manager | Finance Manager | E-0101 | Level 2 approver; line manager of E-0301 and E-0302 |
| E-0301 | Vo Thi Hoa | Finance | Finance Officer | Accountant | E-0201 | Finance Officer in most tests; has own claims (TC-12, TC-16, TC-17, TC-22) |
| E-0302 | Dang Quoc Khanh | Finance | Finance Officer | Accountant | E-0201 | Second Finance Officer; acts on E-0301's claims, including their import results |
| E-0101 | Pham Quoc Dung | Management | Employee | General Director | (none) | Line manager of E-0201 and E-0501 |
| E-0401 | Ngo Thanh Tung | IT | System Administrator | IT Officer | E-0101 | Maintains settings and employees; cannot open other people's claims or Finance batches |

### Departments

| Department | Cost center code | Note |
|---|---|---|
| Sales Da Nang | CC-SDN | TC-14 starts from a wrong value (SALES-DN). |
| Sales Ha Noi | CC-SHN |  |
| Finance | CC-FIN | TC-12 clears this code before the test. |
| Management | CC-MGT |  |
| IT | CC-IT |  |

### Expense categories (SRS §3.4.2, example values)

| Category | GL account code | Receipt needed above (VND) | Limit per line (VND) |
|---|---|---|---|
| Taxi and local transport | 6418 | 200,000 | No limit |
| Hotel | 6418 | 0 (always) | 1,500,000 |
| Meals while travelling | 6418 | 200,000 | 500,000 |
| Client entertainment | 6428 | 0 (always) | 3,000,000 |
| Office supplies | 6428 | 200,000 | 1,000,000 |
| Training fees | (not set) | 0 (always) | No limit |

### Global settings

| Setting | Value |
|---|---|
| Submission deadline | 30 days after the expense date |
| Level 2 threshold | Claim total above 5,000,000 VND |

## 5. CR-01: a simulated change request

> [!NOTE]
> CR-01 is simulated. It is **not approved and not applied**. It shows how I would assess the impact of a change across the SRS, backlog and test cases.

**CR-01: Client entertainment claims always need Finance Manager approval**

| Item | Detail |
|---|---|
| Status | Proposed |
| Requested by | Finance Manager (simulated) |
| Reason | Client entertainment is a sensitive cost. The Finance Manager wants a second check on every such claim, even below the Level 2 threshold. |
| Current rule | BR-04: the route depends only on the claim total. Level 2 is added when the total is above [5,000,000 VND], so a Client entertainment claim at or below the threshold goes to Level 1 only. |
| Requested change | Add a category setting "Always needs Level 2". If a claim has at least one line in such a category, the route is "Level 1 + Level 2" whatever the total. |
| Configuration or requirement change? | FR-15 lets the System Administrator change existing values (limits, thresholds). This request adds a new kind of rule, so it is a requirement change that needs development. |
| Effort (qualitative) | Small: one new category field and one rule change. 15 items to update or add (below) and 5 test cases to re-run. |
| Risk | More Level 2 work for the Finance Manager. The number of entertainment claims per month is unknown; ask Finance (Elicitation Plan). |
| Decision | Waiting for the Product Owner (simulated). If approved, the items below are updated together. |

### Impact if CR-01 is approved

| Group | Document | Item | Change needed | Action |
|---|---|---|---|---|
| Direct | SRS | BR-04 Approval route | Add the category condition to the route rule. | Update |
| Direct | SRS | FR-15 Maintain categories and settings | Add the new category field. | Update |
| Direct | SRS | §3.4.2 Illustrative policy settings (Table 25) | Add a column "Always needs Level 2"; set Client entertainment to Yes. | Update |
| Direct | SRS | §7 Data model (Figure 12 and Table 37) | Add the new field to Expense Category. | Update |
| Direct | Diagram source | erd.drawio | Add the field to Expense Category and export Figure 12 again. | Update |
| Direct | SRS | §1.2 Scope and §2.3 Users (Finance Manager) | "Claims above the threshold" becomes "claims above the threshold or in a category that always needs Level 2". | Update |
| Direct | SRS | Appendix B, OQ-06 (Level 2 per claim) | Note that Level 2 can also come from the category, not only from the total. | Update |
| Direct | SRS | Figure 1 Claim form, state A (route preview) | The route preview must show why Level 2 applies (total or category). | Update |
| Direct | Wireframe source | wf_claim_A.svg | Update the route preview and export Figure 1 again. | Update |
| Direct | Elicitation Plan | Finance questions | Ask how many client entertainment claims there are each month. | Update |
| Direct | Product Backlog | US-06 AC 1 | Add "and no line is in a category that always needs Level 2". | Update |
| Direct | Product Backlog | US-06 new AC 5 | "Given my claim has a Client entertainment line and a total of 800,000 VND, when I submit, then the route is Level 1 + Level 2." | Add |
| Direct | Product Backlog | US-15 AC 1 | Include the new setting when a category is created. | Update |
| Direct | Validation Workbook | TC-02 | Add a step: Client entertainment claim of 800,000 VND → route "Level 1 + Level 2". | Update |
| Direct | Validation Workbook | TC-19 | The new Parking category must include the new setting. | Update |
| Regression | Validation Workbook | TC-01, TC-07, TC-10, TC-11, TC-19 | Re-run: they check routing. Their claims have no Client entertainment line below the threshold, so the expected routes do not change. | Re-run |
| No change | SRS | BR-05, BR-09; Figures 8 and 10 (context, activity); §6.2 export mapping | An own claim is still re-routed (BR-05) and the route is still set at submission (BR-09). No new status, step or export column. | Review only |

