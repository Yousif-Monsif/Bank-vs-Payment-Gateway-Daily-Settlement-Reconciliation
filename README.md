Got it 👍 — you want **the same structure, tone, and simplicity**, just adapted to **Bank vs Payment Gateway Reconciliation**.
Here is a **clean, professional README** in **exactly that style**.

You can paste this directly into GitHub.

---

# RPA-Bank-vs-Payment-Gateway-Reconciliation

An end-to-end UiPath REFramework automation that performs daily financial reconciliation between a Bank system (SQL Server) and a Payment Gateway (CSV files), identifying matched, mismatched, missing, and invalid transactions with full exception handling.

## Business Scenario

Many banks and fintech companies still perform daily settlement reconciliation manually using Excel sheets.
This automation simulates a real enterprise reconciliation process by:

1. Reading daily bank transactions from a SQL Server database
2. Reading payment gateway transactions from CSV files
3. Validating mandatory fields and data integrity
4. Reconciling transactions using TransactionID as a unique key
5. Generating a reconciliation report with detailed statuses
6. Handling business and system exceptions using REFramework

## Architecture

* **Framework:** UiPath REFramework (Transactional Process)
* **Transaction Source:** SQL Server (BankTransactions table)
* **Transaction Item:** TransactionID (String)
* **Secondary Source:** Payment Gateway CSV file
* **Processing Pattern:** Queue-based reconciliation
* **Logging & Retry:** Built-in REFramework mechanisms

## Process Flow

1. **Init State**

   * Open SQL Server connection
   * Load configuration values
   * Read payment gateway CSV file
   * Validate and clean input data
   * Initialize reconciliation result DataTable

2. **Get Transaction Data**

   * Fetch next bank transaction from SQL
   * Extract TransactionID
   * Add TransactionID to Orchestrator Queue

3. **Process Transaction**

   * Retrieve corresponding gateway transaction
   * Compare amount, currency, and transaction date
   * Assign reconciliation status:

     * `Matched`
     * `Mismatch`
     * `Missing in Gateway`
     * `Invalid Data`
   * Append result to reconciliation output

4. **Exception Handling**

   * Business Exception → Missing fields, invalid amounts or dates
   * System Exception → SQL connection failure, file read errors
   * Failed transactions are logged with detailed reasons

5. **End Process**

   * Write reconciliation results to Excel / CSV
   * Close database connection
   * Final logging

## Database Schema

Table: `BankTransactions`

| Column          | Description        |
| --------------- | ------------------ |
| TransactionID   | Primary Key        |
| Amount          | Transaction amount |
| Currency        | Currency code      |
| TransactionDate | Transaction date   |

## Reconciliation Output

| Column        | Description                            |
| ------------- | -------------------------------------- |
| TransactionID | Unique transaction identifier          |
| Status        | Matched / Mismatch / Missing / Invalid |
| Reason        | Explanation of reconciliation result   |
| Source        | Bank / Gateway                         |

## Technologies Used

* UiPath Studio
* UiPath REFramework
* UiPath Orchestrator Queues
* SQL Server
* CSV File Processing
* Excel / CSV Reporting
* LINQ for data validation and comparison

## Key RPA Concepts Demonstrated

* Queue-based transaction processing
* Financial reconciliation automation
* SQL and file system integration
* Data validation and cleansing
* Dictionary-based fast lookups
* Exception classification (Business vs System)
* Retry logic using REFramework

## Project Value

This project simulates a real-world financial reconciliation use case commonly found in:

* Banks
* Fintech companies
* Payment service providers
* Shared Service Centers
* RPA Centers of Excellence

It demonstrates the ability to design scalable, maintainable, and enterprise-grade reconciliation automations using UiPath best practices.

## Author

**Yousif Monsif**
Junior RPA Developer | Mechatronics Engineer
Specialized in UiPath, SQL Automation.
