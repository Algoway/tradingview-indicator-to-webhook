# Architecture and event boundaries

The **Indicator to Webhook** monitor runs in Chrome, using supported trading information shown on an open TradingView chart. It is a source of trade instructions, not a broker-side execution engine.

```text
New compatible indicator setup
    → Browser detection and command construction
    → AlgoWay webhook intake and routing
    → Destination connector
    → Broker or exchange response
    → Actual trading-account order and position state
```

A signal detected in the chart, a webhook sent, a command accepted by the connector and an order filled by a broker are **different events**. A successful HTTP response cannot stand in for the last two.

## Entry and follow-up events

The documented monitor selects one compatible indicator and establishes a baseline when monitoring begins. When it recognizes a new complete setup, it prepares a command using the configured platform, quantity, trade type, ticker and available chart levels.

When supported, take-profit events and optional breakeven instructions rely on ongoing chart observation and their corresponding broker positions. They are not guaranteed server-side exits. Check the destination account's current orders, filled quantity and remaining exposure.

## Indicator to Webhook versus Free Alerts

**Indicator to Webhook** works with readable chart setups, even without a suitable native alert condition. **Free Alerts** forwards existing TradingView alert messages seen by the extension. They are separate modes and should be tested separately.

Native TradingView server-side alerts and a local browser monitor also have different availability requirements. The monitor cannot observe fresh chart events if Chrome or its TradingView tab stops running.

## Webhook and account security

Treat the actual AlgoWay webhook URL as a trading credential. Never publish its UUID or any API key, password, authentication token, browser cookie or broker account identifier in GitHub Issues or screenshots.

A successful delivery response is not confirmation of order execution. After a disconnect, check the real position and protective orders before attempting to resend missed entries or exits.

Read the [setup guide](https://docs.algoway.trade/algoway-free-alerts-chrome-extension-guide.html) for current options and UI labels.
