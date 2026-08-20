# DAX Measures Documentation

46 measures organized into 6 display folders inside a dedicated `_Measures` table, mirroring the dashboard's 6 report pages.

---

## 01 Customers (5 measures)

| Measure | Description |
|---|---|
| `_Total Customers` | Distinct count of customers |
| `New Customers (This Year)` | Customers who joined in the latest year present in the data |
| `Customers with Accounts` | Distinct customers who have at least one account |
| `Customers without Accounts` | Total customers minus those with accounts |
| `% Customers without Accounts` | Share of the customer base with no account |

### 01 Customers \ Churn Analysis (4 measures)

| Measure | Description |
|---|---|
| `Customers Ever Transacted` | Customers with at least one transaction |
| `Churned Customers` | Customers whose last transaction is more than 90 days before the latest transaction date in the data |
| `Active Customers (Transacting)` | Customers ever transacted minus churned customers |
| `Churn Rate` | Churned Customers ÷ Customers Ever Transacted |

### 01 Customers \ Cohort Analysis (3 measures)

| Measure | Description |
|---|---|
| `Cohort Size` | Number of customers who joined in the cohort month in context |
| `Cohort Active Customers` | Customers from that cohort who transacted N months after joining (N from the disconnected `Months Since Join` table) |
| `Cohort Retention %` | Cohort Active Customers ÷ Cohort Size — used in the retention matrix |

---

## 02 Accounts (7 measures)

| Measure | Description |
|---|---|
| `Total Accounts` | Count of all accounts |
| `Total Balance` | Sum of all account balances |
| `Average Balance` | Average balance per account |
| `Average Balance per Customer` | Total Balance ÷ Total Customers |
| `Active Accounts` | Accounts with a transaction within 90 days of the latest transaction date in the data |
| `Dormant Accounts` | Total Accounts minus Active Accounts |
| `% Dormant Accounts` | Dormant Accounts ÷ Total Accounts |

---

## 03 Transactions (3 measures)

| Measure | Description |
|---|---|
| `Total Transactions` | Count of all transactions |
| `Total Transaction Amount` | Sum of all transaction amounts |
| `Average Transaction Amount` | Average amount per transaction |

### 03 Transactions \ By Type (4 measures)

| Measure | Description |
|---|---|
| `Total Deposits` | Total amount where TransactionType = "Deposit" |
| `Total Withdrawals` | Total amount where TransactionType = "Withdrawal" |
| `Total Transfers` | Total amount where TransactionType = "Transfer" |
| `Total Payments` | Total amount where TransactionType = "Payment" |

### 03 Transactions \ Trend (2 measures)

| Measure | Description |
|---|---|
| `Transaction Count - Current Year` | Transaction count in the latest year present in the data |
| `Transaction Amount MoM Growth %` | Month-over-month % change in transaction amount (intended for month-level visuals) |

---

## 04 Loans (9 measures)

| Measure | Description |
|---|---|
| `Total Loans` | Count of all loans |
| `Total Loan Amount` | Sum of all loan amounts |
| `Average Loan Amount` | Average amount per loan |
| `Max Interest Rate` | Highest interest rate across all loans |
| `Min Interest Rate` | Lowest interest rate across all loans |
| `Average Interest Rate` | Average interest rate across all loans |
| `Active Loans` | Loans with an end date on or after today |
| `Matured Loans` | Total Loans minus Active Loans |
| `Average Loan Term (Years)` | Average duration between loan start and end dates |

---

## 05 Cards (5 measures)

| Measure | Description |
|---|---|
| `Total Cards` | Count of all cards |
| `Average Cards per Customer` | Total Cards ÷ Total Customers |
| `Active Cards` | Cards with an expiration date on or after today |
| `Expired Cards` | Total Cards minus Active Cards |
| `% Expired Cards` | Expired Cards ÷ Total Cards |

---

## 06 Support Calls (4 measures)

| Measure | Description |
|---|---|
| `Total Support Calls` | Count of all support calls |
| `Resolved Calls` | Calls where Resolved = "Yes" |
| `Unresolved Calls` | Calls where Resolved = "No" |
| `Resolution Rate` | Resolved Calls ÷ Total Support Calls |

---

## Design Notes

- **Churn and dormancy logic** uses the latest date *present in the data* (not `TODAY()`), since the transaction data doesn't extend to the current calendar date. This keeps the measures stable regardless of when the file is opened.
- **Interest rate measures** use a literal `"%"` format string rather than a percentage format, since `InterestRate` is already stored as a plain number (e.g., `4.38` meaning 4.38%) rather than a decimal fraction.
- **Cohort Retention %** relies on a disconnected `Months Since Join` table joined via `TREATAS` inside the measure — there is no physical relationship between it and `Customers`, by design.
- Calculated columns `Season` (Winter/Spring/Summer/Fall) exist independently on **Customers** (based on JoinDate), **Transactions** (based on TransactionDate), and **Loans** (based on LoanStartDate) — each reflects that table's own date field, not a shared or inherited value.
