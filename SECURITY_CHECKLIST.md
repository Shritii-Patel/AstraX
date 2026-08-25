# 🛡 AstraX Security Checklist

## Purpose

This document provides a structured security checklist for AstraX's Soroban contracts, frontend, wallet integration, deployment pipeline and future Mainnet preparation.

> This checklist is **not an external smart contract audit**.

---

## 1. Protocol-Level Security

### Contract Separation
- [x] Factory has dedicated registry/deployment responsibility
- [x] Pool contains core CLMM accounting
- [x] Router provides user-facing swap routing
- [x] Position Manager handles position lifecycle
- [x] User Profile logic is separated from liquidity logic

### Administrative Controls
Review privileged functions such as `set_protocol_fee`, `set_fee_recipient`, and `set_pool_price`.

- [ ] Every admin-only function requires proper authorization
- [ ] Admin identity cannot be replaced unexpectedly
- [ ] Protocol-fee limits are bounded
- [ ] Fee recipient cannot be changed by unauthorized accounts
- [ ] Administrative actions emit events where appropriate

---

## 2. Factory Security

- [ ] Reject invalid token addresses
- [ ] Reject identical token pairs
- [ ] Canonically sort token pairs
- [ ] Prevent duplicate pool creation
- [ ] Validate supported fee tiers
- [ ] Validate tick spacing
- [ ] Verify stored pool WASM hash
- [ ] Verify constructor parameters
- [ ] Test registry consistency
- [ ] Test unauthorized admin calls

---

## 3. Pool / CLMM Security

### Swap Safety
- [ ] Validate swap amount and direction
- [ ] Enforce sqrt-price limits
- [ ] Prevent invalid tick traversal
- [ ] Verify liquidity availability
- [ ] Test zero-liquidity conditions
- [ ] Test extreme price movement
- [ ] Test high-slippage conditions
- [ ] Test rounding behavior
- [ ] Test fee calculation

### Liquidity Accounting
- [ ] Validate lower tick < upper tick
- [ ] Enforce tick-spacing rules
- [ ] Validate liquidity amount > 0
- [ ] Prevent unauthorized position modification
- [ ] Verify mint/burn accounting
- [ ] Test position ownership
- [ ] Test out-of-range positions
- [ ] Verify fee-growth accounting

### Fee Accounting
- [ ] Test global fee growth
- [ ] Test per-position fee accrual
- [ ] Test fee collection
- [ ] Prevent double collection
- [ ] Verify precision and rounding

---

## 4. Tick Math Security

Review `fixed_point`, `sqrt_price`, `liquidity`, `tick` and `tick_bitmap`.

- [ ] Test minimum and maximum supported ticks
- [ ] Test tick-to-price conversion
- [ ] Test price-to-tick conversion
- [ ] Test negative ticks
- [ ] Test boundary crossing
- [ ] Test bitmap search
- [ ] Test fixed-point rounding
- [ ] Test overflow/underflow behavior
- [ ] Add property/invariant tests

---

## 5. Router Security

- [ ] Validate token pair
- [ ] Validate fee tier
- [ ] Validate recipient
- [ ] Validate input/output amounts
- [ ] Enforce deadline if supported
- [ ] Enforce minimum output
- [ ] Enforce maximum input
- [ ] Use safe price-limit logic
- [ ] Verify returned pool belongs to configured Factory
- [ ] Reject missing pools
- [ ] Test exact-input swaps
- [ ] Test exact-output swaps

---

## 6. Position Manager Security

- [ ] Validate position ownership
- [ ] Prevent unauthorized decrease
- [ ] Prevent unauthorized collection
- [ ] Prevent unauthorized burn
- [ ] Ensure position IDs cannot collide
- [ ] Verify per-owner enumeration
- [ ] Prevent burn while liquidity remains
- [ ] Test multiple positions per wallet

---

## 7. Token Security

Current assets:

| Asset | Soroban Address |
| --- | --- |
| XLM | `CDLZFC3SYJYDZT7K67VZ75HPJVIEUVNIXF47ZG2FB2RMQQVU2HHGCYSC` |
| USDC | `CBIELTK6YBZJU5UP2WWQEUCYKLPU6AUNZ2BQ4WWFEIE3USCIHMXQDAMA` |

- [ ] Validate expected SAC addresses
- [ ] Never use a classic G-address for Soroban token calls
- [ ] Validate token-transfer authorization
- [ ] Handle decimals correctly
- [ ] Test insufficient balances
- [ ] Test trustline failures where applicable

---

## 8. Wallet Security

- [x] User blockchain actions are authorized through a wallet
- [ ] Never request wallet secret keys
- [ ] Validate connected network
- [ ] Validate public address
- [ ] Handle rejected signatures safely
- [ ] Handle disconnect/reconnect
- [ ] Re-check wallet before signing
- [ ] Show clear transaction details before authorization

