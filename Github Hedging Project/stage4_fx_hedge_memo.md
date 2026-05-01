# FX Hedging Decision Memo — Stage 4
**U.S. Solar Equipment Importer**
Prepared by: Jordan Cortez | Date: April 2026 | Version: 1.0

---

## A. Exposure Summary

Our firm, a U.S.-based solar equipment exporter, has contracted to receive **€4,500,000** from a European distributor upon delivery and acceptance of goods in **April 2027** — a 12-month horizon. The firm's functional currency is USD.

At the inception spot rate of **1.1000 USD/EUR**, the receivable represents approximately **$4,950,000** in USD proceeds. The core risk is **EUR depreciation**: if the EUR/USD rate falls by 5% to 1.045 at maturity, USD proceeds drop to approximately $4,702,500 — a **$247,500 shortfall** relative to the unhedged spot conversion. For a mid-sized equipment supplier operating on fixed-price contracts, this magnitude of FX-driven P&L volatility is material.

This memo summarizes the Stage 2 model results, interprets hedge behavior across rate scenarios, and recommends the optimal hedging strategy.

---

## B. Summary of Hedge Outcomes

| Strategy | Locked-In / Floor Proceeds | Key Trade-Off |
|---|---|---|
| **No Hedge** | Variable: $4,500,000–$5,400,000 (S_T range 1.00–1.20) | Full exposure; maximum upside and downside |
| **Forward Contract** | $4,893,750 (fixed) | Certainty; zero upside optionality |
| **Money Market Hedge** | $5,046,117 (locked) | Synthetic forward; requires borrowing EUR and investing USD; liquidity impact |
| **Protective Put** | $4,879,125 floor | Downside protection + upside retained; $70,875 premium cost (FV) |
| **Zero-Cost Collar** | $4,964,175 floor / cap | Net credit of $13,500; floor above forward; upside capped at call strike |

**Forward Contract:** Locks in $4,893,750 with complete certainty. No premium paid. However, if EUR appreciates — say to 1.155 — the unhedged firm would receive $5,197,500, while the forward firm is still locked at $4,893,750, a $303,750 opportunity cost. Appropriate for firms that prioritize budget certainty above all else.

**Money Market Hedge:** Achieves $5,046,117 by borrowing the PV of the EUR receivable today, converting at spot, and investing USD at 5%. This produces a higher result than the forward due to the simple-interest convention mismatch noted in Stage 3 (a $152,367 parity gap). In a fully CIP-consistent model, these two strategies converge. This approach also requires upfront EUR borrowing capacity, which may constrain liquidity.

**Protective Put:** Buying a EUR put at strike 1.1000 for $0.015/EUR ($67,500 total, or $70,875 FV) establishes a floor of $4,879,125 while retaining full upside if EUR appreciates. The cost is real and reduces effective proceeds at the floor, but the structure is straightforward and transparent.

**Zero-Cost Collar:** Buying the EUR put (strike 1.10, premium $0.015/EUR) and simultaneously selling a EUR call (strike 1.10, premium $0.018/EUR) generates a **net premium credit of $13,500** ($14,175 FV). This raises the effective floor to **$4,964,175** — higher than both the forward and the put hedge floor. Because K_PUT = K_CALL in this model, the floor and cap are identical; in a properly structured collar with K_PUT < K_CALL (e.g., 1.08 put / 1.12 call), the firm would retain a meaningful upside band between the two strikes.

---

## C. Sensitivity Interpretation

The sensitivity table spans S_T = 1.045 to S_T = 1.155 (±5% around the 1.10 inception spot) in 1% increments.

**EUR Depreciation Scenarios (S_T < 1.10):**

In a depreciation environment, the forward hedge and collar provide the strongest protection. At S_T = 1.045:
- No Hedge: ~$4,702,500
- Forward: $4,893,750 (outperforms by ~$191,250)
- Put Hedge: $4,879,125 floor (outperforms by ~$176,625)
- Collar: $4,964,175 floor (outperforms by ~$261,675)

The collar's net credit structure means its floor **exceeds** both the forward and put hedge at every depreciation scenario — a notable advantage with zero net premium outlay.

**EUR Appreciation Scenarios (S_T > 1.10):**

