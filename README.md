# Automated Data Collection & Reporting Pipeline (Power Platform)

**Tools:** Power Automate · Power Apps · Microsoft Dataverse · Power BI  

---

## Overview

A fully low-code data pipeline built on Microsoft Power Platform. Power Apps collects structured business form data and writes it to Dataverse with relational schemas and validation rules enforced at entry. Power Automate cloud flows orchestrate routing, notifications, and quality checks. Power BI delivers real-time operational dashboards connected live to Dataverse.

This project replaces a manual spreadsheet-based reporting cycle for a simulated multi-department business scenario.

---

## Dataset / Sample Data

**Microsoft Power BI Sample Datasets (Official)**  
📥 https://learn.microsoft.com/en-us/power-bi/create-reports/sample-datasets

Download the **Customer Profitability Sample** and **Retail Analysis Sample** `.pbix` files — these serve as the basis for the Power BI dashboard layer.

**PnP Power Automate Community Samples**  
📥 https://github.com/pnp/powerautomate-samples

Specifically, reference:
- `teams-adaptive-card-reminders` — flow trigger patterns
- `sharepoint-collect-feedback` — list/Dataverse write patterns

**Microsoft Power Platform Templates**  
📥 https://github.com/microsoft/Templates-for-Power-Platform

Use the `Employee Kudos` and `Hardware Request` templates as structural references for the Power Apps model-driven app pattern.

---

## Project Structure

```
3-power-platform-pipeline/
├── docs/
│   ├── architecture.md          # System design and data flow diagram
│   ├── dataverse_schema.md      # Table definitions and relationships
│   ├── power_automate_flows.md  # Flow documentation (trigger → action)
│   └── powerbi_dax_measures.md  # DAX measures used in dashboard
├── src/
│   ├── dataverse_schema.json    # Exportable Dataverse table definitions
│   ├── sample_data.csv          # Seed data for testing
│   └── dax_measures.txt         # All DAX measures for Power BI
└── README.md
```

---

## Architecture

```
[User / Field Staff]
       │
       ▼
[Power Apps Canvas App]
  - Data entry form
  - Client-side validation
  - Lookup fields (dropdowns from Dataverse)
       │
       ▼
[Microsoft Dataverse]
  - Tables: Submissions, Products, Departments, Audit_Log
  - Column validation rules
  - Relational lookups
       │
       ├──────────────────────────────────┐
       ▼                                  ▼
[Power Automate Cloud Flow]        [Power BI Service]
  - Trigger: New Dataverse row       - Live connection to Dataverse
  - Validate completeness            - Real-time operational dashboard
  - Route to approver                - Trend analysis, KPIs, alerts
  - Write to Audit_Log table         - Row-level security by department
  - Send Teams/email notification
```

---

## Setup Instructions

### Prerequisites
- Microsoft 365 license with Power Platform access
- Power BI Pro or Premium Per User license
- Dataverse environment (Default or dedicated)

### Steps

1. **Import Dataverse schema**
   - Go to Power Apps > Tables > Import
   - Upload `src/dataverse_schema.json`
   - Verify relationships between Submissions, Departments, Products

2. **Import Power Automate flows**
   - Go to Power Automate > My Flows > Import
   - Upload the flow `.zip` packages (reference `pnp/powerautomate-samples`)
   - Reconnect Dataverse and Outlook/Teams connectors

3. **Connect Power BI**
   - Open Power BI Desktop
   - Get Data → Dataverse
   - Connect to your environment URL
   - Load `Submissions`, `Audit_Log`, `Departments` tables
   - Apply DAX measures from `src/dax_measures.txt`

4. **Load sample data**
   - Import `src/sample_data.csv` into the Submissions table via Power Apps or Excel connector

---

## References

- Power BI Sample Datasets: https://learn.microsoft.com/en-us/power-bi/create-reports/sample-datasets
- PnP Power Automate Samples: https://github.com/pnp/powerautomate-samples
- Microsoft Power Platform Templates: https://github.com/microsoft/Templates-for-Power-Platform
- Dataverse documentation: https://learn.microsoft.com/en-us/power-apps/maker/data-platform/
