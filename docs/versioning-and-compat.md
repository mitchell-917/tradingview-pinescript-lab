# Versioning & Compatibility

This document explains how **Pine Script versions** and **TradingView compatibility** are handled in this repository.

---

## 1. Pine Script Version

All scripts in this repository target **Pine Script v5**:

```pine
//@version=5
```

Reasons:

- v5 is the current major version at the time of writing.
- It provides better namespacing (`ta.*`, `math.*`, `array.*`, etc.).
- It’s the most future-proof choice for new development.

If you are still on an older version of Pine (v3 or v4) you may need to:

- Replace `ta.*` calls (e.g., `ta.sma` → `sma`).
- Remove `indicator()`/`strategy()` v5-only parameters or adjust syntax.

We do **not** maintain separate v4/v3 branches in this repository.

---

## 2. TradingView Platform Compatibility

These scripts are tested with:

- Current TradingView web interface.
- Standard chart types (candlestick, bar, etc.).

They **should** also work on TradingView desktop and mobile, as Pine scripts are synced across devices, but:

- The Pine Editor experience is best in the web or desktop apps.
- Some interfaces (e.g., adding alerts) may look slightly different on mobile.

---

## 3. Multi-Timeframe & Security Calls

Some scripts use `request.security()` to access higher or different timeframes.

We aim to:

- Use `lookahead = barmerge.lookahead_off` by default to avoid future leaks.
- Document any repainting risks where applicable.

If you notice unexpected behavior (e.g., historical signals differ from real-time signals), check:

- Whether the script uses security calls.
- Whether plotting is done on confirmed vs real-time bar states (`barstate.isconfirmed`, `barstate.isrealtime`).

---

## 4. Updating Scripts Over Time

Over time, the Pine language may add features or deprecate older behavior.

When updating scripts:

1. Keep `//@version=5` unless a new **major** version (e.g. v6) is broadly adopted.
2. Replace deprecated functions/methods with their recommended alternatives.
3. Run scripts on a chart and check for warnings or errors in TradingView.

If a script is materially changed in a way that affects behavior:

- Note the change in a `CHANGELOG` entry (if maintaining this repo in Git).
- Add a brief comment inside the script explaining what changed and why.

---

## 5. Known Limitations

- **Backtesting differences**: Strategy results can vary when Pine or TradingView changes internal execution details. We do not guarantee exact reproduction of historical results across years.
- **Market data differences**: Scripts are data-source agnostic. Different brokers/exchanges feed different prices → your results may differ from screenshots or examples.
- **Feature availability**: Some advanced Pine features are released gradually; if you’re on an older environment, very new features might not compile until TradingView updates your cluster.

---

## 6. “No-Repaint” & Historical Consistency

Where possible, we aim for **historically consistent** behavior, but:

- Any script using **future-looking logic** (e.g., pivots that need several bars confirmation) will mark signals **after the fact** historically.
- Any script that explicitly uses **lookahead behavior** (rare, and documented) is meant for demonstration, not for live trading alerts.

We highlight these behaviors in comments near the relevant code block.

---

## 7. Support & Issues

If you encounter version-related issues:

- Check that your script’s header still says `//@version=5`.
- Ensure you copied the full script from the repo without modifying the version line.
- Look at TradingView’s error messages/line numbers carefully.

If the problem persists and this is part of a public GitHub repo:

- Open an **issue** with:
  - The script filename.
  - A screenshot or copy of the error.
  - Your TradingView environment (web/desktop, browser, OS).

This helps us keep scripts compatible and up to date.
