[NQ_Framework_Master_Reference.md](https://github.com/user-attachments/files/31832705/NQ_Framework_Master_Reference.md)
# NQ/MNQ Pre-Market Structural Analysis — Master Framework Reference

*VXN Skew-Adjusted Multi-SD Engine · NDX IV Variance Framework*
*Built from 55+ documented RTH sessions — June 2026 to September 2026*
*Valid window: RTH 9:30 AM – 11:30 AM New York Time*

---

## The Four-Step Decision Tree

Every session follows this sequence — in order, without skipping steps.

---

### Step 1 — Regime Identification (Pre-Market)

**The first question before anything else:**

```
Price above Total Gamma Flip (98DTE aggregate) + 0DTE DEX positive
→ Potential Gamma Squeeze / Bullish regime
→ VXN dips = buy entries, rising VXN = absorption noise

Price below Total Gamma Flip + 0DTE DEX negative
→ Potential Bearish / Negative Gamma regime
→ VXN spikes = sell entries, declining VXN = calm/no action

Price at Total Gamma Flip (within 0.2%) + DEX mixed
→ Potential Range / Neutral regime
→ Both sides possible, wait for open confirmation
```

**Why Total Gamma Flip is the primary dividing line:**

Above TGF: dealers are long gamma — they buy dips and sell rallies, dampening moves. Their hedging supports the regime direction.
Below TGF: dealers are short gamma — they sell dips and buy rallies, amplifying moves. Their hedging works against any bounce.

This is a mechanical force, not a prediction. The regime tells you which direction dealer hedging amplifies — not which direction price will go.

---

### Step 2 — DEX Comparison (Pre-Market vs Post-Open)

**Pre-market DEX = dealer starting position**
**Post-open DEX change = real flow hitting the tape**
**The comparison = who is winning**

```
DEX expanding in regime direction = attack or fuel
DEX compressing gradually while price holds = absorption (wall winning slowly)
DEX collapsing suddenly to near-zero = exhaustion (wall won decisively)
DEX expanding against the regime = fuel has become attack
```

**The three DEX patterns documented:**

**Attack (Sep 2):**
Pre-market −175M → 9:45 AM −896M (5x expansion)
Price at Put Wall, unable to break → DEX is attacking the wall
Watch for: sudden DEX collapse to near-zero = exhaustion = wall wins = entry

**Fuel (Sep 2, 10:15 AM):**
Same −618M DEX re-expansion but price already above the wall
Same flow, completely different effect — dealers now buy to hedge
DEX expansion above the wall = fuel for the upside move

**Absorption (Sep 3):**
Pre-market +318M → 10:00 AM +849M peak → +502M at 10:30 AM
Price held 29,248 throughout — barely moved despite peak DEX
DEX compressing while price holds = wall winning slowly = breakout imminent

**Critical rule — DEX is not about magnitude, it is about absorption:**

High DEX + price moves significantly = conviction, directional
High DEX + price barely moves = absorption, opposing wall is defending
Low DEX + price moves significantly = thin air, fragile move
Low DEX + price barely moves = compression, neither side committed

**DEX cannot be spoofed:**
DEX is calculated from real cleared open interest — actual contracts on the books.
Not quotes, not orders that can be pulled. Real capital, real positioning, persists until closed.
This is why DEX is ground truth. VXN can move from spread widening. Price can be pushed in thin markets. DEX requires real money in real contracts.

**DEX sign-flip rule:**
When 0DTE DEX and 1DTE/7DTE DEX have opposite signs — the front-end and back-end are pulling in different directions. This is the DEX-weighted blend engine trigger. The sign-flip itself carries directional information: which tenor is dominant determines which direction gets amplified at the open.

**Small wall + strong DEX rule:**
A small wall normally gets swept. But when DEX is strongly positive (call surge), dealers with long delta mechanically buy every dip — that automatic buying defends even a small floor independently of its OI size. DEX is the real support; the wall is the address.

---

### Step 3 — Nearest Wall (Any Size)

**At the open, price targets the nearest available wall first — not the largest.**

Size determines whether it holds. Not whether it gets tested.

```
Nearest wall holds (body close above/below) = floor/ceiling confirmed
Nearest wall swept (wick through, body returns) = absorbed, level upgraded to hard floor
Nearest wall broken (body closes through) = level flipped, seek next wall
```

**The body/wick distinction:**
- Wick through a level = shorts/longs tried, maximum pressure reached
- Body closes above/below = pressure absorbed, level defended
- Wick through + body return = the strongest absorption confirmation

**Wall size hierarchy:**

| Size | Behavior | Example |
|---|---|---|
| Dominant (largest on chart) | Absorbs significant DEX for extended time | Sep 3: 29,323 absorbed +849M for 75 min |
| Large | Holds cleanly, provides clear bounce | Sep 2: 29,046 held 30 min against −896M |
| Moderate | Holds if DEX supports it | Sep 1: 29,055 held morning + afternoon |
| Small | Holds only with DEX support | Sep 3: 29,248 held with +849M DEX |

**Wall-vs-volume race rule:**
Wall holds if OI growth rate outpaces incoming volume — even if volume is present.
Never buy into a disproportionately large call wall or sell into a put wall until the wall loses the race.

**Level flip rule:**
When price breaks and holds below Total Gamma Flip — it flips from floor to ceiling.
A bounce back toward TGF from below runs into dealers still hedging in the negative gamma regime — rejection at that line rather than support. Always confirmed on next-session settled OI.

**Stack wall rule:**
Multiple smaller walls at adjacent strikes are stronger than their individual size suggests — each represents a separate hedging obligation from different participants. Price must absorb them sequentially. A stack of small walls can defend longer than one large wall if the individual participants are diversified.

**Nearest wall first — documented across sessions:**
- Aug 27: First 3 minutes swept 29,504 cluster, not the deeper Major/Call Wall
- Aug 28: Open immediately swept small Put Wall (29,622), largest walls held
- Aug 31: First 3 minutes swept 29,504 call cluster, reversed hard
- Sep 1: Open swept 29,055 (nearest large put) — not the deeper 28,855
- Sep 2: Open swept 29,198 Put Wall (nearest), then returned above 29,248
- Sep 3: Open swept 29,198 Put Wall (nearest), body held 29,248

---

### Step 4 — VXN Exhaustion (Entry Trigger)

**VXN signals exhaustion — magnitude of tension, not direction.**

Direction comes from price structure context. VXN only tells you when the current move is stretched.

**The exhaustion hierarchy:**

```
±2σ touch alone
→ Ambiguous — may stall or push to ±2.5σ next
→ Note it, watch next 1–2 candles, do not act yet

±2.5σ sweep (price moves through the level)
→ Meaningful exhaustion signal — reached here requires sustained vol expansion
→ Wait for ±2σ cross-back as confirmation

±2σ cross-back after ±2.5σ sweep
→ Confirmed exhaustion — act

±3σ breach
→ Beyond standard exhaustion range
→ Apply three-leg check before calling exhaustion
→ Skew behavior is the filter: compressing skew + +3σ = symmetric vol expansion (Sep 1), not panic
```

**The DEX confirmation hierarchy:**

| VXN signal | DEX confirmation | Strength |
|---|---|---|
| ±2.5σ sweep + ±2σ cross-back | DEX compression | Strongest |
| ±2.5σ sweep alone | DEX compression | Strong |
| ±2σ approach without sweep | DEX compression to near-zero | Valid — DEX fills the gap (Sep 2) |
| ±2σ approach without sweep | No DEX compression | Ambiguous — stay out |

**The 2–3 minute signal rule:**
When the right structural level is the genuine destination, VXN signals it within 2–3 minutes of the price touch. The first ±2.5σ sweep at the wrong level = rejection. The second ±2.5σ sweep at the right level = destination.

**Non-confirmation rule:**
Same VXN SD level, second occurrence, price NOT at a new extreme = non-confirmation.
The price location relative to the previous extreme is the filter.
- Sep 3: +2.5σ at 9:36 AM (session low) = genuine. Near +3σ at 10:00 AM (price 49pts above low) = noise.
- Aug 26: Same +2SD level marked both the ceiling rejection and the floor rejection in one session.

**Regime-specific VXN reading:**

Bearish/Range regime:
```
+2.5σ sweep + nearest wall holds → short exhaustion → entry long
−2.5σ sweep + nearest ceiling holds → call exhaustion → entry short
VXN declining all session = calm, no urgency (−3σ does not require action)
```

Gamma Squeeze regime:
```
+2.5σ sweep + floor holds → short exhaustion → BUY DIP
Every VXN dip to +2σ/+2.5σ zone = buy entry until dominant call wall breaks
Post-breakout: revert to normal exhaustion reads
VXN declining after wall break = squeeze spent, normal session resumes
```

**Why +2σ/+2.5σ matters more than −2σ/−3σ:**
Fear has a natural ceiling — you can only price in so much downside before puts become too expensive and vol exhausts on its own weight. That's why +2.5σ sweeps produce clean reversals.
Calm has no natural floor — VXN can stay below −3σ indefinitely without a mechanical force requiring resolution. −3σ signals calm, not urgency.

---

## Engine Selection Rules

**Standard 30DTE matrix (symmetric or skew-adjusted):**
Use when:
- 0DTE σ is close to 30DTE σ (within ~0.05)
- SKEW is settling or already settled post-open
- DEX profile is moderate and not sign-flipping

**Blend engine (DEX-weighted or variance-weighted):**
Use when:
- 0DTE σ is meaningfully above 30DTE σ (>0.08 divergence)
- SKEW sign-flips between tenors
- DEX sign-flips between 0DTE and 1DTE/7DTE
- Pre-market carries a genuinely extreme read (σ >0.35 or SKEW >0.40)

**Skew settlement rule:**
Pre-market skew can be extreme and still settle to normal by the open (Aug 25, 27, 28, 31, Sep 1, 2).
Always check the 9:30–9:45 AM σ and SKEW before committing to the engine.
A skew sign-flip at the open qualifies as a blend trigger even if the pre-market number was extreme.

**Compressing skew + rising VXN:**
= Symmetric vol expansion, not directional fear
= Standard matrix remains valid even through +3σ VXN breach (Sep 1)
Not a blend trigger — the surface is expanding uniformly, not distorting.

---

## The NDX→NQ Basis Rules

- Confirm the live basis at the 9:30–9:31 AM open — do not reuse pre-market basis
- Basis can drift meaningfully intraday on high-volatility sessions (Sep 1: 55→46, Sep 3: ~48)
- Re-check the basis whenever you're marking a level against a live GEX chart
- The pre-market map correctly identifies structural levels — the live basis tells you exactly where those levels sit in NQ at the moment of interaction

---

## Wall Behavior Rules

**Wall decay on reversal:**
Walls unwind after price leaves, confirmed persisting into next-day settled OI.
Pre-market wall sizes must be re-checked post-move and again the following session.

**Wall formation around pre-existing anchor:**
A tiny pre-existing wall can become the edge of a larger live-built zone (Aug 12).
Live volume monitoring tells you when a wall is growing into something structural.

**Pre-emptive defense of an oversized wall:**
When a very large wall sits well below current price, price may stall and reverse before reaching it — the wall's presence alone changes dealer behavior above it.

**Fair-zone midpoint:**
The midpoint between two independently-confirmed structural boundaries is a reference level for range sessions. Price naturally gravitates toward the midpoint when vol is suppressed.

---

## The Three-Leg Exhaustion Check

Before calling an extreme read as "exhausted, not early":

1. **Rejection at the level** — price touched the extreme and showed a reversal candle
2. **Real volume still building in the move's direction** — volume not fading at the extreme
3. **Structure on the opposite side to reverse into** — a real wall or level to target

If all three say "no" → the move is early, not exhausted. Continuation is correct.
If any one says "yes" → exhaustion possible, apply VXN and DEX confirmation before acting.

---

## Position Sizing Rule

```
Size = FLOOR(B ÷ (D_total × M))

B = $100–150 hard risk budget (MNQ)
D_total = structural stop distance + execution lag buffer
M = $2/point (MNQ)

If result = 0 → skip trade entirely, never default to 1 contract
```

---

## Key Framework Findings (Chronological)

| Session | Finding |
|---|---|
| Aug 5 | VXN tracks price same direction in stable-skew regime (not always inverse) |
| Aug 6 | Wall decay confirmed post-move on next-day settled OI |
| Aug 11 | Liquidity-seeking sweep — price targets volume pools, not directional conviction |
| Aug 12 | VXN exact SD-extreme touch-and-reject = fear spike hit natural ceiling, pullback capped |
| Aug 13 | Wall-vs-volume race: asymmetric range read from live GEX reveals weak boundary before breakout |
| Aug 17 | Put volume 5x overwhelming a call wall signals imminent break, not defense |
| Aug 20 | Immediate 98DTE small-wall stack check — stacked small walls cap the open pullback |
| Aug 21 | Skew sign-flip leads VXN + price reversal by 5 minutes |
| Aug 24 | DEX-weighted blend engine: VXN breach of standard +3σ within minutes = engine switch live |
| Aug 25 | Skew settlement from extreme pre-market to normal at open — standard matrix confirmed |
| Aug 26 | Same +2SD level marks ceiling AND floor in one session — VXN signals magnitude, not direction |
| Aug 27 | Nearest wall first: open targets proximity, not size |
| Aug 28 | Small 0DTE Put Wall swept immediately (confirmed weakest) — call wall stack caps every push |
| Aug 31 | Live put-volume absorption holds floor above pre-market structural levels — absorption is the floor |
| Sep 1 | Compressing skew + rising VXN = symmetric expansion, standard matrix valid through +3σ; ±2.5σ exhaustion hierarchy; 2–3 minute VXN signal rule |
| Sep 2 | DEX attack vs fuel: same flow, opposite effect depending on price location relative to wall; DEX compression = exhaustion confirmation even when VXN doesn't reach ±2.5σ |
| Sep 3 | Gamma Squeeze regime: every VXN dip = buy entry until dominant call wall breaks; small wall holds with strong DEX support; DEX absorption: high volume + price barely moves = wall winning |

---

## Quick Reference — Session Open Checklist

```
□ 1. Price vs Total Gamma Flip → regime (bullish/bearish/neutral)
□ 2. 0DTE DEX sign and magnitude → confirm regime direction
□ 3. Pre-market DEX vs 9:45 AM DEX → what flow hit the tape at open
□ 4. NDX→NQ basis confirmed live at 9:31 AM
□ 5. Nearest wall to current price identified (any size)
□ 6. Skew settled? → engine selection confirmed
□ 7. VXN anchor captured at 9:31 AM → matrix calculated
□ 8. Watch: nearest wall holds or breaks on first test
□ 9. DEX expanding/compressing → attack, absorption, or exhaustion
□ 10. VXN ±2.5σ sweep + ±2σ cross-back + structural level = entry
```

---

*This document is a living reference — updated as new sessions add findings.*
*For educational and research purposes only. Not financial advice.*
*CBOE:VXN · CME:NQ/MNQ*
