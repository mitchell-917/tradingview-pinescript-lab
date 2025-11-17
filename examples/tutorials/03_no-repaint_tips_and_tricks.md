# Tutorial 03 – No-Repaint Tips & Tricks

Understanding repainting is crucial for developing reliable trading indicators and strategies. This guide explains what repainting is, why it happens, and how to avoid it.

## What is Repainting?

**Repainting** occurs when an indicator's historical signals differ from what appeared in real-time. This creates a false sense of accuracy and can lead to poor trading decisions.

### Example of Repainting:

**Real-Time (Bar in Progress):**
- Signal appears: "Buy at $100"
- You prepare to enter the trade

**After Bar Closes:**
- Signal disappears or moves
- Historical chart shows no signal at $100

**Result:** You can't actually trade the signals you see historically

---

## Common Sources of Repainting

### 1. Pivot-Based Indicators

**The Issue:**
Pivots require bars on both sides for confirmation:

```pine
swingHigh = ta.pivothigh(high, 5, 5)
// Needs 5 bars AFTER the high to confirm
```

**Why It Repaints:**
- Historically: Perfect pivots marked exactly at the extreme
- Real-Time: Must wait 5 bars after the high before signal appears

**Scripts Affected:**
- [`support-resistance-zones.pine`](../../indicators/support-resistance-zones.pine)
- [`market-structure-tool.pine`](../../indicators/market-structure-tool.pine)
- [`rsi-divergence-detector.pine`](../../indicators/rsi-divergence-detector.pine)

**Solution:**
Accept the delay as inherent to the technique. These indicators are still valuable but:
- Use for analysis, not instant signals
- Combine with real-time confirmation
- Understand signals are delayed by design

---

### 2. Higher Timeframe Data (request.security)

**The Issue:**
Improper use of `request.security()` can peek into the future:

```pine
// WRONG - Can repaint!
htfClose = request.security(syminfo.tickerid, "D", close)

// CORRECT - No repaint
htfClose = request.security(syminfo.tickerid, "D", close,
     lookahead = barmerge.lookahead_off)
```

**Why It Repaints:**
Without `lookahead_off`, the function can access data from incomplete higher timeframe bars

**Scripts Done Right:**
All scripts in this repo use `lookahead = barmerge.lookahead_off`:
- [`multi-timeframe-trend-analyzer.pine`](../../indicators/multi-timeframe-trend-analyzer.pine)
- [`mtf-trend-dashboard.pine`](../../indicators/mtf-trend-dashboard.pine)

**Best Practice:**
```pine
// Always include these parameters
htfData = request.security(
    syminfo.tickerid,
    "D",
    close,
    lookahead = barmerge.lookahead_off,
    gaps = barmerge.gaps_off
)
```

---

### 3. Intrabar Updates (Real-Time Bar)

**The Issue:**
The current bar updates continuously until it closes:

```pine
// Changes as bar progresses
currentHigh = high  

// Only after bar close:
confirmedHigh = high[1]
```

**Why It Repaints:**
- RSI = 72 (signal triggers)
- Bar continues, RSI drops to 68
- Bar closes at 68 (no signal historically)

**Solution - Wait for Bar Close:**

```pine
// Option 1: Reference closed bars only
rsi = ta.rsi(close[1], 14)  // Previous bar

// Option 2: Check if bar is confirmed
if barstate.isconfirmed
    // Only execute on bar close
    if rsi > 70
        buySignal := true
```

**For Alerts:**
Set alert frequency to "Once Per Bar Close" not "Once Per Bar"

---

### 4. calc_on_every_tick

**The Issue:**
```pine
strategy("My Strategy", 
    calc_on_every_tick = true)  // DANGEROUS!
```

**Why It Repaints:**
- Strategies with `calc_on_every_tick = true` recalculate on every price change
- Historical bars only show closed values
- Real-time behavior differs from historical

**Solution:**
```pine
strategy("My Strategy", 
    calc_on_every_tick = false,      // Safe
    calc_on_order_fills = false)     // Safe
```

