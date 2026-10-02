# Payment reconciliation: business case and acceptance scenarios

**Status:** requirements example for a proposed prototype. This file does not describe a completed pipeline or measured improvements.

**Author:** Krzysztof Słomkowski. Based on operational experience at Empire Music School; prepared and structured with ChatGPT/Codex assistance. All records and amounts below are fictional.

## Problem and decision

Client records, lesson schedules and payment records can describe the same relationship in different ways. A transfer may be made by a parent or another payer, cover several students, or contain an incomplete reference.

The administrative decision is practical: **which balance can be explained to the payer, and which payment still needs human review?**

The first prototype should make that decision inspectable. Automatic matching is useful only when the system preserves the evidence and exposes uncertainty.

## Users and responsibilities

| User | Decision supported |
| --- | --- |
| Administration | Review imports, resolve ambiguous payments and contact the correct payer. |
| Business owner | Agree the rules and check how exceptions affect balances. |
| Payer | Receive a clear explanation of the amount due and payments already recognised. |

My role is to define these workflows, business rules, exceptions and acceptance criteria, and to check the outputs with users. The implementation would be AI-assisted.

## First prototype scope

A narrow flow: import one bank CSV, preserve the original transaction, suggest a payer match, obtain a review decision, allocate the confirmed payment and explain the remaining balance.

| Included | Deferred |
| --- | --- |
| One CSV format; valid and rejected import rows | Multiple bank integrations |
| Exact references and ambiguous-match review | Matching by name alone |
| Partial payments and unallocated amounts | Automatic refunds |
| Duplicate prevention and reversal history | Accounting or tax reporting |
| A readable statement for one billing period | Full lesson-capacity analytics |

The public repository contains documentation only. No live client data, bank account data or production connection is required for this example.

## Minimum information

| Record | Fields needed for the prototype |
| --- | --- |
| Source transaction | Source ID, payment date, amount, currency and original description |
| Payer | Internal reference and linked student references |
| Charge | Charge ID, payer reference, billing period and amount |
| Matching decision | Transaction ID, proposed payer, reason, status and reviewer decision |
| Allocation | Transaction ID, charge ID and allocated amount |

A payment date and an import date are separate facts. Importing an older transaction must not make it appear to be a new payment.

## Proposed rules and open decisions

These are prototype requirements for discussion, rather than a claim about an implemented algorithm.

| Rule | Expected behaviour |
| --- | --- |
| R1. Preserve provenance | Keep the source transaction and original description; normalisation must not replace the original evidence. |
| R2. Separate dates | Show the bank payment date independently from the import timestamp. |
| R3. Prevent double counting | Re-importing a transaction with the same stable source ID must not create another payment. |
| R4. Confirm ambiguous identity | A name shared by several payers must produce a review item, not a silent allocation. |
| R5. Separate payer and student | Do not assume that the transfer sender and student have the same name. |
| R6. Preserve allocation totals | Allocations must not exceed the available payment amount. A remainder stays visibly unallocated. |
| R7. Support partial payments | The statement shows both the confirmed amount paid and the outstanding amount. |
| R8. Keep corrections traceable | A correction reverses the earlier allocation and records the replacement decision. |
| R9. Explain the balance | A reviewer can trace the statement to charges, confirmed allocations and correction history. |
| R10. Limit reminders | An unresolved payment must be visible during review before administration approves a reminder. |

Before implementation, agree the bank's stable transaction identifier, the rules for combining several charges, the treatment of overpayments and negative transactions, and who can confirm or reverse allocations. Do not guess these policies from a transaction description.

## Synthetic example

Assume one payer has two confirmed charges of PLN 350 each for the same period.

| Input | Expected review outcome |
| --- | --- |
| TX-001: PLN 500, exact payer reference | Allocate PLN 350 to charge A and PLN 150 to charge B after confirming the agreed allocation order. Charge B has PLN 200 outstanding. |
| TX-001 imported again | No additional payment or allocation; record the duplicate import outcome. |
| TX-002: PLN 350, a name shared by two payers | Keep unmatched until administration confirms the payer. |
| TX-003: PLN 800, exact payer reference; charges total PLN 700 | Allocate at most PLN 700. Keep PLN 100 visibly unallocated until an overpayment policy is agreed. |

These amounts illustrate expected behaviour only. They are not real payment records or business results.

## Acceptance scenarios

| Scenario | Given / when | Pass condition |
| --- | --- | --- |
| A1. Historical import | A transaction was paid on 3 September and imported on 2 October. | The statement displays 3 September as the payment date and retains 2 October separately as the import date. |
| A2. Duplicate import | The same source ID is imported twice. | The payer's paid amount increases only once. |
| A3. Ambiguous payer | Two active payers share the transfer sender's name. | Neither balance changes until a reviewer confirms the match. |
| A4. Partial payment | A PLN 350 charge receives a confirmed PLN 200 allocation. | The statement shows PLN 200 paid and PLN 150 outstanding, with a link to the transaction. |
| A5. Shared payer | One payer is responsible for two students. | The reviewer sees the linked charges and the combined payer statement without creating a second copy of the payment. |
| A6. Invalid row | A required amount or payment date is missing. | The row is rejected with a specific reason; valid rows remain available for review. |
| A7. Correction | A reviewer moves a payment allocated to the wrong payer. | The original allocation is reversed; both balances reflect the correction and retain its history. |
| A8. Unresolved incoming payment | A relevant transaction remains unmatched. | Administration can see the unresolved item while reviewing the statement before approving contact with the payer. |

## How I would review the result

1. Confirm the intended rules and the unresolved policy decisions with administration.
2. Run these synthetic scenarios through the first prototype.
3. Compare each resulting statement with a manually prepared expected statement.
4. Report discrepancies as a specific input, expected behaviour and actual result.
5. Change the rule or implementation, then repeat only the affected scenarios.

No time saving, accuracy rate or financial improvement is claimed. Those results would need to be measured after a working prototype is used.
