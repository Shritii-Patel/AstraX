# 👤 AstraX User Guide

## Welcome to AstraX

AstraX is a **Concentrated Liquidity Market Maker (CLMM) DEX on Stellar Soroban**.

The application currently focuses on the XLM/USDC market and provides three primary user experiences:

- **Swap** — exchange XLM and USDC
- **Liquidity** — create and manage concentrated-liquidity positions
- **Portfolio** — monitor positions, liquidity and performance

Live application:

https://astra-x-phi.vercel.app/

> AstraX currently operates on **Stellar Testnet**. Use Testnet assets only.

---

## ✅ Before You Start

You need:
- A compatible browser
- Freighter wallet installed
- A Stellar Testnet wallet/account
- Testnet XLM
- Testnet USDC for relevant actions

Never share your wallet recovery phrase, secret key, private key, or password.

---

## 👛 Connect Your Wallet

1. Open AstraX.
2. Click **Connect Wallet**.
3. Approve Freighter.
4. Verify the connected Stellar account.
5. Confirm you are using **Stellar Testnet**.

If connection fails:
- Unlock Freighter
- Confirm the extension is enabled
- Refresh AstraX
- Verify the network
- Retry the connection

---

## 💱 Swap XLM ↔ USDC

### 1. Open Swap
Navigate to `/swap`.

### 2. Select Tokens
Choose XLM and USDC as input/output assets.

### 3. Enter Amount
AstraX calculates estimated output, pool price, price impact, and minimum received based on slippage protection.

### 4. Review
Before signing, check:
- Input token and amount
- Output token and estimated output
- Slippage
- Price/rate
- Wallet balance

### 5. Sign
Approve the transaction in Freighter only after verifying the details.

### 6. Confirmation
Wait for the Stellar Testnet transaction to finish and review the resulting status.

---

## 💧 Add Concentrated Liquidity

### 1. Open Liquidity
Navigate to `/liquidity`.

### 2. Select Pool
Current primary market: `XLM / USDC`.

### 3. Choose a Price Range
Select a minimum and maximum price. Liquidity is active only while the market price is inside that range.

### 4. Review Token Requirements
Required XLM/USDC depends on current price, selected range, and position size.

### 5. Review Position
Confirm token amounts, price range, current price, position state and minimum values.

### 6. Sign
Approve the transaction in Freighter.

### 7. Position Created
After confirmation, the position can be viewed in Portfolio.

---

## 📊 Portfolio

Navigate to `/portfolio` to review:
- Position ID
- Token pair
- Liquidity
- Price range
- Current price
- In-range / out-of-range state
- Fees
- Position activity

---

## 📍 Position States

### In Range
The current market price is between your minimum and maximum prices. Your position is active and may earn fees.

### Out of Range
The market price moved outside the selected range. Your liquidity becomes inactive until price returns to the range.

This is expected CLMM behavior.

---

## 💸 Collect Fees

1. Open your position.
2. Review accumulated fees.
3. Select collection.
4. Review the transaction.
5. Sign with Freighter.
6. Wait for confirmation.

---

## 📉 Decrease Liquidity

1. Open the position.
2. Select decrease/remove liquidity.
3. Choose the amount.
4. Review expected token amounts.
5. Sign.
6. Verify the updated position.

---

## 🔥 Close / Burn Position

A position can be fully closed after liquidity and relevant fees are handled. Verify that no intended liquidity remains before burning the position.

---

## 🧠 CLMM Basics

CLMM positions concentrate liquidity where an LP expects trading to happen.

### Advantages
- Higher capital efficiency
- More useful liquidity near market price
- Potentially greater fee efficiency

### Risks
- Position can move out of range
- LPs may need active management
- Impermanent loss remains possible
- Narrow ranges require more monitoring

---

## 🛡 Slippage Protection

Slippage is the difference between expected and actual execution price.

If a transaction fails due to slippage:
1. Refresh the quote.
2. Check pool price.
3. Review your slippage setting.
4. Confirm again before signing.

Avoid setting extremely high slippage merely to force execution.

---

## 💵 USDC on Stellar Testnet

Soroban USDC address:
```text
CBIELTK6YBZJU5UP2WWQEUCYKLPU6AUNZ2BQ4WWFEIE3USCIHMXQDAMA
```

Classic Testnet issuer:
```text
GBBD47IF6LWK7P7MDEVSCWR7DPUWV3NY3DTQEVFL4NAT4AQH3ZLLFLA5
```

The classic issuer is relevant for trustlines; Soroban interactions use the asset contract.

---

## 🔍 Verify On-Chain Activity

Current Pool:
```text
CCYBX2FOT5RWL6T2CQROAA3ZECYNNE3PSJ7WQXULU6AJOCCK6YHSTH32
```

Current Position Manager:
```text
CC6IBQ7VNVK7CQYIZX47NJPDH5DL5ISQSA26BLBZXVMVEQ3QGUAZDREI
```

Verify transaction status, timestamp, source account and contract through Stellar Expert.

---

## ⚠️ Common Issues

### Wallet not detected
- Install/unlock Freighter
- Refresh browser
- Confirm extension permissions

### Wrong network
AstraX currently targets Stellar Testnet.

### Insufficient balance
Ensure enough XLM/USDC and enough XLM for fees.

### Transaction rejected
A rejected wallet signature prevents submission. Review and try again only if intended.

### Transaction failed
Possible causes include slippage, invalid range values, insufficient balance, network mismatch, RPC issues, or changed pool state.

---

## 🧪 Testnet Safety

Testnet assets have no real monetary value. Before Mainnet use, AstraX should complete broader testing, a security review/audit, production infrastructure review and verified Mainnet deployment.

---

## 💬 Feedback

AstraX uses feedback to improve onboarding, mobile UX, price/range guidance, slippage handling, transaction review, wallet experience and product reliability.

Never include a wallet secret key or recovery phrase in feedback.
