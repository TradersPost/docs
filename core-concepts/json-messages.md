# JSON Messages

TradersPost uses [JSON messages](https://en.wikipedia.org/wiki/JSON) to receive and process trading instructions. If you're new to JSON, don't worry, it's simply a way to structure data in a format that's both machine-readable and easy for humans to understand.

Head to the [webhooks documentation](webhooks.md) to see all the different types of JSON messages you can send.

## What Is JSON?

**JSON** stands for _JavaScript Object Notation_. It’s a simple, text-based format for organizing data using key/value pairs. In TradersPost, JSON allows you to send your trading signals with clear instructions that define _what to trade_ and _how to trade it_.

Here’s a very simple example of a JSON message that TradersPost would use:

```json5
{
  "ticker": "NQ1!",
  "action": "buy",
  "signalPrice": 18250.5,
  "quantity": 2,
  "time": "2025-06-17T10:30:00Z"
}
```

## Required Fields

At minimum, every JSON message sent to TradersPost must include:

* **ticker** — The symbol you want to trade (e.g. `NQ1!` or `MSFT`)
* **action** — The trade action: `buy`, `sell`,  `exit`, `cancel` or `add`&#x20;

Without these two fields, TradersPost won’t know what trade to place.

## Recommended Fields

While not required, we strongly recommend also including:

* **signalPrice** — The price at the time your signal fired
* **time** — A timestamp for when the signal was generated

Providing these values helps you maintain a full record of your signal and enables TradersPost to better track execution slippage and timing.

## All Fields

See our entire [webhook documentation](webhooks.md) page for all the possible fields you can send in a JSON message.
