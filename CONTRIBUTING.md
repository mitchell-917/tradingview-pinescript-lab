# 🤝 Contributing to TradingView Pine Script Lab

Thank you for your interest in contributing! This document provides guidelines and best practices for contributing to this educational repository.

---

## 📋 Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [How Can I Contribute?](#how-can-i-contribute)
3. [Development Guidelines](#development-guidelines)
4. [Submission Process](#submission-process)
5. [Style Guide](#style-guide)
6. [Testing Requirements](#testing-requirements)

---

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for everyone, regardless of:

- Experience level (beginners welcome!)
- Gender identity and expression
- Sexual orientation
- Disability
- Personal appearance
- Body size
- Race or ethnicity
- Age
- Religion or lack thereof
- Professional background

### Our Standards

**Positive behaviors:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints
- Gracefully accepting constructive criticism
- Focusing on what's best for the community
- Showing empathy towards others

**Unacceptable behaviors:**
- Trolling, insulting/derogatory comments, and personal attacks
- Public or private harassment
- Publishing others' private information without permission
- Any conduct which could reasonably be considered inappropriate

---

## How Can I Contribute?

### 🐛 Reporting Bugs

**Before submitting a bug report:**

1. Check the [FAQ](docs/faq.md) for solutions
2. Search [existing issues](../../issues) to avoid duplicates
3. Test on the latest version of TradingView

**When submitting:**

- Use a clear, descriptive title
- Describe the exact steps to reproduce
- Provide specific examples (code snippets, screenshots)
- Describe the behavior you observed vs expected
- Include your TradingView account type (free/pro/premium)
- Mention the symbol, timeframe, and date range tested

**Template:**

```markdown
**Description:**
Clear description of the bug

**Steps to Reproduce:**
1. Open indicator X
2. Set parameter Y to Z
3. Observe behavior...

**Expected Behavior:**
What should happen

**Actual Behavior:**
What actually happens

**Environment:**
- TradingView Plan: Free/Pro/Premium
- Symbol: SPY
- Timeframe: 1H
- Browser: Chrome 120

**Screenshots:**
If applicable
```

---

### 💡 Suggesting Enhancements

We welcome ideas for:

- New indicators or strategies
- Improvements to existing scripts
- Additional documentation
- Code examples and snippets
- Tutorial topics

**When suggesting:**

- Use a clear, descriptive title
- Provide a detailed description of the enhancement
- Explain **why** this would be valuable
- Include code examples or mockups if applicable
- Consider the educational value (this is a learning resource)

---

### 📝 Improving Documentation

Documentation contributions are highly valued!

**Areas to improve:**

- Fixing typos or grammatical errors
- Clarifying confusing explanations
- Adding examples to concepts
- Expanding tutorials
- Translating content (if fluent)

**Guidelines:**

- Keep language clear and accessible
- Use proper markdown formatting
- Include code examples where helpful
- Focus on educational value
- Test all code snippets

---

### 🔧 Contributing Code

**Types of code contributions:**

1. **Bug fixes** - Fix issues in existing scripts
2. **New indicators** - Add well-documented indicators
3. **New strategies** - Add educational strategy examples
4. **Code snippets** - Reusable patterns
5. **Templates** - Starter files for common use cases

---

## Development Guidelines

### Project Philosophy

This repository prioritizes:

1. **Educational Value** - Code teaches Pine Script concepts
2. **Code Quality** - Clean, readable, well-documented code
3. **Practicality** - Real-world applicable tools
4. **Best Practices** - Industry-standard approaches

### What We're Looking For

✅ **Good contributions:**

- Well-commented code explaining key concepts
- Educational value (teaches something useful)
- Follow the Pine Style Guide
- Includes usage examples
- Tested on multiple symbols/timeframes
- Addresses a real need or use case

❌ **Avoid:**

- Uncommented or poorly documented code
- "Black box" indicators with no explanation
- Copy-pasted code from other sources (without proper attribution)
- Overly complex code without educational justification
- "Holy grail" claims or unrealistic promises
- Code that only works on specific cherry-picked charts

---

## Submission Process

### 1. Fork & Clone

```bash
# Fork the repository on GitHub
# Then clone your fork:
git clone https://github.com/YOUR-USERNAME/tradingview-pinescript-lab.git
cd tradingview-pinescript-lab
```

### 2. Create a Branch

```bash
# Create a descriptive branch name:
git checkout -b feature/add-stochastic-indicator
# or
git checkout -b fix/rsi-calculation-bug
# or
git checkout -b docs/improve-getting-started
```

Branch naming conventions:
- `feature/` - New features or scripts
- `fix/` - Bug fixes
- `docs/` - Documentation changes
- `refactor/` - Code improvements without behavior changes

### 3. Make Your Changes

Follow the guidelines in this document, especially:

- [Style Guide](#style-guide)
- [Testing Requirements](#testing-requirements)
- [Documentation Standards](#documentation-standards)

### 4. Test Thoroughly

- Load script in TradingView
- Test on multiple symbols (stocks, forex, crypto)
- Test on multiple timeframes (1m, 5m, 1H, 1D)
- Verify no errors or warnings
- Check performance (no excessive lag)

### 5. Commit Your Changes

```bash
git add .
git commit -m "Add stochastic oscillator indicator with educational comments"
```

**Commit message guidelines:**

- Use present tense ("Add feature" not "Added feature")
- Use imperative mood ("Move file to..." not "Moves file to...")
- Limit first line to 72 characters
- Reference issues: "Fix #123" or "Closes #456"

### 6. Push to Your Fork

```bash
git push origin feature/add-stochastic-indicator
```

### 7. Open a Pull Request

1. Go to the original repository on GitHub
2. Click "New Pull Request"
3. Select your fork and branch
4. Fill out the PR template:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New indicator
- [ ] New strategy
- [ ] Documentation
- [ ] Code refactoring

## Educational Value
What does this teach users?

## Testing
- Tested on: SPY, EURUSD, BTCUSD
- Timeframes: 5m, 1H, 1D
- No errors or warnings

## Screenshots (if applicable)
Add screenshots showing the indicator in action

## Checklist
- [ ] Follows Pine Style Guide
- [ ] Includes comprehensive comments
- [ ] Tested on multiple symbols/timeframes
- [ ] Documentation updated (if needed)
- [ ] No breaking changes
```

---

## Style Guide

### File Naming

**Pine Script files:**

```
lowercase-with-hyphens.pine
```

Examples:
- ✅ `ma-crossover-indicator.pine`
- ✅ `rsi-mean-reversion-strategy.pine`
- ❌ `MyIndicator.pine`
- ❌ `indicator_v2.pine`

**Documentation files:**

```
lowercase-with-hyphens.md
```

Examples:
- ✅ `getting-started.md`
- ✅ `backtesting-best-practices.md`

### Code Structure

Every Pine Script should follow this structure:

```pine
//=============================================================================
// [Indicator Name] [Lab]
//=============================================================================
//
// WHAT THIS DOES
//  - Brief description of functionality
//  - Key features
//
// EDUCATIONAL FOCUS
//  - What concepts does this teach?
//  - What makes this useful for learning?
//
// USAGE NOTES
//  - How to use this indicator
//  - What to look for
//
//=============================================================================
//@version=5
indicator("Indicator Name [Lab]", overlay = true)

//-----------------------------------------------------------------------------
// INPUTS
//-----------------------------------------------------------------------------
// Group related inputs
groupSettings = "Main Settings"
length = input.int(14, "Length", minval = 1, group = groupSettings)

//-----------------------------------------------------------------------------
// CALCULATIONS
//-----------------------------------------------------------------------------
// Main logic goes here
value = ta.sma(close, length)

//-----------------------------------------------------------------------------
// CONDITIONS
//-----------------------------------------------------------------------------
// Logical conditions
bullish = close > value

//-----------------------------------------------------------------------------
// PLOTTING
//-----------------------------------------------------------------------------
// Visual output
plot(value, "SMA", color = color.blue)

//-----------------------------------------------------------------------------
// ALERTS
//-----------------------------------------------------------------------------
// Alert conditions (if applicable)
alertcondition(bullish, "Bullish Signal", "Price above MA")

//-----------------------------------------------------------------------------
// EDUCATIONAL NOTES
//-----------------------------------------------------------------------------
//
// Study ideas:
//  - Try different lengths
//  - Combine with other indicators
//  - Add filters based on HTF trend
```

### Commenting Standards

**Do:**

- Explain **why** code does something, not just what
- Add educational context for complex concepts
- Include study ideas and extension suggestions
- Comment on limitations or edge cases

**Don't:**

- State the obvious: `length = 14 // length is 14`
- Leave complex code unexplained
- Use vague comments: `// do stuff here`

**Example - Good comments:**

```pine
// We use EMA instead of SMA here because EMA responds faster to recent
// price changes, which is critical for this momentum-based system
fastMA = ta.ema(close, 12)

// Lookback excludes current bar [1] to prevent using future data
// This ensures the indicator doesn't repaint
prevHigh = ta.highest(high[1], lookback)
```

**Example - Bad comments:**

```pine
// Calculate EMA
fastMA = ta.ema(close, 12)

// Get previous high
prevHigh = ta.highest(high[1], lookback)
```

### Variable Naming

**Use descriptive names:**

```pine
// ✅ Good
rsiOverbought = 70
sessionHigh = ta.highest(high, sessionBars)
bullishCrossover = ta.crossover(fastMA, slowMA)

// ❌ Bad
ob = 70
sh = ta.highest(high, sb)
bc = ta.crossover(f, s)
```

**Naming conventions:**

- Variables: `lowerCamelCase`
- Constants: `UPPER_SNAKE_CASE` (if applicable)
- Booleans: Start with `is`, `has`, `should`, or use descriptive adjectives
  - `isBullish`, `hasSignal`, `shouldAlert`, `bullish`

---

## Testing Requirements

Before submitting, test your script:

### ✅ **Functional Testing**

1. **Load without errors**
   - No compilation errors
   - No runtime warnings

2. **Test on multiple symbols**
   - Stocks (e.g., SPY, AAPL)
   - Forex (e.g., EURUSD, GBPJPY)
   - Crypto (e.g., BTCUSD, ETHUSD)
   - Indices (e.g., SPX, NDX)

3. **Test on multiple timeframes**
   - Intraday (1m, 5m, 15m)
   - Hourly (1H, 4H)
   - Daily (1D)
   - Weekly (1W) if applicable

4. **Test edge cases**
   - Symbols with gaps (stocks)
   - 24/7 markets (crypto)
   - Low liquidity periods
   - Historical data with missing bars

### ✅ **Performance Testing**

- Chart loads in reasonable time (< 5 seconds)
- No "Script takes too long" errors
- Responsive UI (settings changes apply quickly)
- Reasonable memory usage (no excessive arrays/labels)

### ✅ **Visual Testing**

- Plots are clearly visible
- Colors have good contrast
- Labels don't overlap excessively
- Works on both light and dark themes

---

## Documentation Standards

### Indicator/Strategy Documentation

Each script should include:

**1. Header Block** (in the code)
- What it does
- Educational focus
- Usage notes
- Limitations

**2. Inline Comments** (throughout code)
- Explain complex logic
- Clarify non-obvious decisions
- Add educational context

**3. Study Ideas** (end of script)
- Suggestions for experimentation
- Extension ideas
- Related concepts to explore

### Markdown Documentation

**File structure:**

```markdown
# Title

Brief introduction (2-3 sentences)

---

## Section 1

Content with examples

---

## Section 2

More content

---

<div align="center">
Navigation links
</div>
```

**Formatting:**

- Use headers hierarchically (don't skip levels)
- Include code blocks with language specification
- Add tables for comparisons
- Use emoji sparingly for visual hierarchy
- Include navigation links at bottom

---

## Review Process

### What Reviewers Check

1. **Code Quality**
   - Follows style guide
   - Well-commented
   - No obvious bugs

2. **Educational Value**
   - Teaches useful concepts
   - Clear explanations
   - Appropriate complexity level

3. **Testing**
   - Works on multiple symbols/timeframes
   - No performance issues
   - Handles edge cases

4. **Documentation**
   - Clear and complete
   - No typos or grammar issues
   - Examples work as described

### Feedback Process

- Reviewers will provide constructive feedback
- Make requested changes and push updates
- Discussion happens in PR comments
- Once approved, PR will be merged

### After Merging

- Your contribution will be credited
- Script becomes part of the learning resource
- Others can learn from your work!

---

## Questions?

- **General questions:** Open a [GitHub Discussion](../../discussions)
- **Bug reports:** Open an [Issue](../../issues)
- **Direct contact:** See repository maintainer info

---

Thank you for contributing to the Pine Script learning community! 🎉

---

<div align="center">

[⬅ Back to README](README.md)

</div>
