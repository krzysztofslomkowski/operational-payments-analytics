# Operational Payments Analytics

End-to-end operational analytics system for a service-based education business.

This project consolidates financial transactions, contracts and calendar data into a single analytics pipeline used to monitor cashflow, payment delays and lesson balance.

The system is based on real historical production data from an education business.

---

## Business Context

Service-based education businesses face three recurring operational problems:

1. Payments come from multiple sources with inconsistent descriptions.
2. There is no single source of truth for overdue payments.
3. Contracted lessons are hard to reconcile with lessons delivered and planned.

This project solves all three by building a unified operational analytics layer.

---

## Project Scope

The repository contains three tightly integrated analytical modules:

### 1. Payments & Cashflow Analytics
- Consolidation of bank transfers, cash and card payments
- Data cleaning and normalization
- Matching payments to students and contracts
- Monthly cashflow calculation
- Payment status classification

### 2. Debtors Monitoring & Notifications
- Detection of overdue payments
- Debtors segmentation by delay thresholds
- Automated reminder logic
- Communication log for recovery tracking

### 3. Lessons Balance & Capacity Analysis
- Contracted vs delivered vs planned lessons
- Integration with Google Calendar data
- Lesson balance per student and per teacher
- Capacity utilization analysis

---

## Data Sources

The project is built on historical operational data from the **2024/25 academic year**.

Primary source:
- Administrative Excel file containing consolidated operational data

Planned raw data inputs (to be added):
- Bank transaction exports (CSV)
- Cash and card payment records
- Google Calendar lesson exports
- Contract and student reference data

---

## Architecture

The project follows a three-layer data architecture:

### RAW
Planned input layer.
Unmodified source files to be added as separate datasets.

### CLEAN
Standardized and validated datasets derived from the administrative file and raw inputs.
- Unified identifiers
- Normalized dates and amounts
- Clean payment and lesson records

### LOGIC
Business logic and analytical models.
- Cashflow calculations
- Debtors detection
- Lesson balance computation

---

## Repository Structure

operational-payments-analytics/
├── 01_data_raw/ # planned
├── 02_data_clean/
├── 03_models/
├── 04_automation/
├── 05_dashboards/
└── README.md


---

## Tech Stack

- SQL
- Google Sheets
- Google Apps Script
- Python (optional extensions)
- Google Calendar API

---

## Key Outcomes

- Single source of truth for operational finance
- Automated detection of overdue payments
- Clear visibility into lesson balance and capacity
- Reduced manual administration effort
- Scalable analytics framework applicable to any service-based business

---

## Status

Work in progress.

Current focus:
- Payments & Cashflow Analytics module
- Data model definition and normalization

---

## Author

Krzysztof Słomkowski
