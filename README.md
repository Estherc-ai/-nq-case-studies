[README (1).md](https://github.com/user-attachments/files/29560999/README.1.md)
# NQ Futures — Pre-Market Structural Analysis
### Institutional GEX / Options-Flow Research Portfolio · VXN Skew-Adjusted Multi-SD Engine

[![Cases](https://img.shields.io/badge/Case%20Studies-11%20Published-brightgreen)](https://estherc-ai.github.io/-nq-case-studies/)
[![Instrument](https://img.shields.io/badge/Instrument-NQ%20%2F%20MNQ%20Futures-blue)](https://estherc-ai.github.io/-nq-case-studies/)
[![Window](https://img.shields.io/badge/Valid%20Window-9%3A30--11%3A30%20AM%20NY-orange)](https://estherc-ai.github.io/-nq-case-studies/)
[![Engine](https://img.shields.io/badge/Engine-VXN%20Skew--Adjusted%20Multi--SD-purple)](https://estherc-ai.github.io/-nq-case-studies/)

> **Live portfolio:** [estherc-ai.github.io/-nq-case-studies](https://estherc-ai.github.io/-nq-case-studies/)

---

## Overview

This repository documents a systematic pre-market analytical framework applied to NQ/MNQ futures during the RTH morning session (9:30–11:30 AM New York Time). Every structural level, volatility boundary, and regime classification is derived from options market data collected before the open — prior to any RTH price action.

The framework integrates three analytical layers:

- **Options Gamma Exposure (GEX):** Vol Trigger (ZG), Call Wall, Put Wall, and Max Pain gravitational levels derived from NDX option open interest
- **NDX Implied Volatility Term Structure:** Blended 0DTE/1DTE/7DTE IV inputs producing daily standard deviation bands anchored to three structural reference points
- **VXN Skew-Adjusted Multi-SD Engine:** CBOE NASDAQ 100 Volatility Index modeled with signed 0DTE skew to produce asymmetric upside and downside volatility boundaries

All case studies are produced exclusively from pre-market data. Afternoon skew, wall levels, and Max Pain may differ materially due to intraday time decay and options flow.

---

## Instruments

| Instrument | Ticker | Role |
|---|---|---|
| NASDAQ 100 Volatility Index | CBOE:VXN | All volatility calculations · skew-adjusted multi-SD engine |
| Micro NQ Futures | CME:MNQ | Price levels · SD bands · condition classification |
| NDX Options Chain | CBOE:NDX | GEX levels · Max Pain · skew inputs |

> **Note:** VIX (S&P 500 volatility) is explicitly excluded. VXN is the correct volatility instrument for NQ/NDX analysis — it derives from the same option chain as the underlying index.

---

## Core Methodology

### Step 1 — IV Blend and Daily Scaler

Three implied volatility inputs are collected from the NDX options smile chart at 9:00–9:15 AM NY, selecting PM-settled contracts only:

```
σ_blend = (σ_0DTE × 0.50) + (σ_1DTE × 0.30) + (σ_7DTE × 0.20)
σ_daily = σ_blend ÷ √252
```

The blended volatility weights the front-end of the term structure (0DTE at 50%) to capture intraday realized volatility expectations while incorporating the 1DTE and 7DTE inputs to stabilize against single-expiry distortions.

### Step 2 — VXN Base Step

```
base_step = A × σ_daily
```

Where `A` is the VXN previous day official close (4:00 PM ET). On elevated-risk sessions the 9:15 AM spot may be substituted. The base step represents one standard deviation of expected VXN movement expressed in VXN index points.

### Step 3 — Asymmetric Skew Multipliers

The 0DTE skew is collected as a **signed** value from the NDX options smile chart:

```
upside_mult   = 1 − SK
downside_mult = 1 + SK
```

**Positive SK** (calls expensive, puts hollowed out) compresses the upside multiplier and stretches the downside — reflecting structurally unsupported VXN downside and NQ upside runaway risk.

**Negative SK** (standard equity skew — puts expensive) stretches the upside multiplier and compresses the downside — consistent with the traditional "fear is unbounded" VXN behavior.

### Step 4 — Six Daily Volatility Boundaries

```
+3σ = A + (base_step × 3 × upside_mult)    ← Extreme Panic Peak
+2σ = A + (base_step × 2 × upside_mult)    ← Standard Volatility Ceiling
+1σ = A + (base_step × 1 × upside_mult)    ← Normal Resistance
 0σ = A                                     ← Baseline Anchor
−1σ = A − (base_step × 1 × downside_mult)  ← Normal Support
−2σ = A − (base_step × 2 × downside_mult)  ← Skew-Adjusted Floor
−3σ = A − (base_step × 3 × downside_mult)  ← Extreme Vacuum Floor
```

---

## SK Tier Classification

| Tier | \|SK\| Range | Structural Meaning |
|---|---|---|
| Baseline / Normal | 0.01 – 0.09 | Low distortion · multipliers near 1.0 · symmetric behavior |
| Elevated | 0.10 – 0.19 | Meaningful asymmetry · early floor/ceiling fragility |
| Extreme / Vacuum State | 0.20 – 0.30+ | Severe asymmetry · structurally unsupported side |

---

## Regime Matrix

VXN absolute level and SK tier combine to determine the operative regime each session:

| | Normal SK | Elevated SK | Extreme SK (+) |
|---|---|---|---|
| **VXN HIGH (≥ 20)** | Standard symmetric behavior | Floor softening · monitor | **VACUUM DROP RISK** — fragile floor, NQ runs unhindered |
| **VXN LOW (< 20)** | Calm · low edge | Floor testing | **MM DEFENDS FLOOR** — pinned, no vacuum |

**HIGH VXN + Extreme positive SK:** elevated fear baseline already priced, but put-side support is hollowed out. If a directional trigger fires (NQ gaps above Call Wall, gamma desert opens), VXN vacuum-drops with no structural floor defense and NQ advances unhindered.

**LOW VXN + Extreme positive SK:** market makers are near minimum premium and need protection against a volatility expansion surprise. They defend the low VXN floor aggressively — expect pinning and chop rather than a clean directional move.

---

## NQ Standard Deviation Bands

Three independent SD band sets are calculated daily, each anchored to a different structural reference:

```
SD move        = anchor × σ_daily
1-SD upper     = anchor + SD move
1-SD lower     = anchor − SD move
```

| Anchor | Base | Purpose |
|---|---|---|
| ZG pivot | GEX Vol Trigger level | Options structure reference · WHY price stops |
| Asian NQ open ★ | First candle 18:00 NY | Session origin · draw bands on chart |
| RTH open | 9:30 AM first candle | Direction confirmation after open |

**Convergence rule:** when Asian 1-SD lower + ZG pivot + previous session low all fall within 100 points, this constitutes structural inevitability — the highest confidence floor of the session.

**1-SD completion rule (empirical):** the 1-SD band tends to be fully traveled within the session. If the relevant band has not been reached by RTH open, the day's statistical work is not done — expect continued travel toward the unfilled level before assuming exhaustion or reversal.

---

## Condition Classification

| ZG Distance | Condition | Bias |
|---|---|---|
| > +1.5% above ZG | C1 / C1B — Stratospheric | Short |
| +0.5% to +1.5% | C6 / C7 — Moderate gap | Context-dependent |
| ±0.2% | C2 — Pinned at ZG | Neutral |
| Below ZG | C3 — Negative gamma | Watch for C7 mutation |

The ZG distance is the **primary** condition classifier. It determines whether market makers retain gamma control near spot (low ZG distance) or whether price has moved into a gamma desert with no structural overhead resistance (high ZG distance). This distinction is more important than any single wall level.

---

## Triple Confirmation Signal

The highest-confidence entry requires all three simultaneously:

1. NQ body close held at GEX floor (ZG / Max Pain cluster)
2. NQ at Asian 1-SD lower (ideally matching previous session low)
3. VXN body close held inside +2σ zone (for C1B short sessions)

**Signal hierarchy:** GEX leads. NQ body close at GEX floor is the primary entry signal. VXN confirmation follows. Never reverse this order.

---

## Worked Example — June 30, 2026 (C1 Vacuum Drop)

```
Inputs:
  A = 29.37 · σ_0DTE = 0.26 · σ_1DTE = 0.27 · σ_7DTE = 0.23 · SK = +0.260

Calculation:
  σ_blend   = (0.26×0.50) + (0.27×0.30) + (0.23×0.20) = 0.2570
  σ_daily   = 0.2570 ÷ √252                             = 0.016189
  base_step = 29.37 × 0.016189                          = 0.4755
  upside_mult   = 1 − 0.260 = 0.740
  downside_mult = 1 + 0.260 = 1.260

VXN Boundaries:
  +3σ : 29.37 + (0.4755 × 3 × 0.740) = 30.43
  +2σ : 29.37 + (0.4755 × 2 × 0.740) = 30.07
  +1σ : 29.37 + (0.4755 × 1 × 0.740) = 29.72
   0σ : 29.37
  −1σ : 29.37 − (0.4755 × 1 × 1.260) = 28.77
  −2σ : 29.37 − (0.4755 × 2 × 1.260) = 28.17
  −3σ : 29.37 − (0.4755 × 3 × 1.260) = 27.57

Classification:
  VXN level : HIGH (29.37 ≥ 20)
  SK tier   : Extreme / Vacuum State (+0.260)
  Regime    : VACUUM DROP RISK

Session result:
  RTH open      : 30,029.50 — at Call Wall (30,030), +1.89% above ZG
  VXN cascade   : −1σ (28.77) → −2σ (28.17) → −3σ (27.57) all cleared
  NQ behavior   : advanced to 30,582 — Asian 1-SD upper (30,491) cleared
  Live tail     : VXN extended to 27.23–27.24 past modeled −3σ (27.57)
  Validation    : all four modeled levels confirmed on live chart ✅
```

---

## Case Study Index

| Date | Condition | Key Feature | Result |
|---|---|---|---|
| Jun 16, 2026 | C7 Avalanche Flip | Two-phase engineered flush | Steel Wall 30,400 ✅ |
| Jun 17, 2026 | C1B Stratospheric | FOMC day · slow grind | Max Pain 30,100 ✅ |
| Jun 18, 2026 | C1 Breakout Mutation | Post-FOMC gamma desert | Cap Line 30,515 ✅ |
| Jun 22, 2026 | C6 Multi-Variable | 2-SD extension and reversal | VIX floor 16.50 ✅ |
| Jun 23, 2026 | C3→C7 Mutation | Short-squeeze snapback | Max Pain 30,050 ✅ |
| Jun 24, 2026 | C7 Violent Sweep | Stack Max Pain launchpad | Morning high 29,907 ✅ |
| Jun 25, 2026 | C1B Stratospheric | VXN −1σ = session high | Session low 29,312 exact ✅ |
| Jun 26, 2026 | C3 VXN Outside Range | Microsecond convergence | 406-pt recovery ✅ |
| Jun 29, 2026 | C6 Multi-Variable | +2σ exhaustion exact | Asian 1-SD rejected ✅ |
| Jun 30, 2026 | C1 Vacuum Drop | Extreme positive skew +0.260 | VXN cascade all 4 levels ✅ |
| Jul 01, 2026 | C6 Pinned | ZG +0.51% · +3σ overshoot | Live Put Wall defense ✅ |

---

## Valid Trading Window

```
Entry signals valid : 9:30 AM – 11:30 AM New York Time ONLY
Hard close          : 11:30 AM · no exceptions
All pre-market levels are calculated from 9:00–9:15 AM NY data only
Afternoon skew, GEX walls, and Max Pain may differ due to time decay
Do not apply pre-market levels to afternoon sessions without recalculating
```

---

## Risk Disclaimer

> **This repository is for educational and research purposes only. Nothing contained herein constitutes financial advice, investment advice, trading advice, or any other form of advice. All case studies, analytical frameworks, calculations, and structural level identifications are presented solely for the purpose of documenting a systematic analytical methodology applied to publicly available market data.**
>
> **Past structural identification accuracy does not guarantee future results. NQ/MNQ futures trading involves substantial risk of loss and is not appropriate for all investors. Options-derived GEX levels, Max Pain calculations, and implied volatility bands are probabilistic reference levels — not guaranteed price targets or entry/exit signals.**
>
> **The author makes no representations or warranties regarding the accuracy, completeness, or fitness for purpose of any information in this repository. All trading decisions are the sole responsibility of the individual trader. Always manage risk independently and in accordance with your own financial situation and risk tolerance.**
>
> **This framework is valid only within the stated RTH morning window (9:30 AM – 11:30 AM New York Time). Application of these levels outside this window, to other instruments, or in other market conditions is explicitly outside the documented scope of this research.**

---

*VXN Skew-Adjusted Multi-SD Engine · NDX IV Variance Framework*
*CBOE:VXN · CME:NQ/MNQ · Educational use only*