---

## 9. Frontend Security

### Environment Variables
AstraX uses public `NEXT_PUBLIC_*` configuration for network URLs and contract addresses.

- [x] Contract addresses may be public
- [x] RPC/Horizon URLs may be public
- [ ] Never place private keys in `NEXT_PUBLIC_*`
- [ ] Never expose deployment secrets to the browser
- [ ] Maintain `.env.example`
- [ ] Validate required variables during build/startup

### Transaction UX
- [x] Pre-transaction review is included
- [x] Slippage validation has been improved
- [ ] Always display expected input/output
- [ ] Always display network
- [ ] Show transaction state
- [ ] Prevent duplicate submission
- [ ] Handle expired quotes

---

## 10. RPC / Network Security

- [ ] Validate network passphrase
- [ ] Validate Soroban RPC URL
- [ ] Validate Horizon URL
- [ ] Handle RPC timeout
- [ ] Handle stale state
- [ ] Retry reads carefully
- [ ] Never automatically repeat a financial write without checking whether the first submission succeeded

---

## 11. CI/CD Security

Current contract CI includes `cargo fmt --check`, `cargo test`, and WASM build. Frontend CI includes install, lint, typecheck, tests and build.

- [x] Contract CI exists
- [x] Frontend CI exists
- [ ] Add `cargo clippy`
- [ ] Add dependency audit
- [ ] Add npm vulnerability checks
- [ ] Add secret scanning
- [ ] Protect `main`
- [ ] Require passing CI before merge
- [ ] Restrict deployment secrets

---

## 12. Deployment Security

Current canonical Testnet addresses:

```text
Factory:          CDFY5UX77PQDP2QGNY4YGZVKK6FE6J2LSSVZFXTQSHRO2JIES7LSZGPE
Pool:             CCYBX2FOT5RWL6T2CQROAA3ZECYNNE3PSJ7WQXULU6AJOCCK6YHSTH32
Router:           CDLCGPUP7NW4B4SSFG5H4I75PKDGPUZDHOX5C6YICJY7RDJ7VP7BAT62
Position Manager: CC6IBQ7VNVK7CQYIZX47NJPDH5DL5ISQSA26BLBZXVMVEQ3QGUAZDREI
```

- [ ] Maintain one canonical deployment manifest
- [ ] Remove or mark stale addresses in legacy docs
- [ ] Verify frontend environment matches canonical addresses
- [ ] Verify deployed WASM hashes
- [ ] Record deployment transaction hashes
- [ ] Tag audited release commit before Mainnet

### Documentation warning
The repository's `contract.md` currently contains older deployment addresses while the root README lists newer canonical Testnet deployments.

Before final review:
- [ ] Update `contract.md` to current addresses, **or**
- [ ] Rename it as a historical/legacy deployment document

---

## 13. User Safety

- [ ] Clearly label Testnet
- [ ] Explain CLMM range risk
- [ ] Explain impermanent loss
- [ ] Explain out-of-range positions
- [ ] Explain slippage
- [ ] Explain Testnet assets have no real value
- [ ] Provide transaction-verification links

---

## 14. Pre-Mainnet Security Gate

- [ ] Complete comprehensive contract tests
- [ ] Add CLMM invariant/property testing
- [ ] Complete external audit or approved security review
- [ ] Fix all high/critical findings
- [ ] Verify canonical deployment configuration
- [ ] Review protocol administration
- [ ] Review fee controls
- [ ] Test production wallet flows
- [ ] Complete transaction monitoring
- [ ] Publish final Mainnet addresses
- [ ] Publish security-review proof

---

## 15. Recommended CLMM Invariants

```text
Total position liquidity must remain consistent with active pool liquidity.
A user must never collect the same accrued fee twice.
A position cannot be modified by an unauthorized wallet.
Pool price must stay inside supported mathematical bounds.
Swap execution must respect user-specified price/slippage limits.
Factory registry must resolve one canonical pool per token pair + fee tier.
Position IDs must remain unique.
Token accounting must remain consistent after mint → swap → collect → burn sequences.
```

---

## ✅ Security Status Summary

| Area | Current State |
| --- | --- |
| Modular Soroban architecture | ✅ Implemented |
| Contract testing pipeline | ✅ Present |
| Frontend CI | ✅ Present |
| Wallet authorization | ✅ Present |
| Slippage / transaction validation | ✅ Improved |
| Testnet deployment | ✅ Present |
| External audit | ⏳ Required before Mainnet |
| Advanced invariant/fuzz testing | 🔄 Recommended |

> AstraX should not describe this checklist as an audit. It is an internal security-readiness document.
