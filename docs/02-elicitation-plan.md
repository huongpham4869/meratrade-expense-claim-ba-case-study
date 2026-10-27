# Elicitation Plan

*MeraTrade Distribution – Expense Claim & Approval System*

> [!NOTE]
> MeraTrade Distribution is a fictional company and all people and data are invented. Version 4, 27 Oct 2026. This document is complete for portfolio purposes but has **not** been approved as a business baseline. Values in [square brackets] are examples or assumptions, not company policy.

# 1. Purpose

The SRS is built on assumptions taken from common practice. This plan shows how they would be checked: whom to ask, what to ask, and which requirements could change with each answer. Interview participants act as proxies for MeraTrade roles. Their answers show how similar companies work, not how MeraTrade works, so the key rules still need confirmation from MeraTrade stakeholders.

# 2. Approach

*Table 1. Elicitation methods*

| **Method**          | **What**                                                                                                                                                                                         | **Output**                                                    |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| **Interviews**      | Three semi-structured interviews of 30 to 45 minutes with people who do similar work: an employee who submits claims, a manager who approves them and a finance staff member who processes them. | A short summary of each interview, checked by the participant |
| **Document review** | Blank or anonymised claim forms and expense policies, if participants choose to share them.                                                                                                      | Common fields, rules and receipt requirements                 |
| **Desk research**   | Public product help pages and requirements guides (see SRS §1.4).                                                                                                                                | Common practice; already used in the SRS                      |

**Ground rules**

- Ask for consent before taking notes.

- Record only what the case study needs: role, industry, company size and findings. Do not collect real receipts, salaries, bank details or confidential business data.

- Send each participant a short summary to check. This confirms the summary, not MeraTrade's requirements.

# 3. Participants

*Table 2. Interview participants*

| **Participant** | **Profile**                                        | **Main topics**                                                                                             |
|-----------------|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| **Employee**    | Submits business expenses, for example sales staff | Current process, time to reimbursement, how status is checked, why claims are returned, receipts, phone use |
| **Manager**     | Approves employees’ claims                         | Approval criteria, return or reject, cover during absence, approval threshold, claim purpose                |
| **Finance**     | Reviews claims and reimburses employees            | Checks, duplicates, accounting import, who may record results, payment, record keeping, reports, workload   |

IT and HR are not interviewed in this round. IT must still confirm the accounting file, whether a commercial product is acceptable, the response-time target and how system roles are assigned; HR must confirm the employee and reporting-line data.

# 4. Interview Questions

Start with open questions about the participant's most recent real case, then move to the specific points. The open question that each point helps to answer is shown in brackets.

## 4.1 Employee

1\. Walk me through your last expense claim, from paying to being reimbursed.

2\. How long did it take, and how did you check where it was?

3\. What usually causes a claim to be returned?

4\. Do you need to prepare claims or take receipt photos on your phone?

## 4.2 Manager

1\. How do you review a claim, and how do you find the claims waiting for you?

2\. When do you return a claim instead of rejecting it? Do you need a purpose on every claim to decide?

3\. What happens to claims waiting for you when you are away?

4\. Who approves your own claims? If you are both line manager and second approver for a claim, is one approval enough?

5\. Should the approval limit apply to each claim or to related claims, such as one business trip? Should a corrected claim come back to you or start again at the first level?

## 4.3 Finance

1\. What do you check on each claim, and which problems are most common?

2\. Are spending limits, receipt rules and deadlines written down? Who maintains them, and should claims already in approval be checked again when they change?

3\. How do you notice a receipt claimed twice? Which invoice details help, should claims not yet submitted be compared, and do you need to see every matching expense?

4\. How are claims entered in the accounting software? Which fields are needed, what happens if only part of a claim is rejected, and which cost center is used if a department’s code changes?

5\. Who may record that a claim was booked in the accounting software? May anyone do this, verify it or pay it for their own claim, or for a claim they approved as a manager? Does anyone in Finance also administer the system?

6\. How and when are employees paid? Must paper receipts be kept, and for how long?

7\. Roughly how many claims, status questions and returned claims are there each month, and how long does one claim take you?

8\. How are mistakes corrected after a claim is booked, and how are claims of employees who leave handled?

9\. How should claims still in Excel or e-mail be finished when a new system starts? Must changes to roles, line managers, categories or codes be traceable?

# 5. Assumptions to Confirm

The SRS assumptions and BA recommendations, whom to ask, and what may change if the answer is different. Every open question in SRS Appendix B appears at least once.

*Table 3. Assumptions to confirm*

