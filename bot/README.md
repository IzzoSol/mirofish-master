# ZA Signals Bot v2

Zero-dependency Node bot (Node 18+). Live TA on Binance pairs + memecoin scan on DexScreener, rugcheck-gated, broadcast to Telegram and/or Discord.

## Run

```
set TELEGRAM_BOT_TOKEN=123:abc      # optional — omit for dry-run
set TELEGRAM_CHAT_ID=-100123        # optional
node signals-bot.js                 # live loop, one cycle every 15 min
node signals-bot.js --once          # single cycle
node signals-bot.js --dry-run       # force console output, no sending
```

## Modules

| File | Role |
|---|---|
| `config.js` | All knobs: strategy, risk, TA thresholds, watchlists, TG/Discord |
| `ta.js` | RSI-14, volume spikes, regression divergence (10/20/30/40 windows, 3+ confirmations). `node ta.js` runs the self-test |
| `rugcheck.js` | rugcheck.xyz gate (score, authorities, top-holder %) + plain-text token card |
| `broadcast.js` | Telegram Bot API + Discord webhook senders |
| `signals-bot.js` | Loop: klines → TA → memes → rugcheck → digest → broadcast. 6h per-signal cooldown, top 8 per digest |
| `engine.js` | ZA paper engine with wired circuit breaker (15% drawdown), $25/day, $5/trade, 20 trades/day. `node engine.js` runs the simulation |

## Signal policy

- Strength 0-100; only ≥60 broadcast (`signalMinStrength`)
- Meme calls need $20k+ liquidity and either 1.8x 6h-volume pace or ±8% 24h move, then must pass rugcheck — failures surface as ⚠️ AVOID with flags
- Binance TA: RSI overbought/oversold, volume spikes >5x average, multi-window divergence
