# Task 1 — Bank Account Management System (Build Challenge)

A Python-based bank account management system that supports multiple account types, transaction processing (deposit/withdraw/transfer), full transaction history logging (including failures), monthly interest processing for savings, and monthly statements.

This repo includes:
- Clean object-oriented design (`Account`, `Transaction`, `Bank`)
- Rule-based transaction validation
- Full transaction audit trail (SUCCESS/FAILED with reason)
- Unit tests covering core methods and rules
- A demo script that creates 4 accounts and runs 20+ transactions (including failed attempts)

---

## Features Implemented

### Account Types

#### CHECKING
- No minimum balance
- **10 free successful transactions per month**
- After 10 free transactions: **$2.50 fee per successful transaction**

#### SAVINGS
- **Minimum balance: $100** (cannot fall below this after withdrawal/transfer-out)
- **Max 5 withdrawals per month**
  - Withdrawals include:
    - `WITHDRAWAL`
    - `TRANSFER` out (from savings)
- **Earns 2% monthly interest** (applied via `applyMonthlyInterest()`)

---

## Transaction Types
- `DEPOSIT`
- `WITHDRAWAL`
- `TRANSFER`

Every transaction is recorded with:
- `transactionId`
- `timestamp`
- `type`
- `amount`
- `balanceBefore`
- `balanceAfter`
- `status` (`SUCCESS` / `FAILED`)
- `reason` (present for failures and fee/interest notes)

**Failed transactions are still recorded** and do not change account balances.

---

## Project Structure

task_1/
├── README.md
├── requirements.txt
├── .gitignore
├── src/
│ └── bank_system/
│ ├── init.py
│ ├── models.py # Account, Transaction, enums
│ ├── bank.py # Bank class + business rules
│ └── demo.py # Demo: 4 accounts + 20+ txns (incl failures)
└── tests/
├── init.py
├── test_open_close.py
├── test_checking_rules.py
├── test_savings_rules.py
├── test_transfer.py
└── test_history.py


---

## Prerequisites
- **Python 3.10+** (recommended)
- pip

To confirm:
```bash
python --version
pip --version

## Setup Instructions 
Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate

## Install dependencies
pip install -r requirements.txt

## to run the unit tests
PYTHONPATH=src pytest -q

## to run the demo
PYTHONPATH=src python -m bank_system.demo

## Assumptions
- The initial deposit recorded during `openAccount()` counts as a successful monthly transaction and increments `monthlyTransactionCount`.
- For CHECKING accounts, the $2.50 fee applies after 10 free successful transactions per month and applies to **all** transaction types (DEPOSIT, WITHDRAWAL, TRANSFER), not only deposits.