<table>
<colgroup>
<col style="width: 52%" />
<col style="width: 11%" />
<col style="width: 25%" />
<col style="width: 10%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Assumption in the SRS</strong></th>
<th><strong>Ask</strong></th>
<th><strong>If the answer is different</strong></th>
<th><strong>Open question</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>The problems in SRS §2.1.2 are the main ones.</td>
<td>All</td>
<td>Review the objectives and priorities.</td>
<td>OQ-11</td>
</tr>
<tr class="even">
<td>Receipts, limits and the [30]-day deadline match company policy; over-limit and late lines are justified, not blocked.</td>
<td>Finance</td>
<td>Change the check rules or values.</td>
<td>OQ-05</td>
</tr>
<tr class="odd">
<td>The line manager approves first; the Finance Manager adds Level 2 above [5,000,000 VND]; one approval is enough when one person holds both levels.</td>
<td>Manager, Finance</td>
<td>Change the routing; add an independent second approver.</td>
<td>OQ-01</td>
</tr>
<tr class="even">
<td>The approval threshold applies to each claim.</td>
<td>Manager, Finance</td>
<td>Link related claims and review the scope.</td>
<td>OQ-06</td>
</tr>
<tr class="odd">
<td>A resubmitted claim restarts at Level 1.</td>
<td>Manager, Finance</td>
<td>Send it back to the level that returned it.</td>
<td>OQ-07</td>
</tr>
<tr class="even">
<td>The claim purpose is not checked on submit.</td>
<td>Manager, Finance</td>
<td>Make the purpose required.</td>
<td>OQ-21</td>
</tr>
<tr class="odd">
<td>Duplicates are found by invoice details, or by date, category and amount. Draft and Returned claims are compared, and one match is stored per line.</td>
<td>Finance</td>
<td>Change the matching fields, the claims compared or how many matches are shown.</td>
<td><p>OQ-04</p>
<p>OQ-13</p>
<p>OQ-20</p></td>
</tr>
<tr class="even">
<td>New settings apply only on submission or resubmission.</td>
<td>Finance</td>
<td>Re-check claims already submitted.</td>
<td>OQ-14</td>
</tr>
<tr class="odd">
<td>The accounting software imports a CSV file and accepts or rejects a whole claim. The export uses the department’s cost center code at export time.</td>
<td>Finance, IT</td>
<td>Change the file, how results are recorded or which code is exported.</td>
<td><p>OQ-02</p>
<p>OQ-15</p></td>
</tr>
<tr class="even">
<td><strong>BA recommendation:</strong> only a Finance Officer records import results, never for their own claim; the System Administrator role gives no Finance permissions; each employee has one system role.</td>
<td>Finance, IT</td>
<td>Change BR-05, FR-10, FR-16 and the permission tables.</td>
<td><p>OQ-19</p>
<p>OQ-22</p></td>
</tr>
<tr class="odd">
<td>One person may still act in two steps of another person’s claim.</td>
<td>Finance</td>
<td>Restrict combined steps in BR-05.</td>
<td>OQ-19</td>
</tr>
<tr class="even">
<td>Payment happens after the claim is booked in accounting.</td>
<td>Finance</td>
<td>Change the payment rule.</td>
<td>OQ-03</td>
</tr>
<tr class="odd">
<td>Records are kept for a period set by the accounting-record policy; paper receipts may still be needed.</td>
<td>Finance</td>
<td>Set the retention period; store e-invoice files.</td>
<td>OQ-09</td>
</tr>
<tr class="even">
<td>The System Administrator keeps the HR data up to date.</td>
<td>Finance, HR</td>
<td>Change who owns the data and how updates arrive.</td>
<td>OQ-08</td>
</tr>
<tr class="odd">
<td>A history is kept for claims only.</td>
<td>Finance, IT</td>
<td>Add a history for roles, master data and settings.</td>
<td>OQ-18</td>
</tr>
<tr class="even">
<td>Claims already in the old process at go-live are finished there.</td>
<td>Finance</td>
<td>Plan a different transition.</td>
<td>OQ-17</td>
</tr>
<tr class="odd">
<td>A desktop browser is enough for the MVP.</td>
<td>Employee, Manager</td>
<td>Add mobile use to the scope.</td>
<td>OQ-12</td>
</tr>
<tr class="even">
<td>Lists open within [3 seconds].</td>
<td>IT</td>
<td>Change the target in NFR-07.</td>
<td>OQ-16</td>
</tr>
<tr class="odd">
<td>A commercial expense product is acceptable.</td>
<td>Finance, IT</td>
<td>Re-assess the solution options.</td>
<td>OQ-10</td>
</tr>
</tbody>
</table>

# 6. Baseline Measures

These measures describe the current process. They are needed before any target can be set (see SRS §2.1.3).

*Table 4. Baseline measures*

| **Measure**                | **Objective**        | **Definition**                                                                 |
|----------------------------|----------------------|--------------------------------------------------------------------------------|
| **Status enquiries**       | Status visibility    | Times per month that employees ask Finance or managers about a claim’s status. |
| **Days to payment**        | Status visibility    | Average calendar days from first submission to payment.                        |
| **Returned claims**        | Consistent policy    | Share of claims returned for correction at least once.                         |
| **Duplicates found**       | Lower duplicate risk | Duplicates found before payment compared with those found after payment.       |
| **Finance time per claim** | Less Finance effort  | Active Finance time to check and book one claim.                               |
| **Report preparation**     | Faster reporting     | Time to prepare the monthly expense summary.                                   |

No value has been collected yet. If records are missing, count status enquiries over two normal weeks and label any monthly figure based on that sample as an estimate. Record the source and the period of every value.
