# Frequently Asked Questions (FAQ)

Common questions about using the scripts in this repository and working with TradingView Pine Script v5.

---

## 1. How do I load a script into TradingView?

**Step-by-step instructions:**

1. Open [TradingView](https://www.tradingview.com/) and select any chart
2. Click the **Pine Editor** tab at the bottom of the screen
3. Copy the entire contents of any `.pine` file from this repository
4. Paste the code into the Pine Editor
5. Click **Save** and give your script a meaningful name
6. Click **Add to Chart**

If compilation errors occur, TradingView will highlight them with red underlines and provide error messages in the console below the editor.

---

## 2. Why don't I see any plots or signals?

**Troubleshooting checklist:**

✓ **Compilation:** Did the script compile without errors? Check for red error messages

✓ **For Indicators:**
- Verify `overlay = true` if you expect plots on the main price chart
- Verify `overlay = false` if it's an oscillator (RSI, MACD) that should appear in a separate pane below

✓ **For Strategies:**
- Ensure you added a *strategy* to the chart, not an indicator
- Check the time range and symbol – some strategies are optimized for specific market conditions
- Open the Strategy Tester tab to view backtest results

✓ **Settings:** Verify that input parameters (lengths, thresholds) are appropriate for your timeframe and asset

---

## 3. Are these scripts "no-repaint"?

We strive for **historical consistency**, but some techniques inherently involve delayed confirmation.

**Common sources of repainting:**

- **Pivot-based indicators** (swing highs/lows, fractals)
  - Require several bars for confirmation
  - Appear perfect historically but are delayed in real-time
  - Examples: Support/Resistance zones, Market Structure tool

- **Higher timeframe requests** with improper settings
  - Using `request.security()` without `lookahead = barmerge.lookahead_off`
  - All scripts in this repo use proper non-repainting settings

- **Intrabar updates** on real-time bars
  - Current bar signals can change until the bar closes
  - Solution: Wait for bar close confirmation

**Our approach:** Scripts that involve delayed confirmation or potential repainting include clear comments explaining the behavior. See [`examples/tutorials/03_no-repaint_tips_and_tricks.md`](../examples/tutorials/03_no-repaint_tips_and_tricks.md) for detailed guidance.

---

## 4. Can I use these scripts for live trading?

These scripts are provided for **educational and research purposes** only.

- They are not financial advice.
- They are not guaranteed profitable or robust.
- They may behave differently on different markets, timeframes, or data sources.

You are responsible for:

- Testing thoroughly in **Backtest** and **Paper Trading** modes.
- Understanding the underlying logic and assumptions.
- Deciding whether and how to risk real capital.

---

## 5. How do I set up alerts?

For indicators that support alerts, you will typically see `alertcondition()` calls.

To use them:

1. Add the script to your chart.
2. Right-click on the chart and choose **Add alert...**, or click the alert icon.
3. In the **Condition** dropdown, select your script’s name.
4. Choose the specific alert condition from the second dropdown (e.g., “Bullish Crossover”).
5. Configure:
   - Trigger (once per bar, once per bar close, etc.).
   - Message (often prefilled or described in the script comments).

Refer to the script’s comments for guidance on which conditions correspond to which signals.

---

## 6. Why does my backtest look different from examples or expectations?

Backtest results are influenced by:

- Symbol and exchange (different price feeds).
- Timeframe.
- Spread, commissions, slippage.
- Strategy settings (capital, order size, pyramiding, etc.).

Also, Pine strategies have some inherent simplifications:

- Filled at bar open/close or best-known price, not always realistic intrabar fills.
- One bar may contain multiple price levels historically that did not actually trade in that order in real time.

Always interpret backtest results as **rough estimates**, not precise simulations.

---

## 7. Can I mix and match scripts?

Yes, but with care.

You can:

- Copy logic from one script into another (e.g., combine a trend filter with a volatility filter).
- Use indicators visually alongside strategies to influence your decisions.

When combining scripts:

- Avoid duplicating conflicting names (rename variables as needed).
- Ensure `indicator()` vs `strategy()` is used appropriately.
- Keep an eye on performance – too many heavy calculations can slow down the chart.

---

## 8. How do I learn Pine Script faster?

**Recommended learning approach:**

1. **Start simple:** Begin with [`ma-crossover-indicator.pine`](../indicators/ma-crossover-indicator.pine) and [`rsi-basic-indicator.pine`](../indicators/rsi-basic-indicator.pine)
2. **Read first:** Study the header comments and inline documentation before running
3. **Experiment actively:** Change one parameter at a time (lengths, colors, conditions)
4. **Follow the learning paths:** See the README for [Beginner/Intermediate/Advanced tracks](../README.md#-learning-paths)
5. **Use official resources:** TradingView's [Pine Script Reference](https://www.tradingview.com/pine-script-reference/v5/) is invaluable
6. **Build projects:** Combine concepts from multiple scripts to create your own tools

**Pro tip:** The best way to learn is by breaking things (safely on a chart). Modify scripts, observe what changes, and understand why.

---

## 9. Can I request a new indicator or feature?

If this is a public GitHub repo:

- Open an **issue** describing:
  - What you’re trying to do.
  - Any references or screenshots if useful.
- Be as specific as possible (markets, timeframes, entry/exit concept).

There’s no guarantee every request will be implemented, but clear, realistic ideas are easier to consider.

---

## 10. Can I use these scripts commercially?

Yes, with conditions. This repository is licensed under the **MIT License**, which permits:

✓ Commercial use
✓ Modification
✓ Distribution
✓ Private use

**Requirements:**
- Include the original MIT license and copyright notice
- Scripts are provided "as-is" without warranty

**Important:** These are educational tools, not guaranteed profitable systems. Always:
- Test thoroughly before any commercial use
- Understand the logic completely
- Implement proper risk management
- Comply with all applicable financial regulations

See the [`LICENSE`](../LICENSE) file for complete terms.

- Many educational repos use permissive licenses (e.g., MIT), which typically allow commercial use with attribution.
- Some licenses might have additional conditions.

When in doubt, consult the license text or ask a legal professional.

---

If your question isn’t answered here, check the other docs in `docs/` or open an issue (for a public repo).
