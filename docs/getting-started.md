# Getting Started with TradingView Pine Lab

Welcome to **TradingView Pine Lab** – a practical collection of indicators and strategies written in Pine Script for TradingView.

This document walks you through:

- How to use the scripts in this repository.
- How to load them into TradingView.
- Basic Pine Script concepts you’ll see repeatedly in this codebase.

---

## 1. Prerequisites

To use these scripts, you’ll need:

- A **TradingView account** (free is fine for most examples).
- A web browser capable of running TradingView charts.
- Basic familiarity with charts (candles, OHLC, timeframes).

No prior Pine Script knowledge is required for the *beginner* scripts.

---

## 2. How This Repository Is Organized

Relevant folders for indicators and strategies:

- `indicators/`  
  Standalone visual tools (trend, momentum, market structure, levels, etc.).

- `strategies/` *(planned folder in full repo)*  
  Scripts that include entries/exits and run backtests.

Each of those folders is further split by difficulty:

- `beginner/` – Simple, heavily commented scripts. Copy-paste friendly.
- `intermediate/` – More features, light abstractions, still very readable.
- `advanced/` – More logic, more trade-offs, and more opinionated design.

---

## 3. Loading a Script into TradingView

1. Open TradingView and select a chart.
2. At the top, click **Pine Editor** to open the editor panel.
3. Open a file from this repository (for example:  
   `indicators/beginner/ma-crossover-indicator.pine`) in your code editor.
4. Copy the entire file contents.
5. Paste into the **Pine Editor** in TradingView.
6. Click **Save** (give it a descriptive name).
7. Click **Add to chart**.

If there are any errors, TradingView will highlight them at the bottom of the editor.  
All scripts in this repository are written for **Pine Script v5**.

---

## 4. Basic Pine Script Concepts You’ll See

Across the scripts, you’ll see some recurring functions and keywords:

- `//@version=5` – Declares the Pine Script version.
- `indicator()` vs `strategy()` – Indicators visualize; strategies also place trades.
- `input.*()` – User options that appear in the script settings.
- `plot()` – Draws a line or series on the chart.
- `ta.*` – Technical analysis helpers (e.g., `ta.sma`, `ta.rsi`, `ta.atr`).

Whenever a script uses a slightly more advanced feature, we try to explain it with comments above the relevant block of code.

---

## 5. Recommended Learning Path

If you are **new to Pine Script**, a good path is:

1. **MA Crossover Indicator**  
   `indicators/beginner/ma-crossover-indicator.pine`  
   Learn inputs, moving averages, simple conditions, and plotting.

2. **RSI Basic Indicator**  
   `indicators/beginner/rsi-basic-indicator.pine`  
   Learn oscillators, horizontal levels, and color conditions.

3. **Support & Resistance Zones**  
   `indicators/beginner/support-resistance-zones.pine`  
   Learn how to work with recent highs/lows and draw levels.

Then move on to **intermediate** scripts to see:

- Multi-timeframe logic.
- Volatility-based tools.
- Session-based levels and dashboards.

Finally, explore **advanced** scripts once you’re comfortable reading Pine code.

---

## 6. How to Ask for Help or Contribute

If this is part of a public GitHub repo:

- Open an **issue** if something doesn’t work as expected.
- Open a **pull request** if you’d like to:
  - Fix a bug.
  - Improve comments or documentation.
  - Add an indicator or strategy following the style guide.

Before contributing, read:

- `docs/repository-overview.md`
- `docs/pine-style-guide.md`

---

## 7. Keep Experimenting

Use these scripts as a **starting point**, not as final trading systems.

- Try changing parameters.
- Add filters (trend, volatility, volume).
- Combine ideas from multiple examples.

The fastest way to learn Pine Script is to **edit, break, fix, and iterate**.
