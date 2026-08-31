# Higgsfield CPA Visualizer

A single-file interactive CPA (cost-per-acquisition) / affiliate economics visualizer for the Higgsfield pitch. Open `index.html` in any browser — no build step, no backend, no npm install. Works offline after load.

## Quick start
1. Download `index.html`.
2. Double-click it (or drag it into Chrome / Safari / Firefox).
3. Move sliders, watch the live equation and chart update.

## What it does
- **Live equation board**: `Max affordable CPA = projected LTV − projected credit cost`, updates with every slider.
- **Day-N breakeven**: pick a day (30→365); the ceiling and profit-per-user recalculate live.
- **LTV curve table + chart**: editable LTV & credit cells per checkpoint (30/60/90/120/180/210/240/365); profit-vs-day line chart with cashback day highlighted.
- **Scenario compare**: $200 / $300 / $400 CPA side by side (cashback day, profit @ 180 & 365, max affordable).
- **Competitor "pay just enough to swap"**: suggested CPA = min(max affordable, competitor + premium).
- **Plan presets** (monthly/annual): Starter ~$19, Starter annual ~$228, Mid ~$59, High ~$130, plus Custom.
- **Volume sanity**, **tooltips**, **"Say this to the CTO" script**.
- State persists to `localStorage`; **Reset to placeholders** and **Copy summary** buttons.

## Math (encoded exactly)
```
quality      = trafficQualityMultiplier
contribution(day) = pLTV(day) * quality - pCredit(day) + halo
maxCPA(day)       = max(0, pLTV(day) * quality - pCredit(day) + halo)
profit(day, C)    = pLTV(day) * quality - pCredit(day) + halo - C
cashbackDay(C)    = first day in table where profit(day, C) >= 0  (else ">365 / never")
suggestedCPA      = min(maxCPA(selectedDay), competitorCPA + swapPremium)
```
Quality scales **LTV only**; credits stay unscaled.

## ⚠️ Replace with real data before trusting
All LTV & credit curves are **PLACEHOLDER / FAKE** teaching numbers. Before the numbers mean anything, replace:
- LTV by plan at each day N (monthly)
- LTV if yearly at each day N (annual)
- Credit cost by plan at each day N (monthly)
- Credit cost if yearly at each day N (annual)

Edit the cells in the LTV Curve table live during the meeting — changes persist to localStorage.
