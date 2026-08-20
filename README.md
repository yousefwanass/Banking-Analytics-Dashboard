# Banking Analytics Dashboard

**A Power BI Business Intelligence Solution for Banking Operations**

![Project Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Power BI](https://img.shields.io/badge/Power%20BI-Advanced-blue)
![DAX](https://img.shields.io/badge/DAX-46%20Measures-orange)

---

## 📋 Project Overview

An end-to-end Power BI Business Intelligence solution built to monitor, analyze, and visualize key banking performance metrics. It provides insight into customer behavior, financial health, operational efficiency, risk management, and customer support quality — helping banking teams make data-driven decisions on retention, revenue growth, loan performance, and service improvement.

Everything in this project — data validation, modeling, relationships, and all 46 DAX measures — was built directly in Power BI Desktop.

---

## ✨ Key Features

- **5,000+ Customers** with demographic, geographic, and behavioral data
- **20,000+ Transactions** spanning 2022–2025
- Full **Time Intelligence** (Monthly, Quarterly, Yearly, Seasonal trend analysis)
- **Churn Analysis** — identifies customers who have stopped transacting
- **Cohort Retention Matrix** — tracks customer activity month-over-month since joining
- Star-schema data model across 6 entities
- Interactive dashboards with cross-filtering across 6 dedicated report pages
- Seasonal breakdowns (Spring, Summer, Fall, Winter) across Customers, Transactions, and Loans
- Geographic analysis by U.S. State

---

## 🗂️ Data Model

Star schema with **Customers** as the hub table:

```
                    Customers (hub)
                    /   |   |   \
             Accounts Loans Cards SupportCalls
                /
         Transactions
```

| Table | Rows | Description |
|---|---|---|
| Customers | 5,000 | Demographics, join date, state, season |
| Accounts | 5,000 | Account type, balance, creation date |
| Transactions | 20,000 | Transaction type, amount, date, season |
| Loans | 2,500 | Loan type, amount, interest rate, start/end dates, season |
| Cards | 4,000 | Card type, issue/expiration dates |
| SupportCalls | 3,000 | Issue type, resolution status, call date |

Plus a disconnected **Months Since Join** table (0–36) used to power the cohort retention matrix.

---

## 📊 Dashboard Pages

### 1. Customers
Total customers, new customers, customers with/without an account, geographic distribution by state, seasonal join trends, churn rate, active vs. churned customer split, and a full **cohort retention matrix** (% of each monthly cohort still transacting N months after joining).

### 2. Accounts
Total accounts and balance, breakdown by account type (Business/Checking/Savings), active vs. dormant account tracking, and balance trends by account opening date.

### 3. Transactions
Transaction volume and value trends over time, breakdown by transaction type (Deposit/Withdrawal/Transfer/Payment) and account type, seasonal transaction patterns.

### 4. Loans
Loan portfolio breakdown by type (Home/Car/Personal/Education), interest rate range (min/avg/max), active vs. matured loans, and loan origination by season.

### 5. Cards
Card issuance by type (Debit/Credit/Prepaid), active vs. expired cards, and average cards per customer.

### 6. Support Calls
Resolution rate, resolved vs. unresolved call volume, and breakdown by issue type.

---

## 🧮 DAX Measures

46 measures organized into 6 display folders, mirroring the dashboard structure. See [`docs/DAX_Measures.md`](docs/DAX_Measures.md) for the full list with descriptions.

Highlights:
- **Churn Rate** — % of transacting customers with no activity in the last 90 days of available data
- **Cohort Retention %** — month-by-month retention using a disconnected date-offset table
- **% Dormant Accounts**, **% Expired Cards**, **Resolution Rate** — operational health indicators

---

## 🛠️ Tech Stack

- **Power BI Desktop** — data modeling, visualization
- **DAX** — 46 measures across 6 display folders
- **Power Query (M)** — data import and transformation

---

## 📁 Project Structure

```
Banking-Analytics-Dashboard/
├── Banking_Analytics_Dashboard.pbix
├── README.md
├── screenshots/
│   ├── 01_landing_page.png
│   ├── 02_customers.png
│   ├── 03_accounts.png
│   ├── 04_transactions.png
│   ├── 05_loans.png
│   ├── 06_cards.png
│   └── 07_support_calls.png
├── data/
│   ├── customers.csv
│   ├── Banking_Analytics_Transactions_Updated.csv
│   └── Banking_Analytics_Dataset.xlsx
└── docs/
    └── DAX_Measures.md
```

---

## 🚀 How to Use

1. Clone the repository
2. Open `Banking_Analytics_Dashboard.pbix` in Power BI Desktop
3. Click **Refresh** to reload the data
4. Explore the 6 report pages

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for details.

Built by Yousef Ashraf
