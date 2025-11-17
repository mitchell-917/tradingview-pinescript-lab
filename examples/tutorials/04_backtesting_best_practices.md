# Tutorial 04 – Backtesting Best Practices

Backtesting is a powerful tool for evaluating trading strategies, but it has significant limitations. This guide teaches you how to conduct realistic, meaningful backtests and avoid common pitfalls.

## Understanding Backtest Limitations

### What Pine Strategies Assume:

✅ **Perfect Execution:**
- Orders fill at exact prices (OHLC)
- No requotes or rejections
- Infinite liquidity
- Instant order processing

✅ **Simplified Market Model:**
- One bar = four prices (O, H, L, C)
- No intrabar price action
- No spread widening during news
- No overnight gaps (unless in data)

### What Reality Includes:

❌ **Slippage:**
- Market orders fill at worse prices
- Large orders move the market
- Fast markets = worse fills

❌ **Costs:**
- Commissions
- Spreads
- Swap/rollover fees
- Platform fees

❌ **Execution Issues:**
- Order rejections
- Partial fills
- Latency delays
- Broker restrictions

❌ **Market Conditions:**
- Liquidity varies
- Volatility changes
- Correlations shift
- Black swan events

---

## Critical Strategy Settings

### 1. Initial Capital

```pine
strategy("My Strategy", 
    initial_capital = 10000)  // Match your real account
```

**Why it matters:**
- Affects position sizing
- Influences compounding
- Determines realistic profit expectations

**Recommendation:**
Set to your actual trading capital or slightly less

---

### 2. Commission Structure

```pine
strategy("My Strategy",
    commission_type = strategy.commission.percent,
    commission_value = 0.1)  // 0.1% per trade
```

**Commission Types:**
- `strategy.commission.percent` - % of trade value
- `strategy.commission.cash_per_contract` - Fixed $ per contract
- `strategy.commission.cash_per_order` - Fixed $ per order

**Recommended Values:**

| Asset Class | Commission | Notes |
|-------------|------------|-------|
| **Forex** | 0.01-0.02% | Spread usually 1-3 pips |
| **Stocks (US)** | 0.01-0.10% | Depends on broker |
| **Crypto** | 0.10-0.25% | Higher fees typical |
| **Futures** | $2-5/contract | Per round trip |

**Critical:** Always include commissions. A 0.1% commission can turn a profitable system into a loser.

---

### 3. Slippage

```pine
strategy("My Strategy",
    slippage = 2)  // 2 ticks/pips of slippage
```

**What is slippage?**
Difference between expected price and actual fill price

**Typical Slippage:**
- **Low volatility:** 1-2 ticks
- **Normal conditions:** 2-5 ticks
- **News/volatile:** 10+ ticks
- **Large orders:** Proportional to size

**Recommendation:**
Use 3-5 ticks for conservative estimates

---

### 4. Order Execution

```pine
strategy("My Strategy",
    process_orders_on_close = true,  // Execute at bar close
    calc_on_every_tick = false)      // No intrabar recalc
```

**Safe Settings:**
- `process_orders_on_close = true` - Most realistic
- `calc_on_every_tick = false` - Prevents lookahead
- `calc_on_order_fills = false` - Prevents unrealistic recalc

---

## Avoiding Overfitting

### What is Overfitting?

**Overfitting** = Optimizing parameters so perfectly to historical data that the strategy fails on new data.

### Signs of Overfitting:

❌ **Too many parameters:**
```pine
// 8+ parameters = high risk
maLen1 = 23
maLen2 = 47  
rsiLen = 13
threshold = 67.3  // Too specific!
```

❌ **Unrealistic performance:**
- Win rate > 80%
- Profit factor > 5
- Every trade wins
- Smooth equity curve with no drawdowns

❌ **Single asset optimization:**
- Works perfectly on EURUSD
- Fails on GBPUSD, USDJPY

❌ **Single timeframe optimization:**
- Perfect on 1H
- Terrible on 4H and 15M

---

### How to Avoid Overfitting

#### 1. Use Walk-Forward Testing

