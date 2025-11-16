# Indicator Development Guide (TradingView / Pine Script v5)

This guide is meant to help people who find your repo learn **how to build TradingView indicators** using Pine Script v5.

It uses your lab-style indicators (RSI, MA crossovers, structure, volume profile, etc.) as reference implementations.

---

## 1. How TradingView Scripts Are Structured

Every Pine Script starts with:

```pine
//@version=5
indicator("My Cool Indicator", overlay = true)
```

Key parts:

- `//@version=5`  
  Tells TradingView which Pine version you’re using (always v5 for new code).

- `indicator()` vs `strategy()`  
  - `indicator()` is for visual tools only (no orders executed).
  - `strategy()` is for backtestable strategies (entries, exits, performance).

- `overlay = true` vs `overlay = false`  
  - `overlay = true` → plots on the price chart.  
  - `overlay = false` → plots in its own separate pane (like RSI).

---

## 2. Inputs: Making Indicators Configurable

Inputs let users configure your indicator from the UI **without editing code**.

Example:

```pine
length = input.int(20, "Length", minval = 1)
src    = input.source(close, "Source")
```

Common input types:

- `input.int()` – integer (lengths, bars, counts)
- `input.float()` – decimals (multipliers, thresholds)
- `input.bool()` – checkboxes (show/hide stuff)
- `input.string()` – dropdowns (MA type, mode)
- `input.color()` – custom colours
- `input.timeframe()` – user-selectable timeframes
- `input.session()` – session times like "0900-1700"

In your repo, see:

- `ma-crossover-indicator.pine` for **MA type & lengths**.
- `volatility-band-indicator.pine` for **length & std-dev multiplier**.
- `volume-profile-lite.pine` for **bins & lookback**.

---

## 3. Basic Building Blocks: Series & Calculations

Pine operates on **series** (values per bar).

Classic example: a Moving Average:

```pine
ma = ta.sma(close, 20)
plot(ma, "20 SMA", color = color.orange)
```

Other common built-ins:

- `ta.rsi(src, length)` – RSI
- `ta.ema(src, length)` – EMA
- `ta.stdev(src, length)` – standard deviation
- `ta.atr(length)` – average true range
- `ta.highest(src, length)` / `ta.lowest(src, length)` – extremes
- `ta.crossover(a, b)` / `ta.crossunder(a, b)` – crossing conditions

Your indicators demonstrate these:

- `rsi-basic-indicator.pine` – uses `ta.rsi`.
- `volatility-band-indicator.pine` – uses `ta.stdev`.
- `ma-crossover-indicator.pine` – uses `ta.crossover` and `ta.crossunder`.

**Tip:** Keep your calculations in a clear section like:

```pine
//-----------------------------------------------------------------------------
// CALCULATION
//-----------------------------------------------------------------------------
```

to make the code structure easy to learn from.

---

## 4. Conditions & Alerts

Indicators often boil down to answering:

> “When should something be highlighted or trigger an alert?”

Example from the MA crossover script:

```pine
bullCross = ta.crossover(fastMa, slowMa)
bearCross = ta.crossunder(fastMa, slowMa)

plotshape(bullCross, title = "Bullish Cross", style = shape.triangleup, location = location.belowbar)
plotshape(bearCross, title = "Bearish Cross", style = shape.triangledown, location = location.abovebar)

alertcondition(bullCross, "Bullish MA Crossover", "Fast MA crossed ABOVE slow MA.")
alertcondition(bearCross, "Bearish MA Crossover", "Fast MA crossed BELOW slow MA.")
```

Your repo shows several patterns:

- **RSI OB/OS alerts** → `rsi-basic-indicator.pine`
- **Band breakouts** → `volatility-band-indicator.pine`
- **Liquidity sweeps** → `liquidity-sweep-detector.pine`

**Rule of thumb:** write conditions in a logically simple, readable way and then reuse them for:

- visual markers (`plotshape`, `bgcolor`)
- alerts (`alertcondition`)

---

## 5. Overlays vs Separate Windows (Panels)

Deciding where an indicator should live:

- Use `overlay = true` for:
  - trend tools (MAs, structure, S/R, sessions)
  - anything that directly references price levels

- Use `overlay = false` for:
  - oscillators (RSI, Stoch, MACD-style)
  - custom metrics not naturally “on price”

Examples in your repo:

- `support-resistance-zones.pine` → **overlay** (draws lines on price)
- `session-high-low-indicator.pine` → **overlay**
- `rsi-basic-indicator.pine` → **separate pane**

---

## 6. Multi-Timeframe (MTF) Basics

MTF logic uses `request.security()` to pull data from another timeframe.

Example:

```pine
htf = input.timeframe("60", "Higher Timeframe")
htfMa = request.security(syminfo.tickerid, htf, ta.ema(close, 50))

plot(htfMa, "HTF EMA", color = color.new(color.blue, 50))
```

In your repo, the **MTF Trend Dashboard** generalises this:

```pine
f_trend(tf) =>
    c_tf  = request.security(syminfo.tickerid, tf, close)
    ma_tf = request.security(syminfo.tickerid, tf, ta.ema(close, maLen))
    // classify bull / bear / neutral...
```

