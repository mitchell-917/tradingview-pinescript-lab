# Strategies Folder Overview

This folder contains **example TradingView strategies** built on top of the indicators from this repo.

Each strategy is written in Pine Script v5 and heavily commented, so you can learn **how to go from indicator idea → backtestable strategy**.

---

## 1. `ma-crossover-strategy.pine`

A classic **trend-following** system:

- Uses a **fast/slow MA crossover** on the current timeframe.
- Optional **higher timeframe MA filter** to only trade in the dominant trend.
- ATR-based stop loss and take profit with configurable **risk per trade**.

**Good for learning:**

- How to port an indicator (MA crossover) into a `strategy`.
- Using `strategy.entry` + `strategy.exit` with dynamic position sizing.
- Combining trend filters and R:R exits.

---

## 2. `rsi-mean-reversion-strategy.pine`

A simple **mean reversion** concept:

- Buys when RSI leaves oversold territory.
- Sells when RSI leaves overbought territory.
- Optional long-term MA filter to only fade pullbacks in the main trend.
- Uses ATR-based SL and TP, plus optional **exit when RSI returns to 50**.

**Good for learning:**

- Oscillator-based strategies.
- Counter-trend logic and risk vs reward.
- Combining RSI signals with a higher timeframe or long MA filter.

---

## 3. `session-breakout-strategy.pine`

A **session range breakout** model inspired by the Session High/Low indicator:

- Marks a user-defined intraday session (e.g. London 08:00–12:00).
- Records session high and low.
- After the session (or optionally during), trades breakouts above/below that range.
- Uses ATR buffers around SL and configurable R:R for TP.

**Good for learning:**

- Working with `input.session` and session-based logic.
- Trading breakouts of structurally important intraday levels.
- Position sizing based on distance from session extremes.

---

## 4. `liquidity-sweep-reversal-strategy.pine`

A more advanced **liquidity sweep / stop-hunt reversal** concept:

- Re-uses the logic from `liquidity-sweep-detector.pine`.
- Longs after downward sweeps (lows taken and price closes back inside).
- Shorts after upward sweeps (highs taken and price closes back inside).
- ATR-based stops beyond the sweep and TP using a reward multiple.

**Good for learning:**

- How to reuse indicator logic inside a strategy.
- Event-based reversal entries vs continuous conditions.
- The risks and behaviour of trading “stop hunts” / liquidity grabs.

---

## How to Use These Strategies

1. Open a script in TradingView Pine Editor.
2. Click **Add to Chart**.
3. Open the **Strategy Tester** tab to see performance metrics.
4. Experiment by changing:
   - Timeframes
   - Assets (FX, indices, crypto)
   - Risk parameters (SL, TP, risk %)
   - Filters (trend filters ON/OFF)

> These are **learning tools**, not production-ready algos.  
> The goal is to help you understand how to structure strategies, not to sell a “holy grail”.

---

## Suggested Learning Path

1. Start with `ma-crossover-strategy.pine` to understand basic `strategy` structure.
2. Move to `rsi-mean-reversion-strategy.pine` to see oscillator-based logic.
3. Explore `session-breakout-strategy.pine` for session/range concepts.
4. Finally, look at `liquidity-sweep-reversal-strategy.pine` as a more advanced, event-driven example.

Feel free to fork, tweak, and remix these into your own systems 🚀