**Traditional Backtest (WRONG):**
```
Optimize on: Jan 2020 - Dec 2023
Test on:     Jan 2020 - Dec 2023  ❌ Same data!
```

**Walk-Forward (RIGHT):**
```
Optimize on: Jan 2020 - Dec 2022
Test on:     Jan 2023 - Dec 2023  ✅ Unseen data!
```

#### 2. Test Multiple Assets

**Single Asset (WRONG):**
- Optimize on EURUSD
- Perfect results!
- Fails on all other pairs ❌

**Multiple Assets (RIGHT):**
- Test on: EURUSD, GBPUSD, USDJPY, AUDUSD
- If it works on all = more robust ✅

#### 3. Test Multiple Timeframes

**Single TF (WRONG):**
- Works on 1H only ❌

**Multiple TFs (RIGHT):**
- Test on: 15M, 30M, 1H, 4H
- Similar performance = good sign ✅

#### 4. Use Round Numbers

**Overfitted (WRONG):**
```pine
maLength = 23.7  // Too specific!
rsiLevel = 67.3
```

**Robust (RIGHT):**
```pine
maLength = 20    // Round number
rsiLevel = 70    // Standard level
```

#### 5. Limit Parameters

**Too Complex (WRONG):**
- 10+ input parameters
- Each optimized individually
- Perfect on one data set

**Simple (RIGHT):**
- 3-5 key parameters
- Use standard values (14, 20, 50, 200)
- Slight changes don't drastically affect results

---

## Key Metrics to Evaluate

### 1. Net Profit
**What it tells you:** Total profit/loss
**Good:** Positive after costs
**Be careful:** Doesn't show risk or consistency

### 2. Profit Factor
**Formula:** Gross Profit ÷ Gross Loss
**Good:** > 1.5
**Excellent:** > 2.0
**Suspicious:** > 5.0 (might be overfitted)

### 3. Win Rate
**Formula:** Winning Trades ÷ Total Trades
**Good:** 40-60%
**Be careful:** 
- > 80% often means tight targets
- < 30% needs very large winners

### 4. Max Drawdown
**What it tells you:** Largest peak-to-trough decline
**Good:** < 20%
**Acceptable:** 20-30%
**Risky:** > 30%

**Critical:** Can you psychologically handle this drawdown?

### 5. Sharpe Ratio
**What it tells you:** Risk-adjusted returns
**Good:** > 1.0
**Excellent:** > 2.0
**Note:** Only available on TradingView premium

### 6. Average Trade
**Formula:** Net Profit ÷ Number of Trades
**Must exceed:** Commissions + Slippage + Buffer

### 7. Consecutive Losses
**What it tells you:** Longest losing streak
**Important:** Can you survive this mentally and financially?

---

## Sample Size Requirements

### Minimum Trade Count

❌ **Too few:**
- 10-20 trades = statistically insignificant
- Results likely due to chance

✅ **Sufficient:**
- 100+ trades = starting to be meaningful
- 300+ trades = statistically significant
- 1000+ trades = very confident

### Time Periods

❌ **Too short:**
- 1 month of data
- Doesn't cover different market conditions

✅ **Sufficient:**
- 2-3 years minimum
- Includes bull, bear, ranging markets
- Multiple economic cycles

---

## Realistic Expectations

### Performance Degradation

Expect real trading to be **30-50% worse** than backtest:

| Backtest | Real Trading (Conservative) |
|----------|----------------------------|
| 50% annual return | 25-35% annual return |
| 60% win rate | 45-50% win rate |
| 2.0 profit factor | 1.5-1.7 profit factor |
| 15% max DD | 20-25% max DD |

### Why the Degradation?

1. **Psychological factors** (fear, greed, impatience)
2. **Execution differences** (slippage, rejections)
3. **Market changes** (volatility, correlations)
4. **Costs underestimated** (forgot something)
5. **Curve fitting** (some overfitting always exists)

---

## Testing Checklist

Before going live with any strategy:

