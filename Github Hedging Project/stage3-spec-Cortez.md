# FX Hedge Model — Quantitative Specification
**Stage 3 | U.S. Solar Equipment Importer**
**Prepared by:** Jordan Cortez
**Date:** April 2026
**Version:** 1.0

---

## 1. Problem Statement

A U.S.-based solar equipment exporter has contracted to receive **€4,500,000** from a European distributor upon delivery and acceptance of goods in **April 2027** (12-month horizon). The firm's functional currency is USD. At the inception spot rate of **1.1000 USD/EUR**, the receivable represents approximately **$4,950,000** in USD proceeds.

The core risk is EUR depreciation over the next 12 months. A 5% adverse move (EUR/USD falling to 1.045) would reduce USD proceeds to approximately **$4,702,500**—a **$247,500 shortfall** relative to the unhedged spot conversion. For a mid-sized equipment supplier operating on fixed-price contracts, this magnitude of FX-driven P&L volatility is material and warrants a formal hedging decision.

The objective of this model is to quantify USD proceeds under three hedge strategies—forward contract, protective put, and zero-cost collar—across a range of spot rate outcomes at maturity, and to identify the structure that best balances cost, certainty, and upside optionality.

---

## 2. Inputs (Known Variables)

All variables carry standardized named ranges for model reproducibility.

| Named Range  | Description                        | Value      | Unit         | Source                        |
|--------------|------------------------------------|------------|--------------|-------------------------------|
| `FC_AMT`     | EUR receivable                     | 4,500,000  | EUR          | Contract (March 2026)         |
| `S0_in`      | Spot rate at inception             | 1.1000     | USD per EUR  | FIN-321 scenario              |
| `F0_in`      | 1-year forward rate                | 1.0875     | USD per EUR  | FIN-321 scenario              |
| `R_USD`      | USD interest rate (p.a.)           | 5.00%      | Annual %     | FIN-321 scenario              |
| `R_FC`       | EUR interest rate (p.a.)           | 3.00%      | Annual %     | FIN-321 scenario              |
| `T_DAYS`     | Days to settlement                 | 360        | Days         | Contract terms                |
| `K_PUT`      | Put option strike                  | 1.1000     | USD per EUR  | At-the-money-spot             |
| `K_CALL`     | Call option strike                 | 1.1000     | USD per EUR  | At-the-money-spot             |
| `PREM_PUT`   | Put premium per unit of EUR        | 0.0150     | USD per EUR  | Indicative mid-market quote   |
| `PREM_CALL`  | Call premium per unit of EUR       | 0.0180     | USD per EUR  | Indicative mid-market quote   |

---

## 3. Assumptions & Constraints

- **Rate basis:** Annual simple interest, 360-day convention (ACT/360) applied uniformly across all hedges. No compounding.
- **Transaction costs:** No bid-ask spreads, brokerage fees, or dealer margins modeled. All rates are mid-market.
- **Covered-interest parity (CIP):** The forward rate is taken as given from the scenario (1.0875) rather than derived from CIP. A CIP check (1.10 × 1.05/1.03 = 1.1214) reveals a deviation from the theoretical forward, likely due to the use of simple rather than compound interest conventions. A residual parity gap of approximately **$152,367** exists between the forward and money market hedge results, consistent with this convention mismatch.
- **Option premiums:** Premiums are fixed, indicative quotes at inception. No dynamic re-pricing or delta-hedging is modeled.
- **Full settlement:** The entire €4,500,000 receivable is assumed to settle on the due date. No partial payments, counterparty default, or early termination is modeled.
- **Interest rate stability:** USD and EUR rates are assumed constant over the 12-month period.
- **Collar structure:** The collar uses identical strikes for the put (1.1000) and call (1.1000). Because PREM_CALL > PREM_PUT, the structure generates a net premium credit of $0.003/EUR ($13,500 total), making it technically a net-credit collar rather than a true zero-cost collar.

---

## 4. Calculation Flow

### 4.1 Forward Hedge

1. Multiply `FC_AMT` by `F0_in` to obtain locked-in USD proceeds.
   - Result: **$4,893,750** — fixed regardless of S_T.

### 4.2 Money Market Hedge

1. **Borrow** the present value of the EUR receivable: divide `FC_AMT` by `(1 + R_FC × T_DAYS/360)`.
   - Borrowing amount: €4,368,932
2. **Convert** the borrowed EUR to USD at the spot rate: multiply by `S0_in`.
   - USD proceeds at spot: $4,805,825
3. **Invest** USD proceeds at the USD rate: multiply by `(1 + R_USD × T_DAYS/360)`.
   - Locked-in result: **$5,046,117**
4. **Parity check:** Subtract the forward hedge result from the MM result. A value of approximately $0 confirms CIP holds; the observed residual of –$152,367 reflects the simple-interest convention mismatch noted in Section 3.

### 4.3 Protective Put Hedge

1. Compute total put premium paid: `PREM_PUT × FC_AMT` = –$67,500.
2. Compute future value of premium: multiply by `(1 + R_USD)` = –$70,875.
3. Compute floor proceeds: `K_PUT × FC_AMT + FV(premium)` = **$4,879,125**.
   - Below K_PUT: proceeds equal the floor (put exercised, upside foregone).
   - Above K_PUT: proceeds equal `S_T × FC_AMT – FV(premium)` (put expires, upside captured net of cost).

