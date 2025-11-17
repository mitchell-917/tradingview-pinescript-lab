# 📊 TradingView Pine Script Lab

> **A comprehensive, production-quality learning resource for mastering Pine Script v5**

[![Pine Script v5](https://img.shields.io/badge/Pine%20Script-v5-blue)](https://www.tradingview.com/pine-script-docs/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

---

## 🎯 What is This?

**TradingView Pine Script Lab** is a meticulously crafted educational repository designed to help traders and developers **master Pine Script v5** through practical, real-world examples. Whether you're building your first indicator or developing sophisticated trading strategies, this repository provides clean, well-documented reference implementations that follow industry best practices.

### 🌟 Why This Repository Stands Out

- **📚 Production-Ready Code** - Every script is written with clarity, maintainability, and best practices in mind
- **🎓 Educational First** - Extensive inline comments explain not just *what* the code does, but *why* it works
- **🔬 Progressive Learning** - Structured path from basic concepts to advanced techniques
- **⚡ Copy-Paste Ready** - All scripts work out-of-the-box in TradingView
- **🛠️ Real-World Applications** - Practical tools you can actually use and customize for your trading
- **📈 Comprehensive Coverage** - Indicators, strategies, utilities, and design patterns

---

## 🚀 Quick Start

### 1. **Choose Your Path**

```
New to Pine Script?     → Start with indicators/ma-crossover-indicator.pine
Have some experience?   → Explore indicators/liquidity-sweep-detector.pine
Ready for strategies?   → Jump into strategies/ma-crossover-strategy.pine
```

### 2. **Load a Script**

1. Open [TradingView](https://www.tradingview.com/)
2. Click **Pine Editor** (bottom of screen)
3. Copy any `.pine` file from this repo
4. Paste into the editor
5. Click **Save** → **Add to chart**

### 3. **Start Learning!**

Each script includes:
- **Header comments** explaining the concept
- **Inline documentation** for every key section
- **Study ideas** to extend your learning
- **Practical tips** for customization

---

## 📁 Repository Structure

```
tradingview-pinescript-lab/
│
├── 📖 docs/                          # In-depth guides and references
│   ├── getting-started.md            # Your first steps with Pine Script
│   ├── pine-style-guide.md           # Code formatting & conventions
│   ├── repository-overview.md        # Detailed repo navigation
│   ├── versioning-and-compat.md      # Pine Script versions explained
│   └── faq.md                        # Common questions answered
│
├── 📊 indicators/                    # Ready-to-use indicators
│   ├── ma-crossover-indicator.pine           # Moving average crossovers
│   ├── rsi-basic-indicator.pine              # RSI with OB/OS zones
│   ├── rsi-divergence-detector.pine          # 🆕 Automatic divergence detection
│   ├── support-resistance-zones.pine         # Dynamic S/R levels
│   ├── volatility-band-indicator.pine        # Bollinger-style bands
│   ├── session-high-low-indicator.pine       # Intraday session ranges
│   ├── liquidity-sweep-detector.pine         # Stop hunt identification
│   ├── market-structure-tool.pine            # HH, HL, LH, LL tracking
│   ├── mtf-trend-dashboard.pine              # Multi-timeframe trend overview
│   ├── multi-timeframe-trend-analyzer.pine   # 🆕 Advanced MTF analysis with dashboard
│   ├── smart-money-concepts.pine             # 🆕 Order blocks, FVG, BOS/CHoCH
│   ├── volume-profile-lite.pine              # Simplified volume profile
│   └── indicator-development-guide.md        # How to build indicators
│
├── 📈 strategies/                    # Backtestable trading systems
│   ├── ma-crossover-strategy.pine            # Trend-following MA system
│   ├── rsi-mean-reversion-strategy.pine      # Counter-trend oscillator trades
│   ├── session-breakout-strategy.pine        # Session range breakouts
│   ├── liquidity-sweep-reversal-strategy.pine # Reversal after stop hunts
│   └── strategies-overview.md                # Strategy development guide
│
└── 🧩 examples/                      # Templates & snippets
    ├── templates/                    # Starter files for new scripts
    │   ├── indicator-template.pine
    │   ├── strategy-template.pine
    │   └── library-template.pine
    │
    ├── snippets/                     # Reusable code patterns
    │   ├── alerts/                   # Alert configuration examples
    │   ├── plotting/                 # Visualization techniques
    │   ├── risk-management/          # Position sizing patterns
    │   └── utilities/                # Helper functions & tools
    │
    └── tutorials/                    # Step-by-step walkthroughs
        ├── 01_basic_indicator_walkthrough.md
        ├── 02_basic_strategy_walkthrough.md
        ├── 03_no-repaint_tips_and_tricks.md
        └── 04_backtesting_best_practices.md
```

---

## 🎓 Learning Paths

### 🌱 **Beginner Track** (Start Here!)

Perfect if you're new to Pine Script or programming:

1. **📖 Read:** [`docs/getting-started.md`](docs/getting-started.md)
2. **🔍 Study:** [`indicators/ma-crossover-indicator.pine`](indicators/ma-crossover-indicator.pine)
   - Learn inputs, calculations, and plotting
   - Understand basic conditions and alerts
3. **📊 Explore:** [`indicators/rsi-basic-indicator.pine`](indicators/rsi-basic-indicator.pine)
   - Oscillator concepts
   - Overbought/oversold logic
4. **📚 Follow:** [`examples/tutorials/01_basic_indicator_walkthrough.md`](examples/tutorials/01_basic_indicator_walkthrough.md)

**Goal:** Build confidence with Pine Script syntax and structure

---

### 🌿 **Intermediate Track**

Ready to level up with more complex concepts:

1. **🎯 Learn:** Multi-timeframe analysis with [`indicators/mtf-trend-dashboard.pine`](indicators/mtf-trend-dashboard.pine)
2. **📈 Understand:** Market structure with [`indicators/market-structure-tool.pine`](indicators/market-structure-tool.pine)
3. **⚙️ Master:** Strategy development with [`strategies/ma-crossover-strategy.pine`](strategies/ma-crossover-strategy.pine)
4. **🔄 Apply:** Position sizing patterns from [`examples/snippets/risk-management/`](examples/snippets/risk-management/)

**Goal:** Combine multiple concepts into coherent trading systems

---

### 🌳 **Advanced Track**

Dive into sophisticated techniques:

1. **🎲 Explore:** Liquidity concepts with [`indicators/liquidity-sweep-detector.pine`](indicators/liquidity-sweep-detector.pine)
2. **📊 Build:** Volume analysis with [`indicators/volume-profile-lite.pine`](indicators/volume-profile-lite.pine)
3. **🧪 Test:** Event-driven strategies with [`strategies/liquidity-sweep-reversal-strategy.pine`](strategies/liquidity-sweep-reversal-strategy.pine)
4. **⏱️ Master:** Session-based trading with [`strategies/session-breakout-strategy.pine`](strategies/session-breakout-strategy.pine)

**Goal:** Develop unique, production-ready trading tools

---

## 🔥 Featured Scripts

### 🎯 **Best for Learning**

| Script | Concepts Covered | Difficulty |
|--------|------------------|------------|
| [MA Crossover Indicator](indicators/ma-crossover-indicator.pine) | Inputs, plotting, alerts, conditions | ⭐ Beginner |
| [RSI Basic Indicator](indicators/rsi-basic-indicator.pine) | Oscillators, separate panes, OB/OS logic | ⭐ Beginner |
| [RSI Divergence Detector](indicators/rsi-divergence-detector.pine) | 🆕 Pivot detection, arrays, line drawing, pattern recognition | ⭐⭐ Intermediate |
| [Support & Resistance Zones](indicators/support-resistance-zones.pine) | Pivots, arrays, dynamic lines | ⭐⭐ Intermediate |
| [Multi-Timeframe Trend Analyzer](indicators/multi-timeframe-trend-analyzer.pine) | 🆕 request.security(), MTF analysis, tables, dashboard | ⭐⭐⭐ Advanced |
| [Smart Money Concepts](indicators/smart-money-concepts.pine) | 🆕 Order blocks, FVG, BOS/CHoCH, box drawing | ⭐⭐⭐ Advanced |
| [Liquidity Sweep Detector](indicators/liquidity-sweep-detector.pine) | Advanced conditions, market microstructure | ⭐⭐⭐ Advanced |

### 💼 **Best for Trading**

| Script | Use Case | Key Features |
|--------|----------|--------------|
| [Multi-Timeframe Trend Analyzer](indicators/multi-timeframe-trend-analyzer.pine) | 🆕 Trend alignment | 5 timeframes, 4 methods, visual dashboard |
| [Smart Money Concepts](indicators/smart-money-concepts.pine) | 🆕 ICT-style trading | Order blocks, FVG, liquidity, structure breaks |
| [RSI Divergence Detector](indicators/rsi-divergence-detector.pine) | 🆕 Reversal trading | Auto divergence detection, 4 types |
| [MTF Trend Dashboard](indicators/mtf-trend-dashboard.pine) | Quick trend overview | Multiple timeframes, visual table |
| [Market Structure Tool](indicators/market-structure-tool.pine) | Swing trading | HH/HL/LH/LL identification |
| [Session High/Low](indicators/session-high-low-indicator.pine) | Intraday trading | Session tracking, key levels |
| [MA Crossover Strategy](strategies/ma-crossover-strategy.pine) | Trend following | ATR stops, position sizing |

---

## 💡 Key Features

### ✅ **Code Quality**

- **Consistent Style** - All scripts follow our [Pine Style Guide](docs/pine-style-guide.md)
- **Comprehensive Comments** - Every section is thoroughly documented
- **No Magic Numbers** - All values are configurable inputs
- **Error Handling** - Defensive coding prevents common pitfalls

### ✅ **Educational Value**

- **Progressive Complexity** - Start simple, add sophistication gradually
- **Real Explanations** - Not just *what*, but *why* and *how*
- **Study Ideas** - Suggestions for experimentation in every script
- **Best Practices** - Learn industry-standard approaches

### ✅ **Practical Tools**

- **Production Ready** - Use these scripts as-is or customize them
- **Well-Tested** - All code verified on multiple symbols and timeframes
- **Flexible Design** - Easy to adapt to your trading style
- **Performance Optimized** - Efficient code that won't slow your charts

---

## 🛠️ How to Use This Repository

### **For Learning:**

1. **Follow the learning paths** above based on your experience
2. **Read the code** - don't just copy-paste, understand each line
3. **Experiment** - change parameters, add features, break things (safely!)
4. **Build projects** - combine concepts to create your own unique tools

### **For Development:**

1. **Use as templates** - start new projects from our template files
2. **Reference implementations** - see how to properly implement complex features
3. **Code snippets** - copy reusable patterns for your scripts
4. **Style guide** - maintain consistent, readable code

### **For Trading:**

1. **Test thoroughly** - backtest on multiple markets and timeframes
2. **Customize** - adapt parameters and logic to your strategy
3. **Paper trade** - verify behavior in real-time before risking capital
4. **Risk management** - always use proper position sizing and stops

---

## 📖 Core Concepts Explained

### **Indicators vs Strategies**

- **Indicators** (`indicator()`) - Visual tools, no order execution
- **Strategies** (`strategy()`) - Backtestable systems with entries/exits

### **Overlay vs Separate Pane**

- **Overlay = true** - Plots on the price chart (MAs, S/R levels)
- **Overlay = false** - Separate window below chart (RSI, MACD)

### **No-Repaint Considerations**

Many techniques (pivots, higher timeframes) can show different signals in real-time vs historically. We document these behaviors clearly in affected scripts. See [`examples/tutorials/03_no-repaint_tips_and_tricks.md`](examples/tutorials/03_no-repaint_tips_and_tricks.md) for details.

---

## ⚠️ Important Disclaimers

### **Educational Purpose**

All scripts in this repository are provided for **educational and research purposes only**. They are not:

- ❌ Financial advice
- ❌ Guaranteed profitable
- ❌ Suitable for all markets or timeframes
- ❌ Ready for live trading without thorough testing

### **Risk Warning**

Trading financial instruments involves substantial risk. You should:

- ✅ Test extensively in paper trading mode
- ✅ Understand the logic and assumptions
- ✅ Never risk more than you can afford to lose
- ✅ Consult with financial professionals before trading

---

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### **Ways to Contribute:**

- 🐛 **Report bugs** - Found an issue? Open an issue
- 💡 **Suggest features** - Have an idea? Share it
- 📝 **Improve docs** - Make explanations clearer
- 🔧 **Submit scripts** - Add new examples or improvements
- ⭐ **Star this repo** - Help others discover it

### **Contribution Guidelines:**

1. Follow the [Pine Style Guide](docs/pine-style-guide.md)
2. Include comprehensive comments
3. Test on multiple symbols and timeframes
4. Add educational notes explaining the concept
5. Submit a pull request with clear description

---

## 📚 Additional Resources

### **Official Documentation**

- [Pine Script v5 Documentation](https://www.tradingview.com/pine-script-docs/)
- [Pine Script v5 Reference](https://www.tradingview.com/pine-script-reference/v5/)
- [TradingView Community](https://www.tradingview.com/scripts/)

### **Learning Resources**

- [Pine Script Tutorial Series](https://www.tradingview.com/pine-script-docs/en/v5/Introduction.html)
- [TradingView Blog](https://www.tradingview.com/blog/en/)

### **This Repository's Guides**

- [Getting Started Guide](docs/getting-started.md)
- [Indicator Development Guide](indicators/indicator-development-guide.md)
- [Strategy Overview](strategies/strategies-overview.md)
- [FAQ](docs/faq.md)

---

## 🎯 Roadmap

### **Coming Soon:**

- [ ] Advanced order flow indicators
- [ ] Machine learning integration examples
- [ ] Multi-asset portfolio strategies
- [ ] Custom charting libraries
- [ ] Video tutorial series
- [ ] Interactive code playground

### **Under Consideration:**

- [ ] Pine Script v6 updates (when released)
- [ ] Integration with external APIs
- [ ] Advanced risk management modules
- [ ] Real-time alert webhooks examples

---

## 📬 Get in Touch

- **Issues:** Use [GitHub Issues](../../issues) for bug reports and feature requests
- **Discussions:** Share ideas in [GitHub Discussions](../../discussions)
- **Pull Requests:** Contributions are welcome via [Pull Requests](../../pulls)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **TradingView** - For creating the powerful Pine Script language
- **Community Contributors** - For feedback, suggestions, and improvements
- **Traders & Developers** - Who inspire continuous learning and innovation

---

## ⭐ Star History

If you find this repository useful, please consider giving it a star! It helps others discover these learning resources.

---

<div align="center">

**Built with ❤️ for the trading community**

[⬆ Back to Top](#-tradingview-pine-script-lab)

</div>
