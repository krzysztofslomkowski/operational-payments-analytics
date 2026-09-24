# Operational Payments Analytics

Portfolio case study for an operational payments and lesson-settlement problem in a service-based education business.

## Current status

**Documentation / solution-design stage.**

At the moment this repository contains the project description only. It does **not** yet contain a working SQL/Python pipeline, dashboard, automation or production data. The sections below describe the business problem and the intended analytical solution.

## Business context

In a music-school operation, payments can arrive through bank transfers, cash and card, while lessons are scheduled separately. This creates recurring operational questions:

- which payments belong to which student or contract,
- which balances are genuinely overdue,
- how many lessons were contracted, delivered and planned,
- where manual reconciliation creates unnecessary administrative work.

## Intended scope

### 1. Payments and cashflow
- consolidate transaction sources,
- normalize descriptions, dates and amounts,
- match payments to students/contracts,
- calculate monthly cashflow and payment status.

### 2. Debtors monitoring
- identify overdue balances,
- segment by delay,
- prepare reminder logic and a communication log.

### 3. Lessons balance and capacity
- compare contracted, delivered and planned lessons,
- connect lesson schedules with payment/contract records,
- show lesson balance by student and teacher,
- support capacity analysis.

## Data inputs considered

The concept is based on real operational workflows from an education business. Any public version of the project should use anonymised or synthetic data.

Potential inputs:
- bank transaction exports (CSV),
- cash/card payment records,
- Google Calendar lesson exports,
- student and contract reference data.

## My role

My contribution is primarily **business and operational**:

- defining the problem from real administrative workflows,
- identifying business rules and exceptions,
- specifying expected outputs and acceptance criteria,
- validating whether the proposed logic reflects how the school actually operates.

Technical implementation is developed with substantial assistance from **ChatGPT/Codex**. I do not present this repository as evidence of independent software-engineering, SQL or Python proficiency.

## Planned implementation

A future implementation may use:
- Google Sheets / Excel for operational validation,
- SQL or Python for transformation and reconciliation,
- Google Calendar exports/API for lesson data,
- a lightweight dashboard for review.

Those technologies are **planned**, not evidence of completed implementation in the current repository.

## Next steps

1. Add an anonymised sample dataset.
2. Implement one narrow workflow end-to-end: payment import → matching → overdue status.
3. Add tests/validation examples for ambiguous payment cases.
4. Only then expand to lesson-balance and capacity analysis.

## Author

Krzysztof Słomkowski
