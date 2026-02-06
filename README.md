# Bank Account Management System – Build Challenge (Assignment 1)

## Overview

This project implements a **bank account management system** in Python that supports multiple account types, transaction processing, complete transaction history tracking, and monthly statement generation.

The system follows clean object-oriented design principles and includes comprehensive unit tests to validate business rules, transaction validation, and state management.

---

## Features

- Supports **CHECKING** and **SAVINGS** account types
- Handles **DEPOSIT**, **WITHDRAWAL**, and **TRANSFER** transactions
- Records full transaction history (including failed transactions)
- Enforces account-specific rules (fees, minimum balance, withdrawal limits)
- Applies monthly interest for savings accounts
- Generates formatted monthly account statements
- Includes a demo that exercises all required scenarios

---

## Account Rules

### CHECKING Account
- No minimum balance
- First **10 successful transactions per month are free**
- After 10 transactions, a **$2.50 fee** is applied per successful transaction
- Fee applies to **all transaction types**:
  - Deposit
  - Withdrawal
  - Transfer

### SAVINGS Account
- Minimum balance: **$100**
- Maximum **5 withdrawals per month**
- Earns **2% monthly interest**
- Transfers count as withdrawals
- **Unlimited deposits** are allowed

---

## Transaction Recording

Every transaction (successful or failed) is recorded with:
- `transactionId`
- `timestamp`
- `type` (DEPOSIT / WITHDRAWAL / TRANSFER)
- `amount`
- `balanceBefore`
- `balanceAfter`
- `status` (SUCCESS / FAILED)
- `reason` (for failures, fees, or interest)

Failed transactions do **not** modify account balances but are always recorded for auditability.

---

## Prerequisites

- **Python 3.10+** (recommended)
- pip

To confirm:
```bash
python --version
pip --version
```

## Setup & Installation

Create and activate a virtual environment (Unix/macOS):

```bash
python -m venv .venv
source .venv/bin/activate
```

Create and activate a virtual environment (Windows PowerShell):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Run Unit Tests

From the `task_1` directory (Unix/macOS):

```bash
PYTHONPATH=src pytest -q
```

From the `task_1` directory (Windows PowerShell):

```powershell
$env:PYTHONPATH = 'src'
pytest -q
```

All tests should pass successfully.

## Run Demo

From the project root (Unix/macOS):

```bash
PYTHONPATH=src python -m bank_system.demo
```

From the project root (Windows PowerShell):

```powershell
$env:PYTHONPATH = 'src'
python -m bank_system.demo
```

The `demo.py` module exercises account operations and prints sample output to the console.

## Assumptions

- The initial deposit recorded during `openAccount()` counts as a successful monthly transaction and increments `monthlyTransactionCount`.
- For `CHECKING` accounts, the $2.50 transaction fee applies after 10 free successful transactions per month.
- The transaction fee applies to all transaction types (`DEPOSIT`, `WITHDRAWAL`, `TRANSFER`), not only deposits.
- `SAVINGS` accounts are assumed to allow unlimited deposits; limits specified in the assignment apply only to withdrawals.
- Failed transactions are always recorded but do not modify account balances.
- Monthly transaction counters reset as part of monthly processing (assumed per assignment scope).

## Sample Input and Output

The demo file (`demo.py`) serves as the sample input and output for this assignment. The demo demonstrates:

- Opening multiple accounts
- Deposits, withdrawals, and transfers
- Transaction fees for `CHECKING` accounts
- Withdrawal limits for `SAVINGS` accounts
- Failed transactions due to rule violations
- Monthly statements with full transaction history and ending balances

The console output produced by `demo.py` represents the expected sample output.

---