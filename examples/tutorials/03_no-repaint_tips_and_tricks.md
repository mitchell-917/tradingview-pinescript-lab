# Tutorial 03 – No-Repaint Tips & Tricks

Repainting is when a signal looks different in history than it did in real time.

## 1. Common Repainting Sources

- Pivot-based indicators (swings, fractals).
- Indicators that use future bars (lookahead).
- Intrabar updates on realtime bars.

## 2. Safer Practices

- Use `lookahead = barmerge.lookahead_off` with `request.security()`.
- Base signals on **confirmed bars** (e.g., `barstate.isconfirmed`).
- Accept that some techniques (like pivots) are inherently delayed.

## 3. How This Repo Handles It

Scripts that may repaint or use delayed confirmation:

- Include comments near the relevant code.
- Are meant for **education**, not for blind signal following.

When in doubt, watch the indicator live for a while and see how signals evolve as new bars form.
