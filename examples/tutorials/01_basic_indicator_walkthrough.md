# Tutorial 01 – Basic Indicator Walkthrough

This tutorial walks through the key parts of a simple moving-average indicator.

## 1. Open the Example

1. Open the file: `indicators/beginner/ma-crossover-indicator.pine`.
2. Read the header comments to understand what it does.
3. Copy/paste it into TradingView’s Pine Editor and add it to a chart.

## 2. Identify the Sections

Look for these blocks:

- **Inputs** – user-configurable settings like lengths and sources.
- **Calculations** – the moving averages and crossover logic.
- **Plotting** – the visual output on the chart.
- **Alerts** – optional signals you can tie to TradingView alerts.

## 3. Experiment

Try making small changes:

- Change the MA types (`ta.sma` → `ta.ema`).
- Adjust lengths (e.g., 9 & 21 → 20 & 50).
- Disable or enable specific plotshapes.

Each change helps you see how Pine responds and how the chart updates.
