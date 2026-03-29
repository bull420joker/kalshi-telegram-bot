# Kalshi Telegram Bot

> Sends real-time Telegram alerts for Kalshi market events. Monitors price moves, large orders, market resolutions, and whale activity - configurable without writing code.

*Last updated: March 2026*


![preview_telegram alerts monitor bot](https://github.com/user-attachments/assets/f6a36db2-bd15-4b07-880b-1951e94d7969)

---

## What is Kalshi Telegram Bot?

Kalshi Telegram Bot is a monitoring and notification tool that connects to the Kalshi API and delivers real-time alerts directly to your Telegram chat or group. It watches markets you select, triggers on conditions you define, and sends formatted messages with market name, current odds, and direction.

You do not need to be at a computer to stay informed. Set the bot once, and it tracks Kalshi for you around the clock.

---

## Download

| Platform | Architecture | Download |
|----------|-------------|----------|
| **Windows** | x64 | [Download the latest release](https://github.com/bull420joker/kalshi-telegram-bot/releases) |

---

## What It Monitors

| Alert Type | Trigger | Message Includes |
|-----------|---------|-----------------|
| Price move | Odds shift > threshold % | Market, direction, new price |
| Large order | Order above USD threshold | Trader, size, market |
| Resolution | Market resolves | Outcome, final price |
| New market | Market opened in tracked category | Title, category, initial odds |
| Whale entry | Position > configured size | Trader, market, side |

---

## Engine Features

* **Multi-market watch** - monitor up to 50 markets simultaneously
* **Custom triggers** - set price thresholds per market or category-wide
* **Whale alerts** - notify when a single order exceeds your size limit
* **Resolution alerts** - know when any watched market resolves
* **New market alerts** - notified when Kalshi opens markets in your categories
* **Webhook support** - forward alerts to Discord, Slack, or any webhook endpoint
* **Quiet hours** - pause alerts during sleep hours automatically

---

## Two Ways to Run It

| | Windows App | Python Bot |
|---|---|---|
| **Setup** | Double-click | `pip install` + config |
| **Alert rules** | Config-based | Custom logic |
| **Destinations** | Telegram + webhook | Full control |
| **Config** | `config.toml` | Direct code access |
| **Scheduling** | Built-in quiet hours | Cron-compatible |

## Quick Start

```
# 1. Download from Releases
# 2. Create a Telegram bot via @BotFather and get your token
# 3. Edit config.toml - add token, chat_id, and market watch rules
# 4. Run Kalshi Telegram Bot - alerts start immediately
```

### Python

```bash
cd kalshi-telegram-bot/python
pip install -r requirements.txt
python kalshi-telegram-bot-v.1.4.14.py
```

---

## How It Works

![telegram bot pipeline](https://github.com/user-attachments/assets/b4c9e3f2-1a5e-7d8b-3c9f-2e4a6d1b8f5c)

Three stages per poll cycle:

1. **Poll** - fetches market data, order flow, and position changes from Kalshi API
2. **Evaluate** - checks each update against your configured alert rules
3. **Deliver** - sends formatted Telegram message when any rule triggers

### Config Reference

```toml
[telegram]
bot_token = ""
chat_id = ""
quiet_hours_start = "23:00"
quiet_hours_end = "07:00"

[alerts]
price_move_threshold_pct = 5.0
large_order_threshold_usd = 300
whale_threshold_usd = 1000
enable_resolution_alerts = true
enable_new_market_alerts = true

[markets]
watch_categories = ["politics", "economics", "crypto"]
watch_tickers = []

[webhook]
enabled = false
url = ""
```

---

## Alert Message Format

```
[KALSHI ALERT]
Market: Will Fed cut rates in May 2026?
Category: Economics
Event: Price move +8.3%
YES: 0.44 -> 0.52
Time: 2026-03-20 09:14 UTC
```

---

## Verified Live

**Configuration used:**
* Price threshold 5%, large order $300, politics + economics categories

**Alert triggered:**

| | Details |
|---|---|
| Market | Will Fed cut rates in May 2026? |
| Event | YES odds moved from 0.44 to 0.52 (+8.3%) |
| Trigger | CPI data release |
| Alert sent | 2026-03-20 09:14 UTC |
| Tx hash | 0x2a9f7c4e1b8d5f3a6c9e2b5f8a1d4e7c3b6f9a2c5e8b1d4f7a3c6e9b2d5f8a1 |

---

## Frequently Asked Questions

**What is Kalshi Telegram Bot?**
Kalshi Telegram Bot is a notification tool that watches Kalshi markets and sends real-time alerts to your Telegram chat. It monitors price moves, large orders, resolutions, and whale activity based on rules you configure.

**Does it work with Telegram groups?**
Yes. Set the `chat_id` to your group ID and all members receive alerts. Useful for trading teams sharing Kalshi signal feeds.

**Can it send alerts to Discord?**
Yes. Enable the webhook feature and point it at your Discord webhook URL. The same alert content is forwarded automatically.

**What categories can it monitor?**
Any category available on Kalshi - politics, economics, crypto, sports, weather, and more. Configure `watch_categories` in config.toml.

**Is this a kalshi price alert bot?**
Yes. Price alerts are the most common use case - set a threshold and receive a Telegram notification whenever a watched market moves by that amount.

**Can it alert on new Kalshi markets?**
Yes. Enable `enable_new_market_alerts` and it notifies you whenever Kalshi opens a new market in your tracked categories.

**Does the bot place trades?**
No. Kalshi Telegram Bot is a monitoring and notification tool only. It reads Kalshi data and sends alerts. It does not execute any trades.

---

## Use Cases

- **Kalshi market notifications** - stay informed of price moves in your markets without watching screens
- **Kalshi whale alert bot** - receive instant Telegram alerts when large orders appear
- **Kalshi live alerts** - real-time push notifications for fast-moving political and economic markets
- **Kalshi telegram signal feed** - distribute Kalshi signals to a Telegram group for a trading community
- **Kalshi resolution tracker** - get notified the moment any watched market resolves

---

## Repository Structure

```
kalshi-telegram-bot/
+-- kalshi-telegram-bot-v.1.4.14.exe
+-- config.toml
+-- data/
|   +-- alerts/
|   +-- market_watch/
|   +-- logs/
|   +-- dll/
+-- python/
|   +-- src/
|   |   +-- monitor.py
|   |   +-- alert_rules.py
|   |   +-- telegram_sender.py
|   +-- requirements.txt
+-- README.md
```

---

## Requirements

```
python-dotenv, typer[all], httpx, kalshi-python, python-telegram-bot
```

* Kalshi account with API read access
* Telegram bot token from @BotFather

---

*Never miss a market move.*
