
#  TokenTrust: Real World Asset Tokenization Contract

StacksTokenize is a Clarity smart contract designed to tokenize **real-world assets (RWAs)** on the Stacks blockchain. This contract enables secure and compliant fractional ownership, dividend distribution, proposal-based governance, and price feed integration for tokenized assets.

---

## 🚀 Features

### ✅ Asset Registration & Tokenization

* Assets are registered by the contract owner.
* Each asset is assigned a unique `asset-id`.
* Assets are fractionalized into **100,000 semi-fungible tokens (SFTs)** per asset.

### 🔐 Ownership & Compliance

* Only the **contract owner** can register new assets.
* KYC status is checked for users interacting with sensitive features (placeholder for future).

### 📊 Asset Metadata

* Assets include:

  * `metadata-uri`
  * `asset-value`
  * `total-dividends`
  * Timestamps for creation and price updates

### 📈 Price Feeds

* Price data is linked to each asset, along with oracle info and last update height.

### 💰 Dividends

* Token holders can claim proportional dividends.
* Dividends are tracked per `asset-id` and `claimer`.

### 🗳️ Proposal Governance

* Holders with ≥10% of tokens can create proposals.
* Community can vote **for/against** within a specified duration.
* Votes are tracked and weighted by token holdings.

### 🔒 Data Integrity & Security

* Multiple validation layers for:

  * Asset values
  * Metadata URIs
  * Proposal durations
  * Minimum vote thresholds
  * KYC level and expiry

---

## 🛠 Data Structures

### Maps

| Map               | Description                            |
| ----------------- | -------------------------------------- |
| `assets`          | Stores asset metadata and value        |
| `token-balances`  | Tracks user balances for each asset    |
| `kyc-status`      | Tracks KYC approval and expiry         |
| `proposals`       | Governance proposals                   |
| `votes`           | Tracks user votes per proposal         |
| `dividend-claims` | Last dividend claim per user per asset |
| `price-feeds`     | Oracle-based price updates             |

---

## 📥 Public Functions

### `register-asset(metadata-uri, asset-value)`

> Register a new real-world asset. Only callable by contract owner.

### `get-asset-info(asset-id)`

> Fetch all metadata of a given asset.

### `get-balance(owner, asset-id)`

> Check the token balance for a user.

### `claim-dividends(asset-id)`

> Claim dividend payouts based on user’s token holdings.

### `create-proposal(asset-id, title, duration, minimum-votes)`

> Submit a new governance proposal.

### `vote(proposal-id, vote-for, amount)`

> Vote on an active proposal.

---

## 🧪 Read-Only Functions

* `get-asset-info(asset-id)`
* `get-balance(owner, asset-id)`
* `get-proposal(proposal-id)`
* `get-vote(proposal-id, voter)`
* `get-price-feed(asset-id)`
* `get-last-claim(asset-id, claimer)`

---

## 📌 Constants & Limits

* `tokens-per-asset`: 100,000
* `MAX-ASSET-VALUE`: 1 trillion
* `MIN-ASSET-VALUE`: 1,000
* `MAX-DURATION`: ~1 day
* `MIN-DURATION`: ~1 hour
* `MAX-EXPIRY`: ~1 year

---

## ⚠️ Error Codes

| Code        | Meaning                         |
| ----------- | ------------------------------- |
| `u100`      | Only owner can call             |
| `u101`      | Asset or data not found         |
| `u102`      | Already listed                  |
| `u103`      | Invalid amount                  |
| `u104`      | Not authorized                  |
| `u105`      | KYC required                    |
| `u106`      | Vote already exists             |
| `u107`      | Vote period ended               |
| `u108`      | Price feed expired              |
| `u110-u117` | Various input validation errors |

---

## 📚 Future Improvements

* Full KYC enforcement logic
* Asset transfer and lock functionality
* Proposal execution and resolution
* Oracle feed updates and verification
* Secondary market support

---

## ✅ Deployment Notes

* Ensure `contract-owner` is correctly set at deployment.
* All functions dependent on `tx-sender` for identity.
* Proposal IDs and asset IDs need tracking off-chain until auto-increment support is added.

---

## 💬 Example Usage

```clarity
;; Registering a new asset
(register-asset "https://example.com/asset123.json" u500000)

;; Claiming dividends
(claim-dividends u1)

;; Creating a proposal
(create-proposal u1 "Upgrade building" u24 u5000)

;; Voting
(vote u1 true u1000)
```

---