In an appreciation environment, the no-hedge position captures full upside. At S_T = 1.155:
- No Hedge: ~$5,197,500
- Forward: $4,893,750 (locked, opportunity cost of ~$303,750)
- Put Hedge: ~$5,126,625 (S_T × €4,500,000 – $70,875 FV premium) — tracks upside net of cost
- Collar: $4,964,175 (capped; because K_CALL = K_PUT in this model, upside is fully surrendered above 1.10)

The put hedge is the only structure that captures meaningful upside while maintaining downside protection — at a $70,875 cost. The collar trades that upside for a premium credit and a higher floor.

**Key Crossover:** The forward hedge outperforms the unhedged position whenever S_T < 1.0875 (the forward rate). Below that threshold, locking in the forward was the right call. Above it, hedging had an opportunity cost.

---

## D. Strategic Recommendation

**Recommended Strategy: Zero-Cost Collar**

The collar is the optimal structure for this firm given the following:

1. **Net premium credit of $13,500** — rather than paying to hedge, the firm receives a credit, improving effective proceeds at every scenario below the call strike.
2. **Floor of $4,964,175** — the highest floor among all strategies, exceeding the forward ($4,893,750) and put ($4,879,125) by $70,425 and $85,050 respectively.
3. **Cost efficiency** — for a mid-sized supplier on fixed-price contracts, avoiding a $67,500–$70,875 option premium outlay materially improves working capital.
4. **Downside elimination** — the put leg ensures the firm never receives less than $4,964,175 regardless of EUR depreciation severity.

**Caveat:** In this model, K_PUT = K_CALL = 1.10, which eliminates any upside band. In the improved model (Stage 3 recommendation), the collar should use K_PUT = 1.08 and K_CALL = 1.12, creating a $180,000 upside participation band while maintaining downside protection. That structure would preserve the net credit benefit while allowing EUR appreciation gains up to the call strike.

If the CFO's primary concern is **absolute budget certainty** with no tolerance for any variability, the forward contract remains a suitable alternative. However, for a firm willing to accept a defined upside cap in exchange for a higher floor and zero premium cost, the collar is strictly superior.

---

## E. Executive Justification

**Cash Flow Stability:** The collar establishes a hard floor of $4,964,175, ensuring the firm can meet its USD-denominated operating commitments regardless of EUR movement. This floor exceeds the forward-locked amount, providing greater budget confidence.

**Budget Certainty:** While the collar does not lock in a single fixed number (unlike the forward), the floor is known at inception. The CFO can plan around a worst-case USD receipt of $4,964,175 with confidence.

**Liquidity Impact:** Unlike the money market hedge, the collar requires no upfront borrowing or balance sheet adjustment. The net premium credit of $13,500 is a modest positive cash inflow, not an outflow. This preserves working capital and avoids the EUR borrowing facility required by the money market strategy.

**Optionality Value:** In the improved collar design (split strikes), the firm retains upside participation up to the call strike. Even in the current equal-strike model, the net credit structure means the firm is not paying for protection — it is being compensated for capping upside it may not need given current EUR rate forecasts.

**Premium Costs:** The protective put carries a $70,875 FV premium cost — a real drag on proceeds at every scenario. The collar eliminates this cost entirely and converts it to a net inflow, making it strictly preferable from a cost perspective when downside protection is the primary objective.

**Accounting Implications (Optional):** Under ASC 815, both the forward and the collar qualify for cash flow hedge accounting if properly designated and documented at inception. Hedge-effective gains and losses would be recorded in Other Comprehensive Income (OCI) and reclassified to earnings when the hedged transaction affects P&L (April 2027). The collar's net premium credit would be amortized over the hedge term. Proper documentation — including risk management objective, hedge relationship, and effectiveness testing — should be prepared by the accounting team prior to execution.

---

## F. Structured AI Prompt

### Appendix: AI Prompt for FX Hedging Excel Model Reconstruction

---

