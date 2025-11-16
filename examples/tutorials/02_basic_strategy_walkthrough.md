# Tutorial 02 – Basic Strategy Walkthrough

This tutorial uses `strategies/beginner/ma-crossover-strategy.pine` as a starting point.

## 1. Load the Strategy

1. Open `strategies/beginner/ma-crossover-strategy.pine`.
2. Paste it into TradingView’s Pine Editor.
3. Click **Add to chart**. You should see backtest results in the Strategy Tester.

## 2. Read the Header

The header explains:

- What the strategy is trying to do.
- Key assumptions (e.g., always in the market, no filters).

## 3. Understand Entries & Exits

- Locate the `strategy.entry()` calls.
- See how `bullCross` and `bearCross` conditions control long/short entries.
- Notice there is no explicit `strategy.exit()` call – positions flip on each crossover.

Try adding:

- A basic stop loss using `strategy.exit()`.
- A take profit based on a multiple of ATR.

## 4. Run Simple Experiments

- Change MA lengths.
- Restrict trading to specific timeframes or sessions.
- Observe how the equity curve changes in the Strategy Tester.
