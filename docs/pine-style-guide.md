# Pine Style Guide

This style guide describes how code in **TradingView Pine Lab** is written and organized.

The goals are:

- Make scripts **easy to read** and **easy to modify**.
- Keep examples **consistent**, so you can transfer knowledge from one file to another.
- Encourage good habits for people learning Pine Script.

---

## 1. Language Version

- All scripts use **Pine Script v5**:

  ```pine
  //@version=5
  ```

- We prefer v5 built-ins (`ta.*`, `math.*`, `array.*`, etc.) for clarity and modern features.

---

## 2. Script Declarations

- Indicators use `indicator()`.
- Strategies use `strategy()`.

Example:

```pine
//@version=5
indicator("MA Crossover Indicator", overlay = true, timeframe = "", timeframe_gaps = true)
```

Key points:

- **Human-readable title** as the first argument.
- Explicit `overlay` setting (`true` for drawing on price, `false` for separate pane).
- Optional `timeframe` and `timeframe_gaps` parameters declared explicitly when relevant.

---

## 3. File Structure

Each script should follow this rough order:

1. **Header comment & metadata**
2. `//@version=5`
3. `indicator()` / `strategy()` declaration
4. **Inputs**
5. **Core calculations**
6. **Conditions & logic**
7. **Plotting / visualization**
8. **Alerts / strategy.* calls (if any)**
9. **Notes / limitations (commented)**

Example structure (simplified):

```pine
// MA Crossover Indicator
// - Shows fast/slow MAs and highlights crossovers.
// - Designed as an educational example.

//@version=5
indicator("MA Crossover Indicator", overlay = true)

// Inputs
fastLength = input.int(9, "Fast MA Length", minval = 1)
slowLength = input.int(21, "Slow MA Length", minval = 1)

// Calculations
fastMA = ta.sma(close, fastLength)
slowMA = ta.sma(close, slowLength)

// Conditions
bullCross = ta.crossover(fastMA, slowMA)
bearCross = ta.crossunder(fastMA, slowMA)

// Plotting
plot(fastMA, "Fast MA")
plot(slowMA, "Slow MA")

plotshape(bullCross, "Bullish Crossover", location = location.belowbar, style = shape.triangleup)
plotshape(bearCross, "Bearish Crossover", location = location.abovebar, style = shape.triangledown)
```

---

## 4. Naming Conventions

### Variables

- Use **lowerCamelCase** for variables: `fastLength`, `sessionHigh`, `rsiValue`.
- Be descriptive: `trendUp` is better than `a`, `cond`, or `x`.

### Inputs

- Prefix with the concept if helpful, e.g.:
  - `lenFast`, `lenSlow` (for lengths).
  - `multAtr`, `riskPerTrade` (for multipliers, risk settings).

- Use descriptive labels in `input.*()` so users know what they are changing.

### Constants

- Use ALL_CAPS sparingly for “real” constants (e.g., `MAX_HISTORY_BARS`), but this is optional.

---

## 5. Commenting

Aim for **helpful, not noisy** comments.

- Explain the **intent** of a block, not every trivial line.
- Place brief block comments **above** the the code they explain.

Example:

```pine
// Identify recent swing highs/lows to build support/resistance zones.
swingHigh = ta.pivothigh(high, leftBars, rightBars)
swingLow  = ta.pivotlow(low, leftBars, rightBars)
```

Avoid:

```pine
// add 1 to i
i := i + 1
```

For more complex scripts, consider a short “mini-docstring” at the very top describing:

- What the tool does.
- How it can be used.
- Any non-obvious limitations.

---

## 6. Inputs & Defaults

Good defaults matter. Prefer:

- Widely used defaults (e.g., 14 for RSI, 20 for Bollinger, 14 or 10 for ATR).
- Sensible, not overly-optimized parameters.

Use `input.group` for clarity when there are many inputs, especially in intermediate/advanced scripts.

Example:

```pine
lenRsi   = input.int(14, "RSI Length", minval = 1, group = "RSI Settings")
obLevel  = input.int(70, "Overbought Level", group = "RSI Settings")
osLevel  = input.int(30, "Oversold Level", group = "RSI Settings")
```

---

## 7. Repainting & Security Calls

Where relevant:

- **Call out repainting behavior** in comments.
- For signals based on the *current bar* that might change, mention that this is for visualization and not guaranteed at bar close.
- For `request.security()` calls, clearly label higher timeframes and use `barmerge.lookahead_off` unless explicitly needed otherwise.

Example:

```pine
// Fetch higher-timeframe close without lookahead (no repainting from future data).
htfClose = request.security(syminfo.tickerid, htf, close, lookahead = barmerge.lookahead_off)
```

---

## 8. Plotting

- Use descriptive `title` for plots – this is what appears in the TradingView legend.
- Prefer minimal but meaningful color usage.
- When using `plotshape` or `plotchar`, ensure shape titles are unique and descriptive.

Example:

```pine
plot(fastMA, "Fast MA")
plot(slowMA, "Slow MA")

plotshape(bullCross, "Bullish Crossover", location = location.belowbar, style = shape.triangleup, size = size.tiny)
```

---

## 9. Alerts & Strategies

For indicators that generate actionable signals:

- Use `alertcondition()` with a clear name and message template.
- Note in comments what the alert is intended for (entry, exit, filter, etc.).

For strategies:

- Use `strategy.entry()`, `strategy.exit()`, and `strategy.close()` explicitly.
- Comment on the **logic** for entries/exits and any position sizing assumptions.

---

## 10. Error Handling & Safety

Pine Script is limited, but we can still:

- Guard against division by zero.
- Use `nz()` or `math.max()` where appropriate.
- Keep loops minimal and predictable.

Example:

```pine
atrValue = ta.atr(lenAtr)
safeAtr  = atrValue > 0 ? atrValue : 1.0
```

---

## 11. Performance Considerations

- Avoid unnecessary loops and `varip` abuse.
- Only store state you actually need.
- For advanced scripts, note in comments if a script is heavy and which settings increase cost (e.g., number of lookback bars, resolution of volume profile, etc.).

---

## 12. Final Thoughts

This style guide is a **baseline**, not a rigid law.

If you have a strong reason to deviate (for clarity or functionality), do so – but leave a short comment explaining *why*.  
The priority is always **readability, teachability, and correctness** over extreme compactness or “clever” tricks.