```
# GOAL
Build a complete, professional Excel workbook modeling four FX hedging strategies
for a EUR receivable. The model must be fully formula-driven, use named ranges
throughout, and produce a sensitivity table and chart comparing all strategies
across a range of maturity spot rates.

# INPUT VARIABLES
Use the following named ranges in an Excel Input section. All values are fixed
at inception and must not be hardcoded in formulas — reference named ranges only.

Named Range    | Description                        | Value
---------------|------------------------------------|--------------
FC_AMT         | EUR receivable amount              | 4,500,000
S0_in          | Spot rate at inception (USD/EUR)   | 1.1000
F0_in          | 1-year forward rate (USD/EUR)      | 1.0875
R_USD          | USD interest rate (annual)         | 0.05
R_FC           | EUR interest rate (annual)         | 0.03
T_DAYS         | Days to settlement                 | 360
K_PUT          | Put option strike (USD/EUR)        | 1.08
K_CALL         | Call option strike (USD/EUR)       | 1.12
PREM_PUT       | Put premium per EUR                | 0.0150
PREM_CALL      | Call premium per EUR               | 0.0180

Note: K_PUT and K_CALL use split strikes (1.08 / 1.12) for a properly
structured collar with a meaningful upside band.

# COLOR CODING
Apply the following cell background colors consistently:
- Yellow  (#FFFF00): All input cells (named range values)
- Blue    (#BDD7EE): Assumption cells (interest rates, day count)
- Green   (#E2EFDA): Formula output cells
- Gray    (#D9D9D9): Section headers and labels

# MODEL LOGIC

## Section 1 — Input Table
List all named ranges with descriptions, values, and units. Yellow background on value cells.

## Section 2 — Forward Hedge
Formula: = F0_in * FC_AMT
Result: Fixed USD proceeds regardless of S_T.
Label: "Forward Hedge — Locked-In Proceeds"

## Section 3 — Money Market Hedge (3-Step)
Step 1 — Borrow EUR PV:    = FC_AMT / (1 + R_FC * T_DAYS/360)
Step 2 — Convert to USD:   = Step1 * S0_in
Step 3 — Invest USD:       = Step2 * (1 + R_USD * T_DAYS/360)
Include a parity check row: = Forward_Result - MM_Result
(Expected: ~0 under CIP; flag deviations with a note)

## Section 4 — Protective Put Hedge
Put premium total:        = PREM_PUT * FC_AMT           [negative, cash outflow]
FV of premium:            = Premium_Total * (1 + R_USD * T_DAYS/360)
Floor proceeds:           = K_PUT * FC_AMT + FV_Premium
For S_T > K_PUT:          = S_T * FC_AMT + FV_Premium   [put expires, upside captured net of cost]
For S_T <= K_PUT:         = Floor_Proceeds               [put exercised]

## Section 5 — Zero-Cost Collar
Put premium paid:         = -PREM_PUT * FC_AMT
Call premium received:    = +PREM_CALL * FC_AMT
Net premium:              = Call_Prem + Put_Prem         [positive = net credit]
FV of net premium:        = Net_Premium * (1 + R_USD * T_DAYS/360)
Floor proceeds:           = K_PUT * FC_AMT + FV_Net_Premium
Cap proceeds:             = K_CALL * FC_AMT + FV_Net_Premium
For S_T < K_PUT:          = Floor_Proceeds               [put exercised]
For K_PUT <= S_T <= K_CALL: = S_T * FC_AMT + FV_Net_Premium [both options expire]
For S_T > K_CALL:         = Cap_Proceeds                 [call assigned, upside capped]

## Section 6 — Sensitivity Table
Rows: S_T from 1.00 to 1.20 in 0.01 increments (21 rows)
Columns: No Hedge | Forward | Put Hedge | Collar
Formulas must reference named ranges only — no hardcoded rates.
Add a "Break-Even vs. No Hedge" row identifying the S_T at which each
hedged strategy produces equal proceeds to the unhedged position.

# VERIFICATION CHECKS
Add a verification section with the following checks:
1. Forward vs. MM Parity: = ABS(Forward_Result - MM_Result) < 10000
   Flag "CHECK PASSED" or "REVIEW — CIP DEVIATION" in a labeled cell.
2. Collar Net Premium Sign: = IF(Net_Premium > 0, "Net Credit (correct)", "Net Debit — review strikes")
3. Put Floor Confirmation: = IF(Put_Floor < Forward_Result, "Put floor below forward (expected)", "Review")

# SENSITIVITY CHART
Create a line chart from the sensitivity table with:
- X-axis: S_T (1.00 to 1.20)
- Y-axis: USD Proceeds ($4,400,000 to $5,500,000)
- Four series: No Hedge, Forward, Put Hedge, Collar
- Color each series distinctly; label series in legend
- Add a vertical reference line at S_T = 1.10 (inception spot)
- Add a horizontal reference line at the forward locked-in level ($4,893,750)
- Title: "USD Proceeds by Hedge Strategy vs. EUR/USD at Maturity"

# EXPORT
Save the workbook as: FX_Hedge_Model_Improved_v2.xlsx
Sheet tabs: Inputs | Forward_MM | Options | Sensitivity | Chart | Verification
Protect formula cells; leave input cells unlocked.
```