### 4.4 Zero-Cost Collar

1. Put premium paid: `–PREM_PUT × FC_AMT` = –$67,500.
2. Call premium received: `+PREM_CALL × FC_AMT` = +$81,000.
3. Net premium: –$67,500 + $81,000 = **+$13,500** (net credit).
4. Future value of net premium: `$13,500 × (1 + R_USD)` = **+$14,175**.
5. Floor proceeds: `K_PUT × FC_AMT + FV(net premium)` = **$4,964,175**.
6. Cap proceeds: `K_CALL × FC_AMT + FV(net premium)` = **$4,964,175**.
   - Note: Because K_PUT = K_CALL = 1.10, floor and cap are equal in this model, implying no rate range between the two strikes. In a properly structured collar, K_CALL > K_PUT.

---

## 5. Outputs

The model produces the following named results and tables:

**Summary Output Table**

| Output                              | Value        |
|-------------------------------------|--------------|
| Forward Hedge – Locked-In Proceeds  | $4,893,750   |
| Money Market Hedge – Locked-In      | $5,046,117   |
| Parity Check (Forward – MM)         | –$152,367    |
| Put Hedge – Floor Proceeds          | $4,879,125   |
| Put Hedge – Net Premium Cost (FV)   | –$70,875     |
| Collar – Floor Proceeds             | $4,964,175   |
| Collar – Cap Proceeds               | $4,964,175   |
| Collar – Net Premium (credit)       | +$13,500     |
| Unhedged at S0                      | $4,950,000   |

**Sensitivity Table: USD Proceeds by Strategy vs. S_T**
Eleven exchange rate scenarios from S_T = 1.045 to S_T = 1.155 (S0 ± 5%, in 1% steps), showing proceeds under: No Hedge, Forward, Put Hedge, and Collar. This table is the primary analytical output.

**Sensitivity Chart:** Line chart plotting USD proceeds (y-axis) against S_T (x-axis) for all four strategies, illustrating crossover points, floor levels, and upside capture differences.

---

## 6. Model Review — What Worked & What to Improve

**What Worked:**
- Named ranges (`FC_AMT`, `S0_in`, etc.) are consistently applied across all sections, enabling clean auditability.
- The sensitivity table correctly captures option payoff asymmetry: the put hedge tracks the unhedged outcome above the strike and holds the floor below it.
- The collar net premium calculation is arithmetically correct, and the credit nature of the structure is properly disclosed in the notes.

**What Should Be Improved:**

| Issue | Improvement |
|-------|-------------|
| Forward rate not derived from CIP | Compute `F0` as `S0 × (1 + R_USD) / (1 + R_FC)` to ensure internal consistency; flag deviations from scenario value |
| Identical put/call strikes | Collar should use K_PUT < K_CALL (e.g., 1.08 put / 1.12 call) to create a meaningful rate band and true optionality range |
| Simple interest convention | Adopt compound interest (`(1+r)^(T/360)`) throughout for greater precision; or clearly flag the simple-interest approximation |
| Money market hedge parity gap | Either reconcile the $152,367 gap or remove the MM hedge from the primary comparison if the convention mismatch is structural |
| Sensitivity step size | 1% steps over ±5% yields only 11 data points; 0.5% steps (21 points) would produce smoother chart curves |
| No break-even analysis | Add a row/column identifying the S_T at which each hedge outperforms the unhedged position |
| No weighted outcome | Consider adding an expected USD proceeds row using a simple probability weighting across S_T scenarios |

---

## 7. Sensitivity Plan

The sensitivity table spans **S_T = 1.045 to S_T = 1.155** — a ±5% band around the inception spot of 1.10 — in **1% increments**, producing 11 scenarios. Each scenario computes USD proceeds under all four strategies (No Hedge, Forward, Put, Collar).

The chart communicates three key relationships: (1) the forward hedge's flat line showing complete rate-lock, (2) the put hedge's kinked payoff (floor below strike, slope above), and (3) the collar's bounded range. The most analytically useful comparisons are Forward vs. No Hedge (certainty cost), and Put vs. Collar (premium cost vs. upside retention).

In the improved model, the sensitivity range should extend to ±10% (S_T = 0.99 to 1.21) to stress-test tail scenarios, and the step size should be reduced to 0.5% for chart smoothness.

---

## 8. Limitations & Next Steps

**Excluded from this model:**
- Dynamic or rolling hedges; only static, inception-date hedges are evaluated.
- Counterparty credit risk and margin/collateral requirements.
- ASC 815 hedge accounting treatment and P&L designation.
- Partial settlement scenarios or contract renegotiation.
- Volatility surface inputs for option pricing; premiums are indicative mid-market quotes only.

**How This Spec Feeds Stage 4:**

This document serves as the primary input to the Stage 4 AI prompt. The named ranges, calculation sequences, and improvement notes in Sections 2–6 provide sufficient precision for an AI assistant to reconstruct the model with all identified corrections applied. Section 6 specifically identifies which design changes to implement in the improved version, so the Stage 4 output reflects an enhanced model rather than a replica of the Stage 2 prototype. The Stage 4 deliverable will apply this spec to generate a final hedge recommendation against CFO risk appetite and cost thresholds.
