# FAQ – Frequently Asked Questions

This FAQ covers common questions about using the scripts in this repository and working with TradingView Pine Script.

---

## 1. How do I load a script into TradingView?

1. Open TradingView and select a chart.
2. Click **Pine Editor** at the bottom.
3. Open the desired `.pine` file from this repo in your text editor.
4. Copy all of its contents.
5. Paste into the Pine Editor.
6. Click **Save** and give your script a name.
7. Click **Add to chart**.

If there are errors, TradingView will highlight them in the editor panel.

---

## 2. Why don’t I see any plots or signals?

Check the following:

- Did the script compile successfully? Look for errors or warnings.
- For indicators:
  - Confirm `overlay = true` if you expect plots on the price chart.
  - Confirm `overlay = false` if it’s an oscillator that should appear in a separate pane.
- For strategies:
  - Make sure you added the *strategy* to the chart (not just an indicator).
  - Check the time range and symbol – some logic may be specific to certain volatility/market types.

Also verify that relevant settings (lengths, thresholds) are reasonable for the timeframe and market you’re looking at.

---

## 3. Are these scripts “no-repaint”?

Many scripts aim to be **historically consistent**, but not all scripts are strictly “no-repaint.”

Some common sources of repainting or delayed signals:

- **Pivots / swing points** – They need several bars to confirm, so historically they look perfect, but in real time they appear **after** a pattern is complete.
- **`request.security()` with lookahead** – If a script uses future-looking security calls (rare here), that will be clearly commented as “for demonstration only.”
- **Intrabar updates** – Realtime bars can change until they close; signals based on the current bar can appear/disappear during the bar’s formation.

Where repainting or delayed signals are inherent to the technique, we call it out in comments in the script.

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

Suggestions:

1. Start with **beginner indicators** in `indicators/beginner/`.
2. Change one thing at a time (lengths, conditions, plot styles).
3. Read the comments **before** and **after** running the script.
4. Use the Pine Editor’s built-in **reference** (search the manual for functions).
5. Gradually move to **intermediate** and **advanced** scripts.

The more you modify and experiment, the faster you’ll learn.

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

Check the `LICENSE` file in the root of the repository.

- Many educational repos use permissive licenses (e.g., MIT), which typically allow commercial use with attribution.
- Some licenses might have additional conditions.

When in doubt, consult the license text or ask a legal professional.

---

If your question isn’t answered here, check the other docs in `docs/` or open an issue (for a public repo).
