# Tutorial 02 – Building Your First Strategy

Learn how to convert an indicator into a backtestable trading strategy with entries, exits, and risk management.

## Learning Objectives

- Understand `strategy()` vs `indicator()` functions
- Implement entry and exit logic
- Use the Strategy Tester to analyze performance
- Add risk management with stops and targets

---

## Step 1: Load the Strategy

1. Open [`strategies/ma-crossover-strategy.pine`](../../strategies/ma-crossover-strategy.pine)
2. Study the header comments explaining the system logic
3. Copy the entire script into TradingView Pine Editor
4. Click **Add to Chart**
5. Open the **Strategy Tester** tab (bottom panel)

---

## Step 2: Understanding Strategy Declaration

### Indicator vs Strategy

**Indicator:**
```pine
indicator("My Indicator", overlay = true)
```
- Visual analysis only
- No trade execution
- Can't backtest

**Strategy:**
```pine
strategy("My Strategy", overlay = true, 
     initial_capital = 10000,
     commission_type = strategy.commission.percent,
     commission_value = 0.01)
```
- Executes virtual trades
- Tracks P&L and metrics
- Provides backtesting results

---

## Step 3: Entry Logic

Find the entry code:

```pine
// Entry conditions
bullCross = ta.crossover(fastMA, slowMA)
bearCross = ta.crossunder(fastMA, slowMA)

// Execute trades
if bullCross
    strategy.entry("Long", strategy.long)
if bearCross  
    strategy.entry("Short", strategy.short)
```

**Key Concepts:**
- `strategy.entry()` opens positions
- `strategy.long` / `strategy.short` specifies direction
- Entry ID ("Long", "Short") used to reference positions later

---

## Step 4: Exit Logic

Locate the exit code:

```pine
// Calculate stop loss and take profit
atrValue = ta.atr(14)
stopDist = atrValue * slAtrMult  // SL distance
tpDist = stopDist * tpRR         // TP distance

// Set exits for long positions
if strategy.position_size > 0
    strategy.exit("Long Exit", "Long",
         stop = strategy.position_avg_price - stopDist,
         limit = strategy.position_avg_price + tpDist)
```

**Key Concepts:**
- `strategy.exit()` manages stop loss and take profit
- ATR (Average True Range) creates dynamic stops
- R:R (Risk:Reward) ratio determines profit targets

---

## Step 5: Analyzing Backtest Results

### Key Metrics to Check:

**Performance Tab:**
- **Net Profit:** Total profit/loss
- **Percent Profitable:** Win rate
- **Profit Factor:** Gross profit ÷ Gross loss (>1.5 is good)
- **Max Drawdown:** Largest peak-to-trough decline

**List of Trades:**
- Review individual trade entries/exits
- Check if stops/targets executed as expected
- Identify patterns in winners vs losers

---

## Step 6: Experimentation

### Easy Modifications:

**1. Change MA Periods:**
```pine
fastLen = input.int(20, "Fast MA")  // Instead of 9
slowLen = input.int(50, "Slow MA") // Instead of 21
```

**2. Adjust Risk Parameters:**
```pine
slAtrMult = input.float(3.0, "Stop Loss ATR") // Wider stops
tpRR = input.float(3.0, "Take Profit R:R")   // Larger targets
```

### Intermediate Modifications:

**Add a Trend Filter:**
- Only take long trades when price > 200 SMA
- Only take short trades when price < 200 SMA

**Position Sizing:**
- Use the `riskPct` input to control position size
- Risk fixed % of equity per trade

### Advanced Modifications:

**Multi-Timeframe Filter:**
- Check higher timeframe trend direction
- Only trade with the larger trend

**Time-Based Filters:**
- Only trade during specific sessions
- Avoid major news events

---

## Step 7: Comparing Before/After

### Test These Variations:

| Modification | Expected Impact |
|--------------|----------------|
| Longer MA periods | Fewer trades, less noise |
| Shorter MA periods | More trades, more false signals |
| Wider stops | Better win rate, worse R:R |
| Tighter stops | Lower win rate, better R:R |
| HTF filter ON | Fewer but higher quality trades |

---

## Step 8: Understanding Limitations

### Pine Strategies Assume:
- Orders fill at specific prices (no slippage by default)
- Instant execution
- Sufficient liquidity
- Historical data = future results

### Reality Includes:
- Slippage (especially on market orders)
- Partial fills or rejections
- Changing market conditions
- Psychological factors

**Always paper trade before using real money!**

---

## Next Steps

✅ **Tutorial 03:** [`03_no-repaint_tips_and_tricks.md`](03_no-repaint_tips_and_tricks.md)
- Learn about repainting issues
- Ensure historically consistent signals

✅ **Tutorial 04:** [`04_backtesting_best_practices.md`](04_backtesting_best_practices.md)
- Avoid overfitting
- Proper testing methodology

📚 **Advanced Strategies:**
- [`rsi-mean-reversion-strategy.pine`](../../strategies/rsi-mean-reversion-strategy.pine)
- [`session-breakout-strategy.pine`](../../strategies/session-breakout-strategy.pine)

---

## Common Mistakes

❌ **Over-optimizing parameters** to historical data
✅ Use reasonable defaults, test on multiple assets

❌ **Ignoring commissions and slippage**
✅ Set realistic commission rates in strategy declaration

❌ **Trading every signal**
✅ Add quality filters (trend, volume, session)

❌ **Assuming backtest = live results**
✅ Paper trade first, expect performance degradation

---

**Congratulations!** You've built your first backtestable strategy. Now refine and test it thoroughly!
