# Purple Cloud Alerts

A Python experiment that checks hourly BTC-USD market data for a custom trend-signal condition and sends a Telegram notification when a new signal is detected.

> **Research / alerting project only.** This repository does not provide investment advice, does not establish a profitable trading strategy, and does not include verified out-of-sample performance results.

## What it does

- Downloads up to 120 days of BTC-USD hourly candles using yfinance.
- Calculates ATR-based bands and a Supertrend-style direction state.
- Adds an EMA 200 trend filter.
- Evaluates custom Purple Cloud conditions and detects a newly timestamped BUY or SHORT signal.
- Stores the last signal in signal_state.json to avoid repeating the same alert.
- Sends a Telegram message when a new signal is found.

## Automation

The GitHub Actions workflow at .github/workflows/telegram.yml runs on a two-hour schedule and can also be started manually.

Configure these repository Actions secrets before enabling the workflow:

| Secret | Purpose |
|---|---|
| BOT_TOKEN | Telegram bot token |
| CHAT_ID | Destination chat ID |

Never hard-code tokens or chat credentials in the source code.

## Run locally

    git clone https://github.com/Talket/purple-cloud-alerts.git
    cd purple-cloud-alerts
    python -m venv .venv
    pip install -r requirements.txt

Set BOT_TOKEN and CHAT_ID as environment variables, then run:

    python btc_alert.py

## Repository map

- btc_alert.py — market-data retrieval, indicator calculations, signal state and Telegram notification.
- signal_state.json — timestamp of the most recently notified signal.
- .github/workflows/telegram.yml — scheduled and manual GitHub Actions workflow.
- requirements.txt — Python dependencies.

## Important limitations

This is an indicator-alert implementation, not a backtested trading system. Before using any signal in a decision, independently validate the logic, account for fees and slippage, test out of sample, and understand the risk of leveraged or volatile markets.
