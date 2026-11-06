# Skill cryptos · jeto1337

**English** · [Español](README.es.md)

Eight Claude skills for short-term crypto trading: find what is breaking out,
check whether the news behind it is real, test the plan before you risk a
dollar, size the position to your limits, and paper-trade it on live prices.

Free, MIT, no signup, no API key. Plain Python, standard library only, reading
public data from CoinGecko, Yahoo Finance and the RSS feeds of The Guardian,
The New York Times and the BBC.

**Nothing here trades for you.** No skill ever sends an order to an exchange.
You decide, and you place the order in your own app.

## Install

In Claude Code, as a plugin:

```
/plugin marketplace add spikeich/skill-cryptos-jeto1337
/plugin install skill-cryptos-jeto1337@skill-cryptos-jeto1337
```

Or copy the folders:

```bash
git clone https://github.com/spikeich/skill-cryptos-jeto1337.git
cp -r skill-cryptos-jeto1337/crypto-* ~/.claude/skills/
```

For a single project, copy them into that repo's `.claude/skills/` instead.

They need Python 3.8+ and outbound access to `api.coingecko.com`,
`query1.finance.yahoo.com` and `query2.finance.yahoo.com` (plus
`www.theguardian.com`, `rss.nytimes.com` and `feeds.bbci.co.uk` for news).

The skills were written in Spanish (their author is Argentine): the scripts
print Spanish, and Claude answers you in whatever language you write in.

## The eight skills

| command | what it does |
| --- | --- |
| `/crypto-social-info` | **News, politics and society.** Checks a rumour against 5 reliable sources (known newspapers and agencies, official spokespeople, recognised economists; X posts only with a grey or gold checkmark, and never as confirmation). Measures how crypto moved around bans, laws, ETFs, elections, tariffs, adoption and scandals since 2017. Keeps a calendar of what is coming (CPI, Fed, Congress). |
| `/crypto-scanner` | **What is breaking out.** Opening-range breaks of the **London** or **Wall Street** open, long or short, across the most traded coins, plus daily setups (20-day breakouts and breakdowns, flags, the 20-day average, oversold and overbought). |
| `/crypto-entry` | **When to get in.** Watches bar by bar and tells you the moment a coin closes outside the opening range (or through a level), long or short. |
| `/crypto-exit` | **Where to get out.** Stop, target and flat-by time before you enter, with R net of Binance fees and a liquidation check for your leverage. |
| `/crypto-timemachine` | **Does the plan have an edge?** Replays the rest of the day 10,000 times from the coin's own 5-minute bars of the last 60 days, re-runs the same rule on every past day, and tells you honestly whether it is an edge or a coin flip. |
| `/crypto-risk` | **Does it fit your limits?** Risk per trade, max leverage, liquidation distance, daily losses, open positions, cutoff time. Sizes the trade and prints the order to type into Binance by hand. Keeps the day's journal. |
| `/crypto-alerts` | **While the trade is open.** Rings on price levels and follows your plan: entry filled, stop, target, a limit order that never filled, time to get out. Uses 1-minute highs and lows, so a wick between two looks still counts. |
| `/crypto-scalp` | **Market read and paper trading.** Picks the best coins to scalp right now, sizes a position to your capital and risk, and paper-trades it on live prices with alerts. |

## How they fit together

```
/crypto-social-info  what's in the news? is it true? what's coming?
/crypto-scanner      what broke out at the open
/crypto-entry        the exact moment to get in        -> trader/entry.json
/crypto-exit         stop, target and flat-by time     -> trader/plan.json
/crypto-timemachine  does that plan have an edge?
/crypto-risk         does it fit my limits? size, and the order for Binance
/crypto-alerts       watch the trade while it is open
```

Each skill reads what the previous one wrote to the `trader/` folder of your
project.

## Sessions

Crypto never closes, so "the session" follows the stock markets, which is when
crypto trades the most volume. Each day is worked out with its own daylight
saving offsets for London and New York.

| session | opens | UTC (northern winter) |
| --- | --- | --- |
| `europa` | 08:00 London | 08:00 |
| `wallstreet` | 09:30 New York | 14:30 |
| `europa-wallstreet` | London open to New York close | 08:00-21:00 |

## What the data showed

From 36 verified social and political events, 2017-2026 (`/crypto-social-info`).
A small sample chosen by people: hints, not rules.

- **Bad news weighs more than good news.** After bad news bitcoin fell over the
  next week in 10 of 12 cases (5 of 5 since 2023). After good news it rose in
  only 10 of 21, less often than in a random week.
- **Buy the rumour, sell the news.** Long-expected wins (ETF approvals, the
  bitcoin reserve order, Coinbase's listing) rose before and fell after.
- **Positive surprises do push** (Xi Jinping on blockchain in 2019, Tesla in
  2021, the 2024 US election).
- **Bans give drops that are bought back** within a month.
- **When the news names a coin, that coin moves far more** than bitcoin (XRP
  +73 % the day of the Ripple ruling).

## How news gets verified

| verdict | when |
| --- | --- |
| **VERIFIED** | an official document confirms it, or 4 of 5 reliable, independent sources confirm the same facts (who, what, when, how much), with no denial |
| **DOUBTFUL** | 3 of 5, facts that do not match, a denial from a reliable source, or under an hour old |
| **FALSE** | an official denial, or 2 of 5 or fewer |

Why under an hour is never verified: in January 2024 the SEC's X account was
hacked and announced bitcoin ETF approval. Many outlets repeated it within
minutes, and the price jumped and fell before the denial.

## Credits

`crypto-scanner`, `crypto-entry`, `crypto-exit`, `crypto-timemachine`,
`crypto-risk` and `crypto-alerts` are crypto adaptations of the matching
`trader-*` skills in
[Jakeschincariol/day-trader-skill](https://github.com/Jakeschincariol/day-trader-skill)
(MIT). Its copyright notice is kept in `LICENSE-day-trader-skill`.

## Disclaimer

This is data analysis, not financial advice. A simulation built from the last
60 days does not predict the future: news, liquidation cascades or an exchange
outage can do things those days never did. Leveraged trading can lose
everything you put in. Practice first in your exchange's demo mode.