---

## Extra Credit: Areas for Further Study

### 1. AI Skills & Automation

AI tools such as Claude Code Interpreter or Python-enabled agents could substantially enhance this workflow by pulling **live market data** — spot rates, forward points, and implied volatility surfaces — directly from data providers such as Bloomberg or Refinitiv and feeding them into the model at runtime. Rather than relying on indicative mid-market quotes fixed at inception, an AI-enabled model could reprice option premiums dynamically using Black-Scholes or Garman-Kohlhagen inputs, update the sensitivity table automatically as rates move, and alert the treasury team when the EUR/USD rate crosses predefined thresholds. Furthermore, **Monte Carlo simulation** — feasible with a few hundred lines of Python — would replace the static 21-scenario sensitivity table with a probability distribution of USD outcomes across thousands of simulated rate paths, giving the CFO a more rigorous view of tail risk than the ±5% deterministic band can provide. Claude Skills could be deployed to regenerate the entire model on a scheduled basis (weekly or monthly), turning a one-time analysis into a continuously maintained risk dashboard.

### 2. Multi-File Reasoning & GitHub Version Control

The three-stage structure of this project — Stage 1 memo, Stage 3 specification, Stage 4 prompt — maps directly to the benefits of **version-controlled, multi-file AI reasoning**. By committing each stage artifact to a GitHub repository, an AI assistant given access to the repo can read the spec, the model, and the prompt together, identify inconsistencies (such as the convention mismatch noted in the Stage 3 parity check), and propose targeted corrections without starting from scratch. GitHub's commit history creates an **auditable trail**: every assumption change, model revision, and prompt update is timestamped and attributable, satisfying the documentation requirements of both internal governance and external audit. For hedge accounting purposes under ASC 815, this version-controlled repository could serve as contemporaneous documentation of the hedging objective, risk management strategy, and hedge relationship — evidence that auditors and regulators can inspect independently. Branching workflows also allow the team to maintain a production model (locked) and an experimental branch (in-progress improvements) simultaneously, which mirrors best practices in software engineering and increasingly in modern finance teams.

### 3. Accounting & Audit Integration

This project's analytical outputs connect directly to **ASC 815 cash flow hedge accounting** requirements. For the collar to qualify for hedge accounting, the firm must document at inception: the hedging instrument (the collar), the hedged item (the EUR receivable), the nature of the risk being hedged (EUR/USD exchange rate risk), and the method for assessing hedge effectiveness. Under the simplified dollar-offset or regression methods, the firm must demonstrate that the hedge is highly effective (80–125% offset ratio) on a prospective and retrospective basis. The Stage 2 sensitivity model is directly useful here: the proceeds table quantifies the hedge's offset of unhedged exposure across rate scenarios, forming the basis for effectiveness documentation. A GitHub-hosted model that is version-controlled and timestamped strengthens the audit trail by proving that effectiveness testing was performed contemporaneously, not reconstructed after the fact. AI tools could automate the quarterly effectiveness test by re-running the sensitivity model with updated market rates and producing a standardized effectiveness report suitable for submission to auditors — reducing manual effort and the risk of documentation gaps that can disqualify hedge accounting treatment.

---

*End of Stage 4 Deliverable — FX Hedging Decision Memo*
*Prepared by: Jordan Cortez | FIN-321 | April 2026*
