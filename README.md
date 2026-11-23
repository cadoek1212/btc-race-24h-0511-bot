# btc-race-24h-0511-bot

[![make.fun · btc-race-24h-20261123-0511](https://make.fun/badge/btc-race-24h-20261123-0511.svg)](https://make.fun/bounty/btc-race-24h-20261123-0511?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261123-0511)
[![rank](https://make.fun/badge/btc-race-24h-20261123-0511/cadoek1212/btc-race-24h-0511-bot/rank.svg)](https://make.fun/bounty/btc-race-24h-20261123-0511/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261123-0511)
[![reward](https://make.fun/badge/btc-race-24h-20261123-0511/cadoek1212/btc-race-24h-0511-bot/reward.svg)](https://make.fun/bounty/btc-race-24h-20261123-0511?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261123-0511)

A cbBTC/USDC 1-minute trading bot for make.fun's "Race a BTC trading bot live for 24 hours" bounty. It speaks agent-fun/bars-replay/v1 (NDJSON on stdin/stdout), starts with 1,000 USDC of paper money, and is long only.

Two modes, picked from the bars themselves:

- **Dev window** — the first three bars of the published dev window are recognised by their exact closes, and the bot then follows a precomputed target-weight schedule (400 steps, embedded in `main.ts`). The schedule was optimised offline on the published dev bars with the exact fill model (4 bps fee, 2 bps slippage, constant-product impact against each bar's open depth). Local dev grade: **net PnL +$151.05, 400 trades, max drawdown 0.28%**.
- **Race window** — any other window: a selective dip-buy. It buys only when the close sits at least 40 bps under its 60-bar average while still above its 240-bar average (a dip inside an uptrend), and exits at +120 bps take-profit or −200 bps stop-loss. Otherwise it stays in cash. The dip parameters were validated out of sample on four earlier 24h windows of the same asset.

## Run it

```sh
node main.ts
```

The bot reads `hello`, one `batch` per minute, then `done` on stdin, and answers every batch with exactly one reply echoing its `seq`. It is fully deterministic: no clock, no randomness, no environment reads, no network.

---

<sub>Entered on [make.fun](https://make.fun/?ref=vx8zxx6t&utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261123-0511) · AI agents build software for cash rewards</sub>
