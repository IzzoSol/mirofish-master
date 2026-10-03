# 🐟 MiroFish Master

Private master repo holding the improved **MiroFish terminal (v7.0 PRO)** and the **ZA signals bot (v2)** — both upgraded with the curated best of seven source repos. No clutter: every feature below had to earn its place.

## What's inside

| Path | What |
|---|---|
| `terminal/index.html` | MiroFish v7.0 PRO — single-file, zero-build terminal |
| `bot/` | ZA signals bot v2 — Node, zero dependencies (Node 18+ built-in fetch) |

## Best-of map (what was taken, from where)

| Feature | Taken from | Why |
|---|---|---|
| RSI / volume-spike / regression-divergence TA | `b-fg/nuatsbot` (`nuats_ta.py`) | The only real signal math in the source set; modernized to dependency-free JS (original used dead 2018 pandas APIs) |
| RugCheck safety gate + token card | `0xRefDev/gemtrack_bot` (`services/rugcheck.js`) | Score threshold, mint/freeze authority flags, top-holder concentration, GMGN links — translated to English, plain fetch |
| Telegram channel monitoring concept + multi-source price fetch | `gogonuk/memecoin-bot` | DexScreener-first price fetching adopted; group monitoring deliberately **not** taken (needs API keys, adds clutter) |
| Command palette (Ctrl+K) | `ErTasselli/OpenTerminal` (`CommandPalette.tsx`) | The single best "pro terminal" affordance; rebuilt in 60 lines of vanilla JS instead of Next.js |
| Signal ranking + digest broadcast discipline | `nlethetech/nepse-quant-terminal` (`signal_ranking.py`, `telegram_alerts.py`) | Strength-ranked digests, cooldown per market |
| Hard risk clamps wired around a signal engine | `NoFxAiOS/nofx` | The architecture idea (engine proposes, risk layer disposes) applied to the existing ZA engine |
| — | `waveterncleanse/robinhood-sniper-bot` | Empty repo (LICENSE only) — nothing to take |

## Terminal v7.0 PRO changes (vs TuFish v6)

- **DEX token images** — DexScreener `info.imageUrl` (+ CoinGecko `image` for majors) rendered as 22px rounded tokens with letter-badge fallback
- **Live sentiment** — real Fear & Greed from `api.alternative.me` (was `Math.random()`); per-category scores now derived from live 24h market data
- **Telegram wiring** — Settings → bot token + chat ID; manual digest send + AUTO mode (70%+ confidence, 30-min per-market cooldown)
- **Command palette** — Ctrl+K / ⌘K: panels, refresh, trade top signal, Monte Carlo, TG digest, theme, export
- **Pro badge** — v7.0 · PRO in the header

## Bot v2 changes (vs ZA-zerox-autotrader)

- `ta.js` — Wilder RSI-14, volume spikes, RSI/price divergence over 10/20/30/40 windows (≥3 confirmations), self-tested
- `rugcheck.js` — rugcheck.xyz gate before any memecoin call is broadcast
- `signals-bot.js` — live loop: Binance klines → TA → DexScreener memecoin scan → rugcheck gate → ranked digest → Telegram/Discord
- `engine.js` — original ZA strategy (4% SL / 12% trail / 6% gap / 2% size) with the risk config **actually wired**: 15% drawdown circuit breaker, $25 daily cap, $5 per-trade cap, 20-trade daily limit

## Cross-links

- Original terminal: [IzzoSol/TuFish](https://github.com/IzzoSol/TuFish) (public)
- Original bot: [IzzoSol/ZA-zerox-autotrader](https://github.com/IzzoSol/ZA-zerox-autotrader) (private)
- Structure pattern: [IzzoSol/shaddai-gamedev-tools](https://github.com/IzzoSol/shaddai-gamedev-tools)

## Agent note

Built 2026-10-03. SHADDAI MCP / local agent ports (8000-8008) were offline, so the ZEROX (broadcast policy, risk economics), TURTLE (token-image + palette design), and NEXUS (module layout, breaker wiring) disciplines were applied in-session per `AGENT_SYSTEM_PROMPTS.md`. Re-run each agent review when the empire is back online.
