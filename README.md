# What is this?
This is telegram bot, it receives text and responds the same message with robotic vboice in. By uncummenting few lines of code you can forward this text to locally run Ollama and return return the result voiceover. Text-to-speach (TTS) is performed by locally run tool Balabolkawith preinstalled robotic voice.

## How to create bot?
- Open Telegram and search for BotFather (it’s an official Telegram bot for creating and managing other bots).
- Start a chat with BotFather and type /newbot to create a new bot.
- BotFather will ask you to provide a name for your bot. Choose a name that you want your bot to be identified by.
- After you provide a name, it will ask for a username. The username must be unique and must end with bot (e.g., myamazingbot).
- After creating the bot, BotFather will give you a token.

Save this token. Do not worry if you loose it - you can always open BotFather, get list of your bots and request tokens for each of them.

## Update environment variables
In the same folder with script create file named ".env". Use exactly this name, just 4 symbols.
In this file add text
```
BOT_TOKEN='<TOKEN_FOR_YOUR_BOT>'
HOSTNAME='<YOUR_HOSTNAME_OR_IP>'
```
Ex.
```
BOT_TOKEN='8030XXXXXX:AAHtR5F3H6WUYvAItQa2THEIFoEDbXXXXXX'
HOSTNAME='118-YYY-71-83-67'
```

## Setting up a webhook
Before using telegram you need to set up sebhook. 
If you have public IP, then simply run the script and visit http://your-server-ip-or-domain:5000/setwebhook to set the webhook URL. This will configure Telegram to send updates to your bot.<br>
If you don't have public IP then:
- Run the script on local machine
- Register for free on [ngrok.com](https://ngrok.com). Sign in. After signing in, go to the "Get Started" page and copy your authtoken.
- Download ngrok from [ngrok.com](https://ngrok.com). Unzip downloaded file ex. in script folder.
- Run "ngrok config add-authtoken"
- Run command "ngrok http 5000". Pay attention that port is not 80 (default), but 5000, because script creates local server on this port. When ngrok started, it will give you URL, ex. "https://b\<your IP address\>.ngrok-free.app"
- To set the webhook URL, visit URL https://api.telegram.org/bot\<YOUR_BOT_TOKEN\>/setWebhook?url=\<IP address which ngrock shows\>/\<YOUR_BOT_TOKEN\>. Ex. "https://api.telegram.org/bot8030XXXXXX:AAHtR5F3H6WUYvAItQa2THEIFoEDbXXXXXX/setWebhook?url=https://b118-YYY-71-83-67.ngrok-free.app/8030XXXXXX:AAHtR5F3H6WUYvAItQa2THEIFoEDbXXXXXX". In case of success, you will receive json like this "{"ok":true,"result":true,"description":"Webhook was set"}"

## How to test bot
Now you can search in Telegram bot with your name, ex "myamazingbot". Start conversation and send something. In logs of your script you should be able to see this message, printed from handle_message() method.

## How to install local TTS (Text-to-speach)
**Note!** You can use remote TTS, ex. from ChatGPT. You don't have to use local one. I used local just because it is free.<br>
I assume you can use many applications for local TTS. In my case I used Balabolka tool, in particular, its CLI tool called "balcon" (https://www.cross-plus-a.com/ru/bconsole.html). After tool installation you need to install voices. Pay attention that some voices free, some are not. Write name of voice in script variable TTS_VOICE_NAME. In my case it is 'Maxim'.<br>
Note that if voice, which you use, supports only one language, you should send to TTS text in this language only.
Take into account that TTS results (.mp3 files) will be stored inside script folder. THey are going to be deleted when they are sent back to user, but in case of any failures, you may need to delete them manually.

## Limitations
This bot is created just for fun. It is quite unstable, so you may need to fix some bugs when you find them. Bot is also not intendend to be used in parallel by many users. So, if you need this feature you may need to make slight changes in script.