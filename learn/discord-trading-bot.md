---
description: >-
  This example shows you how to setup an automated trading bot where the signals
  are powered by messages received in a Discord channel.
---

# Discord Trading Bot

To get started, create a new directory where you can test your bot.

```bash
$ mkdir discord-bot
$ cd discord-bot
```

Now install the **symfony/http-client** and **team-reflex/discord-php** dependencies using [composer](https://getcomposer.org).

```bash
$ composer require symfony/http-client
$ composer require team-reflex/discord-php
```

Now create a new file named **bot.php** and paste the following code inside. Be sure to replace the **$token** and **$webhookUrl** variables with your own values.

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
$ php bot.php
```

Now if you go to the channel in Discord where your bot is, you can type messages like the following to send signals to TradersPost.

![](https://traderspost.io/images/docs/bot-examples/discord-bot.png)

This is a simple example, but it should demonstrate to you how you can use TradersPost webhooks to send trade signals from any source with a little bit of custom code. Enjoy!
