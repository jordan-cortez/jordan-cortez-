# FX Hedging Decision Memo: U.S. Solar Equipment Importer

**Created by:** Jordan Cortez  
**Updated by:** Jordan Cortez  
**Date Created:** 2026-04-04  
**Date Updated:** 2026-04-04  
**Version:** 1.0  
**LLM Used:** claude

---

## Executive Summary (≤150 words)

Our firm faces a material exposure in the EUR receivable market that creates significant downside risk to profitability. We expect to receive €4,500,000 in one year, exposing us to currency depreciation that could reduce USD proceeds substantially. Current spot and forward rates suggest hedging is economically defensible. This memo frames the exposure, quantifies the risk, and outlines three distinct hedge strategies for Stage 2 modeling. The objective is to determine which hedging approach—forwards, protective puts, or collars—best balances cost, certainty, and upside optionality for this solar equipment contract.

---

## Background & Objectives

**Firm:** U.S. Solar Equipment Importer  
**Exposure:** €4,500,000 receivable due in 12 months  
**Base Currency:** USD

Our firm manufactures and exports solar equipment to European distributors. A major contract, finalized in March 2026, entitles us to receive €4,500,000 upon delivery and acceptance in April 2027. At current spot rates (1.10 EURUSD), this represents approximately $4,950,000 in USD proceeds. However, exchange rate volatility creates uncertainty: a 5% EUR depreciation would reduce proceeds to $4,698,000 (a $252,000 loss). For a mid-sized equipment supplier, this magnitude of P&L swings material.

**Objectives:**
1. Quantify the downside risk from EUR depreciation over the 12-month period.
2. Evaluate three hedge families to lock in or protect USD proceeds.
3. Establish a decision framework for Stage 2 modeling and Stage 4 recommendation.

---

## Methods

**Hedging Strategies Evaluated:**

1. **Forward Contract**  
   - Lock in the 1-year forward rate (1.0875 EURUSD).  
   - *Pros:* Eliminates FX uncertainty; lowest transaction cost; no premium paid.  
   - *Cons:* Zero optionality if EUR strengthens; loses upside gains.

2. **Protective Put (Long EUR Put, Strike at Spot)**  
   - Buy a 1-year EUR put at strike ≈ 1.10 EURUSD; premium ≈ $0.015 per EUR.  
   - *Pros:* Downside protection; retains full upside if EUR appreciates; known cost.  
   - *Cons:* Premium reduces effective proceeds (€4,500,000 × $0.015 = $67,500 cost); higher than forward.

3. **Zero-Cost Collar (Long Put + Short Call)**  
   - Buy EUR put (strike ≈ 1.10); sell EUR call (strike ≈ 1.10).  
   - Put premium ≈ $0.015; call premium ≈ $0.018.  
   - *Pros:* Protected downside; lower net cost (call premium offsets put); suitable for balanced risk appetite.  
   - *Cons:* Caps upside at the call strike; complex execution.

**Analytical Approach:**
- Stage 2 will build an Excel model computing USD proceeds under each hedge across a range of EURUSD spot rates at maturity (1.00–1.20).
- Stage 3 will document the model structure and design improvements.
- Stage 4 will interpret results and recommend the optimal hedge based on firm risk tolerance and CFO guidance.

---

## Limitations & Next Steps

**Known Constraints:**
- Current USD and EUR interest rates assumed to remain stable over 12 months (in reality, rate forecasts should feed forward pricing).
- Option premiums derived from mid-market indicative quotes; actual dealer pricing may differ.
- No assumption of interim cash flow or early settlement needs.
- Assumes full EUR receivable (no partial default or credit risk adjustment).

**Next Steps:**

| Stage | Action |
|-------|--------|
| **Stage 2** | Build a working Excel model that computes total USD proceeds (or losses) under each hedge strategy across spot rate scenarios. Include break-even analysis and sensitivity tables. |
| **Stage 3** | Document the model architecture, formula logic, and data sources. Design an improved version specification suitable for AI reconstruction. |
| **Stage 4** | Run model results against CFO risk appetite and cost thresholds; write a structured AI prompt; recommend the hedge strategy and present final case. |

---

## References

- FIN-321 Project Scenarios (Scenario 1 – U.S. Solar Equipment Importer)
- Current EURUSD spot rate and 1-year forward: 1.0875 (per scenario)
- Option premium data: EUR put $0.015 per contract, call $0.018 (per scenario)
- Project README: Multi-Stage FX Exposure and Hedging Strategies workflow

---

**Next Deliverable:** Stage 2 Excel Model Build  
**Target Completion:** Per course schedule