### ✅ Backtest Phase
- [ ] Tested on 2+ years of data
- [ ] Tested on 3+ different symbols
- [ ] Tested on 2+ timeframes
- [ ] Included realistic commissions
- [ ] Included realistic slippage
- [ ] 100+ trades in sample
- [ ] Max DD is acceptable
- [ ] Profit factor > 1.5
- [ ] Results make logical sense

### ✅ Forward Test Phase
- [ ] Paper traded for 1-3 months
- [ ] Signals match backtest expectations
- [ ] No repainting issues discovered
- [ ] Can execute trades as planned
- [ ] Psychological comfort maintained
- [ ] Performance within expected range

### ✅ Live Phase
- [ ] Start with minimum position size
- [ ] Trade only during optimal conditions
- [ ] Keep detailed trade journal
- [ ] Review weekly performance
- [ ] Stick to the plan (no revenge trading)
- [ ] Accept that drawdowns will happen

---

## Strategy Iteration Workflow

### 1. Initial Development
- Build basic logic
- Test on one asset/timeframe
- Get initial results

### 2. Robustness Testing
- Test on multiple assets
- Test on multiple timeframes
- Add realistic costs

### 3. Refinement
- Simplify overly complex logic
- Remove redundant parameters
- Add essential filters only

### 4. Validation
- Walk-forward test
- Out-of-sample test
- Live paper trading

### 5. Live Trading
- Start small
- Scale gradually
- Continuously monitor

---

## Common Mistakes

### ❌ The "Optimizer" Trap
```
"I found that MA lengths of 23 and 47 work best!"
```
**Problem:** Overfitted to specific historical data
**Solution:** Use standard values (20, 50, 200) and test robustness

### ❌ The "Perfect Backtest" Trap
```
"My strategy has 95% win rate!"
```
**Problem:** Too good to be true = overfitted or lookahead bias
**Solution:** Check for repainting, realistic costs, logic errors

### ❌ The "Single Asset" Trap
```
"Works great on BTC/USD!"
```
**Problem:** Might be capturing one asset's quirk, not a real edge
**Solution:** Test on 5+ similar assets

### ❌ The "Ignore Reality" Trap
```
Commissions = 0, Slippage = 0
```
**Problem:** Real trading will be much worse
**Solution:** Use conservative estimates for all costs

---

## Example Strategy Configuration

### Conservative Setup (Recommended):

```pine
strategy("My Strategy",
    overlay = true,
    initial_capital = 10000,
    default_qty_type = strategy.percent_of_equity,
    default_qty_value = 10,  // 10% of equity per trade
    commission_type = strategy.commission.percent,
    commission_value = 0.1,  // 0.1% per side
    slippage = 3,            // 3 ticks
    process_orders_on_close = true,
    calc_on_every_tick = false,
    calc_on_order_fills = false,
    pyramiding = 0)          // One position at a time
```

---

## Next Steps

### Practice:
1. Open any strategy from [`strategies/`](../../strategies/)
2. Test with different commission values (0%, 0.1%, 0.2%)
3. Observe how performance changes
4. Test on different symbols
5. Compare results

### Further Learning:
- [`docs/faq.md`](../../docs/faq.md) - Common questions
- [`strategies/strategies-overview.md`](../../strategies/strategies-overview.md) - Strategy guide
- [TradingView Strategy Tester](https://www.tradingview.com/support/solutions/43000481656) - Official docs

---

## Final Thoughts

### The Hard Truth:

> "In backtesting, everything works. In paper trading, most things work. In live trading, few things work."

### The Goal:

Backtesting isn't about finding the "perfect" system. It's about:

✅ Understanding if your idea has merit
✅ Identifying major flaws before risking capital
✅ Setting realistic expectations
✅ Building confidence in your approach

### Remember:

- **Past performance ≠ Future results**
- **Paper trading ≠ Real trading**
- **Emotions matter more than you think**
- **Simple systems often outperform complex ones**
- **Risk management is more important than entries**

---

**Congratulations!** You now understand how to conduct meaningful backtests. Always test thoroughly, expect degradation, and never risk more than you can afford to lose.
