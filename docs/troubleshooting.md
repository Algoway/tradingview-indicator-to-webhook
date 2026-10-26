# Compatibility and troubleshooting

These checks apply to the documented AlgoWay Chrome extension. Use a demo or other non-live destination when evaluating unfamiliar indicator behavior.

## The indicator does not appear in the selector

Keep the TradingView chart open and allow the study to load. The monitor needs readable signal and price-level information from a compatible indicator. A visible arrow or a protected script by itself does not establish compatibility.

## The monitor is enabled but nothing is sent

The monitor establishes a baseline and waits for a new eligible setup. A historical BUY or SELL label already on the chart when monitoring starts is not necessarily a new event. Verify the selected indicator, chart symbol, timeframe, direction and available Entry/SL/TP levels.

## An outgoing command appears in the Alert Log but no order exists

Check AlgoWay Webhook Logs, the correct destination account, connection status, symbol mapping, trade direction, accepted quantity and order restrictions. An HTTP success response does not establish a filled broker order.

## Stop Loss, Take Profit or breakeven behavior looks wrong

Compare the levels displayed on the TradingView chart with those recognized by the monitor and the command sent to AlgoWay. Then inspect the actual broker position, protective orders and remaining size. Avoid repeating an instruction until the account state is known.

## The browser was closed or the computer slept

Browser-based monitoring requires an available Chrome process and an open chart tab. A remote trading terminal or exchange connection can remain online while the local indicator monitor has stopped observing new signals.

## Reporting a compatibility issue

Useful details include the extension mode, indicator format, chart symbol, timeframe, expected event, observed parameters and **redacted** extension/AlgoWay logs. Remove webhook UUIDs, API tokens, personal details and trading-account identifiers before posting.

Current UI and configuration are described in the [AlgoWay Chrome extension guide](https://docs.algoway.trade/algoway-free-alerts-chrome-extension-guide.html).
