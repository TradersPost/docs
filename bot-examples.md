---
description: >-
  The examples in this document intend to demonstrate how you can build trading
  bots but they are not actual real strategies meant to be used live. They are
  purely educational and demonstrative.
---

# Bot Examples

### Trade from Discord

This example allows you to setup a Discord bot that will respond to messages and send trade signals to TradersPost when messages that match a specific pattern are sent to a channel.

To get started, create a new directory where you can test your bot examples:

```bash
$ mkdir botexamples
$ cd botexamples
```

Now install the **symfony/http-client** and **team-reflex/discord-php** dependencies using [composer](https://getcomposer.org).

```bash
$ composer require symfony/http-client
$ composer require php-imap/php-imap
```

Now create a new file named **discordbot.php** and paste the following code inside. Be sure to replace the **$token** and **$webhookUrl** variables with your own values.

```php
<?php

include __DIR__.'/vendor/autoload.php';

use Discord\Discord;
use Discord\Parts\Channel\Message;
use Symfony\Component\HttpClient\HttpClient;

$token = 'paste your discord bot token here';

$discord = new Discord([
    'token' => $token,
]);

$discord->on('ready', function ($discord) {
    $discord->on('message', function ($message, $discord) {
        $content = $message->content;

        preg_match_all('/(BUY|SELL) ([\d+]) ([A-Z]{1,5})/i', $content, $matches);

        if (!isset($matches[3][0])) {
            return;
        }

        $action = strtolower($matches[1][0]);
        $quantity = $matches[2][0];
        $ticker = strtoupper($matches[3][0]);

        $payload = [
            'action' => $action,
            'quantity' => $quantity,
            'ticker' => $ticker,
        ];

        $webhookUrl = 'paste your TradersPost webhook url here';

        $client = HttpClient::create();

        $response = $client->request('POST', $webhookUrl, [
            'json' => $payload
        ]);

        $message->reply($response->getContent());
    });
});

$discord->run();
```

Now you can run the bot.

```bash
$ php discordbot.php
```

Now if you go to the channel in Discord where your bot is, you can type messages like the following to send signals to TradersPost.

![](https://traderspost.io/images/docs/bot-examples/discord-bot.png)

Again, this is purely an educational example to demonstrate the plumbing of how TradersPost works. If you had a strategy tied to the webhook and a subscription for the strategy tied to your broker, then you would have gotten an order in your broker to buy a quantity of 5 TSLA.

To build a real automated trading bot you can combine this example with a service like [Polygon.io](https://polygon.io) to get live real-time market data and build your own completely custom trading strategies and TradersPost can handle the integrations with your broker.

If you are interested building your own custom automated trading strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
