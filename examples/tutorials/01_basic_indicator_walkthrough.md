# Tutorial 01 – Building Your First Indicator

A step-by-step walkthrough of creating and modifying a simple moving average crossover indicator.

## Learning Objectives

By the end of this tutorial, you will:
- Understand basic Pine Script structure
- Know how to use inputs, calculations, and plotting
- Be able to modify and customize indicators
- Create your first alert conditions

---

## Step 1: Load the Example

1. Navigate to [`indicators/ma-crossover-indicator.pine`](../../indicators/ma-crossover-indicator.pine)
2. Read the comprehensive header comments explaining the concept
3. Copy the entire script
4. Open [TradingView](https://www.tradingview.com/) Pine Editor
5. Paste the code and click "Add to Chart"

---

## Step 2: Understand the Structure

### The Four Main Sections:

#### **1. Inputs** (Lines ~19-35)
```pine
fastLen = input.int(9, "Fast MA Length", minval = 1)
slowLen = input.int(21, "Slow MA Length", minval = 1)
```
**What it does:** Creates user-configurable settings in the indicator's settings panel

#### **2. Calculations** (Lines ~40-50)
```pine
fastMA = ta.ema(close, fastLen)
slowMA = ta.ema(close, slowLen)
```
**What it does:** Computes the moving averages using TradingView's built-in functions

#### **3. Conditions** (Lines ~55-65)
```pine
bullCross = ta.crossover(fastMA, slowMA)
bearCross = ta.crossunder(fastMA, slowMA)
```
**What it does:** Detects when crossovers occur

#### **4. Plotting** (Lines ~70-85)
```pine
plot(fastMA, "Fast MA", color = fastColor)
plotshape(bullCross, style = shape.triangleup)
```
**What it does:** Draws everything on the chart

---

## Step 3: Make Your First Modification

### Change the MA Type

**Original:**
```pine
fastMA = ta.ema(close, fastLen)  // Exponential Moving Average
```

**Try changing to:**
```pine
fastMA = ta.sma(close, fastLen)  // Simple Moving Average
```

**What happens:** The line becomes less responsive to recent price changes

### Adjust the Lengths

**Default:** 9 and 21 (short-term trend)
**Try:** 50 and 200 (long-term trend)

**What happens:** Fewer signals, but potentially more significant

---

## Step 4: Add a Background Color

Add this code after the conditions section:

```pine
// Color background when bullish
bgColor = bullCross ? color.new(color.lime, 90) : 
         bearCross ? color.new(color.red, 90) : na
bgcolor(bgColor, title = "Crossover Background")
```

**Result:** Chart background briefly colors when crossovers occur

---

## Step 5: Understanding Alerts

Find these lines in the script:
```pine
alertcondition(bullCross, "Bullish MA Crossover", 
     "Fast MA crossed ABOVE slow MA.")
```

**To set up alerts:**
1. Right-click on the chart → "Add Alert"
2. Select your indicator from the Condition dropdown
3. Choose "Bullish MA Crossover"
4. Configure frequency ("Once Per Bar Close" recommended)
5. Click "Create"

---

## Step 6: Experimentation Ideas

### Easy Modifications:
- Change colors in the Visual inputs group
- Adjust MA lengths to find optimal values for your asset
- Try different MA types (WMA, RMA)

### Intermediate Challenges:
- Add a third MA for additional confirmation
- Create a histogram showing distance between fast/slow MA
- Add volume filter (only signal on high volume crosses)

### Advanced Extensions:
- Implement higher timeframe MA filter
- Add ATR-based signal strength indicator
- Create multi-timeframe alignment dashboard

---

## Next Steps

✅ **Tutorial 02:** [`02_basic_strategy_walkthrough.md`](02_basic_strategy_walkthrough.md)
- Convert this indicator into a backtestable strategy
- Add entry/exit logic and risk management

📚 **Further Reading:**
- [`docs/getting-started.md`](../../docs/getting-started.md) - Complete Pine Script fundamentals
- [`docs/pine-style-guide.md`](../../docs/pine-style-guide.md) - Best practices and conventions

---

## Common Issues & Solutions

**Problem:** Script won't compile
**Solution:** Check that you copied the entire file, including `//@version=5`

**Problem:** No plots visible
**Solution:** Verify the indicator is added to the chart and overlay = true

**Problem:** Crossover signals don't appear
**Solution:** MA lengths may be too long for your timeframe - try shorter periods

---

**Congratulations!** You've completed your first Pine Script tutorial. Keep experimenting!
