# TradingView Indicator to Webhook — AlgoWay Chrome Extension

The AlgoWay Chrome extension can turn trading setups displayed by **compatible TradingView indicators** into webhook commands without access to the indicator's Pine Script source or TradingView's native webhook notification feature.

This repository documents the Chrome extension. It is **not** the extension's source-code repository, and it does not contain trading credentials, proprietary implementation code, or a separately installable build.

## Signal and execution path

```text
TradingView chart with a compatible indicator
              |
              v
AlgoWay Chrome extension — Indicator to Webhook
              |
              v
Configured AlgoWay webhook route
              |
              v
Broker / exchange connector
              |
              v
Trading account
```

The extension reads new, supported setups from the selected indicator on an **open TradingView chart**. The monitor can recognize direction, Entry, Stop Loss and Take Profit levels when the indicator provides them in a supported format. It can also handle documented multi-target and optional breakeven workflows.

A message sent by the extension is not a confirmation of an executed order. Account permissions, symbol mapping, quantity limits and broker-side acceptance still apply.

## Two distinct modes

- **Indicator to Webhook**: monitors one selected compatible indicator, recognizes new setups and generates commands from its displayed trading levels. The selected indicator does not have to provide a native TradingView alert.
- **Free Alerts**: forwards existing TradingView alert messages seen in the open chart tab. This mode does not independently interpret Entry, SL and TP from an indicator's drawings.

Both modes depend on Chrome and the TradingView tab remaining available. Neither mode supplies a trading strategy or guarantees that any indicator is compatible.

## Configure Indicator to Webhook

1. Install the [AlgoWay Chrome extension](https://chrome.google.com/webstore/detail/elpjemcgcgpgklbhgbhmiegamgnckfgb) and open the intended chart in Chrome.
2. In AlgoWay, create a webhook route with **ChromeExtension** as the signal source and select the destination platform/account. Copy the route's unique webhook URL.
3. Open the extension's **Indicator to Webhook** tab, choose **Indicator to monitor**, and enter the AlgoWay webhook URL.
4. Set **Platform**, **Quantity** and **Trade type**, using **Ticker override** when the chart and broker use different symbol names.
5. Where applicable, configure the TP1/TP2/TP3 size distribution and review the total allocation.
6. Enable monitoring on a demo account and wait for a *new* eligible setup. Compare the extension's **Alert Log**, AlgoWay Webhook Logs and the real order status on the destination.

The monitor establishes a baseline when enabled. Historical labels already on the chart are not automatically new trade instructions. Entry and subsequent TP or breakeven management depend on the indicator format and continued browser operation.

## Operating limits

Compatible displayed data is required; an invite-only indicator is **not** automatically supported just because it draws BUY/SELL labels. The extension does not recover protected Pine source code.

Browser sleep, chart reloads, connectivity loss and layout changes may interrupt signal detection. Inspect the trading account before restarting monitoring or replaying instructions, since duplicated entries or missed exits can create unintended exposure.

An HTTP 200 or successful extension log entry does not confirm that the broker filled an order or placed its SL/TP.

## Documentation

- [Extension setup and current interface](https://docs.algoway.trade/algoway-free-alerts-chrome-extension-guide.html)
- [Signal and execution boundaries](docs/architecture.md)
- [Compatibility and troubleshooting](docs/troubleshooting.md)
- [Indicator to Webhook feature](https://algoway.trade/tradingview-indicator-to-webhook)

No latency, performance, compatibility-rate or profitability benchmarks are asserted here.