Tips:

- Always think about **repainting** (HTF bars aren’t complete until they close).
- For most educational uses, `request.security()` with default settings is fine.
- Use MTF data mainly as a **filter** (e.g. only take longs if higher TF is bullish).

---

## 7. Using Pivots & Swings

Pivots are key to structure, support/resistance, and liquidity concepts.

Basic usage:

```pine
left  = 2
right = 2

ph = ta.pivothigh(high, left, right)
pl = ta.pivotlow(low,  left, right)

isSwingHigh = not na(ph)
isSwingLow  = not na(pl)
```

Used in:

- `market-structure-tool.pine` – to label HH/HL/LH/LL.
- `support-resistance-zones.pine` – to generate S/R levels.
- `liquidity-sweep-detector.pine` – as an optional filter (sweeps at swing highs/lows).

Key points to teach:

- Larger pivot lengths = fewer, more significant swings.
- Smaller lengths = more “noisy” swings.

You can encourage users to experiment with `pivotLen` on different timeframes.

---

## 8. Arrays, Loops & Custom Tools

For more advanced indicators (like your **Volume Profile Lite** or S/R clustering), arrays and loops are essential.

Example patterns:

```pine
var float[] levels = array.new_float()

// Add new level at beginning
array.unshift(levels, newLevel)

// Keep only latest N
while array.size(levels) > 20
    array.pop(levels)
```

Usage in repo:

- `volume-profile-lite.pine`
  - Uses arrays to store **volume per price bin** and then draws `box.new()` for each bin.
- `support-resistance-zones.pine`
  - Uses arrays to store **levels** and **line references** for dynamic S/R zones.
- `market-structure-tool.pine`
  - Uses arrays to store sequences of swings and their types (HH/HL/LH/LL).

Teaching points:

- `var` means a variable persists across bars.
- Arrays let you track “history” beyond the built-in series.
- Always manage size (`while array.size > max`) to avoid hitting limits and keeping code efficient.

---

## 9. Building a Simple Strategy from an Indicator

Although your current folder is focused on indicators, it’s natural to show how to turn them into a basic strategy.

**Conceptual steps:**
1. Start from an indicator script (e.g. MA Crossover).
2. Change `indicator(...)` to `strategy(...)`.
3. Replace visual-only signals with `strategy.entry` / `strategy.close`.

Mini example (pseudo-code):

```pine
//@version=5
strategy("MA Crossover Strategy [Lab]", overlay = true, initial_capital = 10000)

fastLen = input.int(9, "Fast")
slowLen = input.int(21, "Slow")

fastMa = ta.ema(close, fastLen)
slowMa = ta.ema(close, slowLen)

bull = ta.crossover(fastMa, slowMa)
bear = ta.crossunder(fastMa, slowMa)

if bull
    strategy.entry("Long", strategy.long)

if bear
    strategy.entry("Short", strategy.short)
```

You can then:

- Backtest on different symbols/timeframes.
- Add filters from your other indicators (e.g. only trade with MTF trend).
- Use S/R or session levels as targets/stop logic.

Later you could add a dedicated `strategy-development-guide.md` to expand this.

---

## 10. Publishing & Making Your Repo “Star-Worthy”

To help people find value:

1. **Good naming & descriptions**
   - Make indicator titles clear: `[Lab]` suffix is nice for “learning tools”.
   - In the Pine header comments, describe exactly what the script teaches.

2. **Screenshots / GIFs**
   - Add example screenshots (in `docs/img/`) and reference them from your README.
   - Show “before/after” of a chart with your indicators applied.

3. **Link back to GitHub from TradingView**
   - When you publish a script on TradingView (public or invite-only), include:
     > “Source code and more examples: GitHub link”

4. **Organise folders**
   - `indicators/` – your .pine files (these).
   - `strategies/` – strategy examples.
   - `docs/` – learning material (like this guide).
   - `examples/` – maybe presets, screenshots, template layouts.

5. **Keep things extremely well-commented**
   - Exactly what you’re doing: educational comments, section headers, and friendly tooltips.
   - Aim for every script to double as a tutorial.

---

## 11. Suggested Reading Order for Your Repo

If someone lands on your GitHub, you can guide them:

1. `docs/indicator-development-guide.md` (this file)
2. Basic building blocks:
   - `indicators/rsi-basic-indicator.pine`
   - `indicators/ma-crossover-indicator.pine`
3. Volatility & ranges:
   - `indicators/volatility-band-indicator.pine`
   - `indicators/session-high-low-indicator.pine`
4. Structure & S/R:
   - `indicators/market-structure-tool.pine`
   - `indicators/support-resistance-zones.pine`
5. Advanced concepts:
   - `indicators/liquidity-sweep-detector.pine`
   - `indicators/volume-profile-lite.pine`
   - `indicators/mtf-trend-dashboard.pine`

You can also add a `README.md` at the repo root that links to this guide and suggests this learning path.

---

Happy building, and welcome to the world of Pine Script 👋  
This repo can genuinely become a go-to learning resource if you keep expanding it with clear, educational examples.