**All strategies in this repo use safe defaults**

---

## Testing for Repainting

### Method 1: Bar Replay

1. Open TradingView chart
2. Click "Bar Replay" button (clock icon)
3. Step through bars one by one
4. Watch if signals appear/disappear/move

### Method 2: Live Monitoring

1. Add indicator to chart
2. Watch real-time for 1 hour
3. Take screenshots of signals
4. After bars close, compare to historical view
5. Signals should match

### Method 3: Code Review

Check for these red flags:
```pine
// ❌ Potential repainting
request.security(...) // Without lookahead_off
ta.pivothigh(...)     // Inherent delay
calc_on_every_tick = true

// ✅ Non-repainting
request.security(..., lookahead = barmerge.lookahead_off)
barstate.isconfirmed  // Bar close confirmation
close[1]              // Previous closed bar
```

---

## Acceptable "Repainting"

### Not All Repainting Is Bad

Some repainting is acceptable for specific uses:

**1. Dashboard Data (Current Bar):**
```pine
// Real-time price display - OKAY to update
currentPrice = close  // Updates as bar progresses
```

**2. Visualization (Not Trading):**
```pine
// Drawing current channel - OKAY to redraw
upper = ta.highest(high, 20)  // Moves with price
```

**3. Alerts (With Understanding):**
- Use "Once Per Bar Close" frequency
- Understand you'll only know after the fact
- Don't expect instant entries

---

## Scripts in This Repo

### ✅ Non-Repainting:
- [`ma-crossover-indicator.pine`](../../indicators/ma-crossover-indicator.pine)
- [`rsi-basic-indicator.pine`](../../indicators/rsi-basic-indicator.pine)
- [`volatility-band-indicator.pine`](../../indicators/volatility-band-indicator.pine)
- [`session-high-low-indicator.pine`](../../indicators/session-high-low-indicator.pine)
- All strategies (when `calc_on_every_tick = false`)

### ⚠️ Delayed Confirmation (By Design):
- [`support-resistance-zones.pine`](../../indicators/support-resistance-zones.pine) - Pivot-based
- [`market-structure-tool.pine`](../../indicators/market-structure-tool.pine) - Swing identification
- [`rsi-divergence-detector.pine`](../../indicators/rsi-divergence-detector.pine) - Pivot comparison
- [`smart-money-concepts.pine`](../../indicators/smart-money-concepts.pine) - Structure breaks

**Note:** These scripts clearly document their behavior in header comments

---

## Best Practices Summary

### ✅ DO:
- Use `barstate.isconfirmed` for real-time logic
- Add `lookahead = barmerge.lookahead_off` to all `request.security()`
- Set alerts to "Once Per Bar Close"
- Test with Bar Replay
- Document any delayed signals in comments
- Reference closed bars `close[1]` for critical decisions

### ❌ DON'T:
- Use `calc_on_every_tick = true` unless you understand implications
- Rely on current bar values for backtest logic
- Assume pivot signals appear instantly
- Use `lookahead_on` for trading signals
- Ignore the difference between real-time and historical behavior

---

## Next Steps

✅ **Tutorial 04:** [`04_backtesting_best_practices.md`](04_backtesting_best_practices.md)
- Learn to avoid overfitting
- Proper testing methodology
- Realistic performance expectations

📚 **Further Reading:**
- [`docs/faq.md`](../../docs/faq.md#3-are-these-scripts-no-repaint) - FAQ on repainting
- [TradingView Repainting Guide](https://www.tradingview.com/pine-script-docs/en/v5/concepts/Repainting.html)

---

## Key Takeaway

**Perfect historical signals don't guarantee real-time profitability.**

Always:
1. Understand WHY an indicator behaves a certain way
2. Test in real-time before trading
3. Accept delays when they're inherent to the method
4. Never rely solely on historical backtest results

**Remember:** An indicator that looks "worse" historically but doesn't repaint is far more valuable than one with perfect historical signals that can't be traded in real-time.
