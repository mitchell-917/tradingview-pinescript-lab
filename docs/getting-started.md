# 🚀 Getting Started with TradingView Pine Script Lab

Welcome to **TradingView Pine Script Lab** – your comprehensive learning resource for mastering Pine Script v5. This guide will walk you through everything you need to start building indicators and strategies like a pro.

---

## 📋 Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Understanding the Repository Structure](#2-understanding-the-repository-structure)
3. [Loading Your First Script](#3-loading-your-first-script)
4. [Pine Script Fundamentals](#4-pine-script-fundamentals)
5. [Recommended Learning Path](#5-recommended-learning-path)
6. [Common Pitfalls & Solutions](#6-common-pitfalls--solutions)
7. [Getting Help](#7-getting-help)

---

## 1. Prerequisites

### **What You'll Need:**

✅ **TradingView Account**
- Free account works for most examples
- Premium features (higher timeframes, custom alerts) require paid plans
- Sign up at [tradingview.com](https://www.tradingview.com/)

✅ **Web Browser**
- Chrome, Firefox, Safari, or Edge
- Modern browser with JavaScript enabled
- Stable internet connection

✅ **Basic Chart Knowledge**
- Understanding of candlesticks and OHLC data
- Familiarity with timeframes (1m, 5m, 1H, 1D, etc.)
- Basic trading concepts (support/resistance, trends)

### **Optional But Helpful:**

- Programming experience (any language helps but not required)
- Understanding of technical indicators (MA, RSI, etc.)
- Trading experience (to better understand use cases)

---

## 2. Understanding the Repository Structure

This repository is organized for **progressive learning**. Here's what each folder contains:

### 📊 **`indicators/`**

Ready-to-use visual tools that plot on your charts:

- **Trend Tools:** Moving averages, market structure
- **Oscillators:** RSI, volatility bands
- **Levels:** Support/resistance, session highs/lows
- **Advanced:** Liquidity sweeps, volume profiles

**Start here if:** You want to learn Pine Script fundamentals

### 📈 **`strategies/`**

Backtestable trading systems with entries, exits, and risk management:

- **Trend Following:** MA crossover systems
- **Mean Reversion:** RSI-based counter-trend trades
- **Breakout:** Session and liquidity-based entries
- **Advanced:** Event-driven reversal strategies

**Start here if:** You already know Pine basics and want to build trading systems

### 🧩 **`examples/`**

Templates, snippets, and tutorials:

- **`templates/`** - Starter files for new projects
- **`snippets/`** - Reusable code patterns
- **`tutorials/`** - Step-by-step guides

**Start here if:** You want structured, guided learning

### 📖 **`docs/`**

Comprehensive documentation:

- Style guides and conventions
- Version compatibility info
- FAQ and troubleshooting
- Deep-dive explanations

**Reference these:** Whenever you need clarification

---

## 3. Loading Your First Script

Let's load your first indicator step-by-step:

### **Step 1: Open TradingView**

1. Go to [tradingview.com](https://www.tradingview.com/)
2. Log in to your account
3. Click **"Chart"** to open the charting interface
4. Select any symbol (e.g., SPY, EURUSD, BTCUSD)

### **Step 2: Open the Pine Editor**

1. Look at the bottom of the screen
2. Click the **"Pine Editor"** tab
3. You'll see a split-screen: chart on top, editor on bottom

### **Step 3: Load a Script**

1. In this repository, open `indicators/ma-crossover-indicator.pine`
2. **Select all** the code (Ctrl+A / Cmd+A)
3. **Copy** it (Ctrl+C / Cmd+C)
4. In TradingView's Pine Editor, **paste** the code
5. Click **"Save"** (give it a name like "My MA Crossover")

### **Step 4: Add to Chart**

1. Click the **"Add to Chart"** button (next to Save)
2. The indicator will appear on your chart
3. You'll see two moving averages and crossover signals

### **Step 5: Customize**

1. Click the **gear icon** ⚙️ next to the indicator name
2. Experiment with the settings:
   - Change MA lengths (try 20 & 50)
   - Switch MA types (SMA → EMA)
   - Toggle visual elements
3. Click **"OK"** to apply changes

### **🎉 Congratulations!**

You just loaded your first Pine Script indicator. Now let's understand how it works.

---

## 4. Pine Script Fundamentals

Every Pine Script has these core components:

### **A. Version Declaration**

```pine
//@version=5
```

**What it does:** Tells TradingView which Pine Script version you're using

**Why it matters:** v5 is the current version with modern syntax and features

**Rule:** Always put this as the **first line** of your script

---

### **B. Script Declaration**

```pine
indicator("My Indicator Name", overlay = true)
```

or

```pine
strategy("My Strategy Name", overlay = true, initial_capital = 10000)
```

**Key differences:**

| Feature | `indicator()` | `strategy()` |
|---------|---------------|--------------|
| Purpose | Visual tools only | Backtestable systems |
| Can plot | ✅ Yes | ✅ Yes |
| Can trade | ❌ No | ✅ Yes |
| Shows in | Chart or pane | Chart + Strategy Tester |

**Parameters:**

- **`overlay = true`** - Draws on price chart (for MAs, levels, structure)
- **`overlay = false`** - Separate pane below chart (for RSI, oscillators)
- **`max_labels_count`** - How many labels to show (default 50)
- **`max_lines_count`** - How many lines to draw (default 50)

---

### **C. Inputs**

```pine
length = input.int(14, "Length", minval = 1, maxval = 200)
source = input.source(close, "Source")
showLabels = input.bool(true, "Show Labels")
```

**What they do:** Create user-configurable settings in the indicator's settings panel

**Common input types:**

| Type | Example | Use Case |
|------|---------|----------|
| `input.int()` | Lengths, periods, lookbacks | `input.int(14, "RSI Length")` |
| `input.float()` | Multipliers, thresholds | `input.float(2.0, "ATR Mult")` |
| `input.bool()` | Toggle features on/off | `input.bool(true, "Show Alerts")` |
| `input.string()` | Dropdown selections | `input.string("EMA", options=["SMA","EMA"])` |
| `input.source()` | Choose price data | `input.source(close, "Source")` |
| `input.color()` | Color pickers | `input.color(color.blue, "Line Color")` |
| `input.timeframe()` | Timeframe selection | `input.timeframe("D", "HTF")` |
| `input.session()` | Session times | `input.session("0930-1600", "NY")` |

**Best practice:** Group related inputs together:

```pine
groupTrend = "Trend Settings"
maLength = input.int(50, "MA Length", group = groupTrend)
maType = input.string("EMA", "MA Type", group = groupTrend)
```

---

### **D. Calculations**

```pine
// Simple moving average
sma = ta.sma(close, 20)

// RSI
rsi = ta.rsi(close, 14)

// ATR
atr = ta.atr(14)

// Custom calculation
customValue = (high + low) / 2
```

**Built-in technical analysis functions (`ta.*`):**

| Function | Description | Example |
|----------|-------------|---------|
| `ta.sma()` | Simple moving average | `ta.sma(close, 20)` |
| `ta.ema()` | Exponential moving average | `ta.ema(close, 12)` |
| `ta.rsi()` | Relative Strength Index | `ta.rsi(close, 14)` |
| `ta.atr()` | Average True Range | `ta.atr(14)` |
| `ta.stdev()` | Standard deviation | `ta.stdev(close, 20)` |
| `ta.highest()` | Highest value in period | `ta.highest(high, 10)` |
| `ta.lowest()` | Lowest value in period | `ta.lowest(low, 10)` |
| `ta.crossover()` | Series crosses above | `ta.crossover(fast, slow)` |
| `ta.crossunder()` | Series crosses below | `ta.crossunder(fast, slow)` |

**Series:** Pine Script operates on **series** - values that exist for every bar in history

---

### **E. Conditions**

```pine
// Simple condition
bullish = close > open

// Crossover detection
maCross = ta.crossover(fastMA, slowMA)

// Multiple conditions
buySignal = close > ma and rsi < 30 and volume > ta.sma(volume, 20)

// Conditional assignment
color barColor = close > open ? color.green : color.red
```

**Comparison operators:**

- `>` greater than
- `<` less than
- `>=` greater than or equal
- `<=` less than or equal
- `==` equal to
- `!=` not equal to

**Logical operators:**

- `and` - both conditions must be true
- `or` - at least one condition must be true
- `not` - inverts the condition

---

### **F. Plotting**

```pine
// Line plot
plot(sma, "20 SMA", color = color.blue, linewidth = 2)

// Shapes
plotshape(buySignal, "Buy", shape.triangleup, location.belowbar, color.green)

// Background color
bgcolor(bullish ? color.new(color.green, 90) : na)

// Horizontal line
hline(0, "Zero Line", color.gray)

// Labels (for text)
label.new(bar_index, high, "Important Level", style = label.style_label_down)
```

**Plotting tips:**

- Use `color.new(color.blue, 50)` for transparency (0 = opaque, 100 = invisible)
- `location.belowbar` / `location.abovebar` for shapes relative to price
- `plot.style_line` / `plot.style_stepline` / `plot.style_histogram` for different styles
- `na` (not available) to hide plots conditionally

---

### **G. Alerts**

```pine
alertcondition(
    buySignal,
    title = "Buy Signal",
    message = "MA crossover detected - potential buy opportunity"
)
```

**How to use alerts:**

1. Right-click on chart
2. Select "Add alert"
3. Choose your indicator
4. Select the specific alert condition
5. Configure notification method (pop-up, email, webhook)

---

## 5. Recommended Learning Path

Follow this path for structured, progressive learning:

### 🟢 **Phase 1: Absolute Beginner (Week 1-2)**

**Goal:** Understand Pine Script basics and structure

**Path:**

1. **Read:** This guide thoroughly
2. **Load:** `indicators/ma-crossover-indicator.pine`
   - Study every line and comment
   - Change parameters and observe results
   - Try different MA types and lengths
3. **Load:** `indicators/rsi-basic-indicator.pine`
   - Understand oscillators and separate panes
   - Experiment with OB/OS levels
4. **Tutorial:** `examples/tutorials/01_basic_indicator_walkthrough.md`
5. **Practice:** Use `examples/templates/indicator-template.pine` to build a simple SMA indicator

**Milestone:** You can read and modify existing indicators

---

### 🟡 **Phase 2: Intermediate (Week 3-4)**

**Goal:** Build more complex indicators with multiple features

**Path:**

1. **Study:** `indicators/support-resistance-zones.pine`
   - Learn about pivots, arrays, and dynamic lines
2. **Study:** `indicators/volatility-band-indicator.pine`
   - Understand standard deviation and bands
3. **Study:** `indicators/mtf-trend-dashboard.pine`
   - Learn `request.security()` for multiple timeframes
4. **Tutorial:** `examples/tutorials/02_basic_strategy_walkthrough.md`
5. **Load:** `strategies/ma-crossover-strategy.pine`
   - Understand strategy structure
   - Learn about position sizing and risk management
6. **Practice:** Build a strategy combining MA and RSI filters

**Milestone:** You can build indicators from scratch and understand strategy basics

---

### 🔴 **Phase 3: Advanced (Week 5+)**

**Goal:** Master sophisticated techniques and patterns

**Path:**

1. **Study:** `indicators/market-structure-tool.pine`
   - Advanced use of arrays and state tracking
   - Swing high/low classification
2. **Study:** `indicators/liquidity-sweep-detector.pine`
   - Complex conditional logic
   - Market microstructure concepts
3. **Study:** `indicators/volume-profile-lite.pine`
   - Custom data structures
   - Performance optimization techniques
4. **Tutorial:** `examples/tutorials/03_no-repaint_tips_and_tricks.md`
5. **Tutorial:** `examples/tutorials/04_backtesting_best_practices.md`
6. **Load:** `strategies/liquidity-sweep-reversal-strategy.pine`
   - Event-driven strategy logic
7. **Practice:** Create your own unique indicator combining multiple concepts

**Milestone:** You can architect sophisticated, production-ready trading tools

---

## 6. Common Pitfalls & Solutions

### ❌ **Problem: "Undeclared identifier"**

**Cause:** Using a variable before defining it

**Solution:**
```pine
// Wrong:
plot(myMA, "MA")
myMA = ta.sma(close, 20)

// Correct:
myMA = ta.sma(close, 20)
plot(myMA, "MA")
```

---

### ❌ **Problem: "Cannot call 'plot' in local scope"**

**Cause:** Using `plot()` inside an `if` statement

**Solution:**
```pine
// Wrong:
if close > open
    plot(close, "Close")

// Correct:
plotValue = close > open ? close : na
plot(plotValue, "Close")
```

---

### ❌ **Problem: Script shows signals historically but not in real-time**

**Cause:** Repainting behavior (pivots, security calls with lookahead)

**Solution:** Read `examples/tutorials/03_no-repaint_tips_and_tricks.md`

---

### ❌ **Problem: "Loop is too long to execute"**

**Cause:** Loop iterating over too many bars

**Solution:**
```pine
// Limit loop iterations
maxBars = 500
for i = 0 to math.min(maxBars, bar_index)
    // Your logic
```

---

### ❌ **Problem: Charts loading slowly**

**Cause:** Too many labels, lines, or boxes

**Solution:**
```pine
// Set limits in indicator declaration
indicator("My Indicator", max_labels_count = 100, max_lines_count = 100)

// Delete old objects
if array.size(myArray) > 50
    label.delete(array.shift(myArray))
```

---

## 7. Getting Help

### **In This Repository:**

- 📖 **[FAQ](faq.md)** - Common questions answered
- 📚 **[Pine Style Guide](pine-style-guide.md)** - Coding standards
- 🔍 **[Repository Overview](repository-overview.md)** - Detailed structure explanation

### **Official Resources:**

- 📘 [Pine Script v5 Documentation](https://www.tradingview.com/pine-script-docs/)
- 📗 [Pine Script v5 Reference](https://www.tradingview.com/pine-script-reference/v5/)
- 💬 [TradingView Community](https://www.tradingview.com/scripts/)

### **Community:**

- **GitHub Issues:** Report bugs or request features
- **GitHub Discussions:** Ask questions and share ideas
- **TradingView Chat:** Connect with other Pine Script developers

---

## 🎯 Next Steps

Now that you understand the basics, choose your path:

1. **Want to learn systematically?**
   → Follow the [Recommended Learning Path](#5-recommended-learning-path) above

2. **Want to build something specific?**
   → Check the [Repository Structure](#2-understanding-the-repository-structure) and jump to relevant scripts

3. **Want templates to start quickly?**
   → Use files in `examples/templates/`

4. **Want to understand best practices?**
   → Read the [Pine Style Guide](pine-style-guide.md)

---

<div align="center">

**Ready to start coding?**

[⬅ Back to Main README](../README.md) | [Next: Pine Style Guide →](pine-style-guide.md)

</div>
