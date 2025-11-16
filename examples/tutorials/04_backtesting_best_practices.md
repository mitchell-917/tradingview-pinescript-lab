# Tutorial 04 – Backtesting Best Practices

Backtesting is a powerful tool, but it has limitations.

## 1. Understand the Model

Pine strategies assume simplified execution:

- Orders fill at bar prices (open/close/high/low), not intrabar ticks.
- Slippage and spreads are approximations at best.

## 2. Key Settings to Check

In the Strategy Tester:

- Initial capital.
- Order size (fixed units vs % of equity).
- Commission settings.
- Slippage.

Make sure these reflect how you might trade in reality.

## 3. Avoid Overfitting

- Don’t optimize parameters to maximize historical profit only.
- Check performance across multiple symbols and timeframes.
- Look at drawdowns, not just net profit.

## 4. Iterate Thoughtfully

Use the strategies in `strategies/` as starting points:

- Add filters.
- Adjust exits.
- Compare results realistically, not just on a single cherry-picked chart.
