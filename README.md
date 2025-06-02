# BitLend Protocol

## Decentralized Bitcoin-Backed Lending on Stacks

---

## Overview

**BitLend** is a decentralized lending protocol built on the [Stacks](https://www.stacks.co/) blockchain, leveraging Bitcoin finality for maximum security. It enables users to deposit STX tokens as collateral, earn passive yield, and borrow assets in a trustless, overcollateralized manner.

BitLend introduces robust mechanisms for **risk management**, **automated liquidations**, and **governance**, ensuring a sustainable, decentralized financial ecosystem anchored to Bitcoin.

---

## 🔑 Key Features

* **STX Collateralization**: Deposit STX to access borrowing power or earn passive income.
* **Bitcoin-Secured Finality**: Built on Stacks, leveraging Bitcoin’s security guarantees.
* **Overcollateralized Loans**: Ensures solvency and mitigates systemic risk.
* **Liquidation Protocol**: Automated liquidation of undercollateralized positions.
* **Dynamic Risk Parameters**: Adjustable thresholds for collateral ratio, liquidation, and protocol fees.
* **Governance Hooks**: Owner-controlled updates for protocol safety parameters.

---

## 🏗️ Architecture

```plaintext
                   +---------------------+
                   |   End Users (UI)    |
                   +----------+----------+
                              |
                              v
                      Smart Contract Layer
                (Written in Clarity on Stacks chain)
                              |
    +-------------------------+-------------------------+
    |                         |                         |
    v                         v                         v
[User Positions Map]   [Loan Registry Map]     [Risk Config Vars]
    |                         |                         |
    |                         |                         |
[Deposit / Borrow]   [Loan Lifecycle Ops]     [Collateral Ratios, Fees]
    |                         |                         |
    +-------------------> Protocol State <--------------+
                              |
                     Final Settlement on Bitcoin
```

---

## ⚙️ Core Contract Components

### 📌 Constants

* `MAX-COLLATERAL-RATIO`: Maximum allowable collateral ratio (e.g. 500%)
* `MIN-COLLATERAL-RATIO`: Minimum ratio before protocol disallows borrowing (e.g. 110%)
* `MAX-PROTOCOL-FEE`: Governance-defined fee cap (10%)

### 🧮 Data Structures

* **`user-positions`**: Aggregates each user’s total collateral, borrowed amount, and loan count.
* **`loans`**: Tracks individual loan metadata.
* **Risk Parameters**: Protocol-wide thresholds for safety enforcement.

---

## 🔁 Public Functions

| Function           | Description                                             |
| ------------------ | ------------------------------------------------------- |
| `deposit()`        | Deposit STX into the protocol as collateral.            |
| `borrow(amount)`   | Borrow STX against existing collateral.                 |
| `repay(amount)`    | Repay borrowed STX to reduce debt.                      |
| `withdraw(amount)` | Withdraw collateral (if collateral ratio remains safe). |
| `liquidate(user)`  | Liquidate undercollateralized user positions.           |

---

## 🔐 Governance Functions

Only callable by the **contract owner** (`tx-sender` on deploy):

| Function                            | Purpose                                  |
| ----------------------------------- | ---------------------------------------- |
| `set-minimum-collateral-ratio(val)` | Update required collateralization level. |
| `set-liquidation-threshold(val)`    | Set the liquidation trigger ratio.       |
| `set-protocol-fee(val)`             | Adjust protocol fee rate.                |

---

## 📖 Read-Only Functions

| Function                  | Description                                |
| ------------------------- | ------------------------------------------ |
| `get-user-position(user)` | Retrieve a user’s collateral/loan status.  |
| `get-protocol-stats()`    | Get protocol-wide statistics and settings. |

---

## 🔐 Error Codes

| Code | Description             |
| ---- | ----------------------- |
| 100  | Not authorized          |
| 101  | Insufficient collateral |
| 102  | Invalid amount          |
| 103  | Loan not found          |
| 104  | Loan still active       |
| 105  | Insufficient balance    |
| 106  | Liquidation failed      |
| 107  | Invalid parameter       |

---

## 📦 Deployment & Usage

1. **Deploy contract** on Stacks chain via Clarity-compatible tools (e.g., Clarinet or Hiro Wallet).
2. Interface with smart contract via:

   * Custom front-end dApp
   * [Stacks Explorer](https://explorer.stacks.co/)
   * Clarity REPL or contract calls via SDKs.

---

## 🔒 Security Considerations

* Overcollateralization protects lenders from borrower defaults.
* Automated liquidation ensures solvency.
* Only the owner can update protocol parameters (consider DAO migration).
* Contract follows safe default patterns and conservative limits for risk control.

---

## 📬 Future Improvements

* Tokenized loans and tradable debt positions.
* Integration with wrapped BTC or BTC-native assets.
* DAO-based governance module.
* Oracle integration for dynamic pricing.

---

## 📚 Resources

* [Stacks Documentation](https://docs.stacks.co/)
* [Clarity Language Reference](https://docs.stacks.co/write-smart-contracts/cl)
* [Bitcoin Finality in Stacks](https://docs.stacks.co/understand-stacks/stacks-blockchain)

---

**Built with trustlessness, backed by Bitcoin.**
