# Using Telegram BOT to interact with Linux shell


Every interaction with Telegram could be accomplished using REST calls but using a library (Python, Node.js or else) helps a lot in programming services.
<br>
For who of  You is interested in Node.js: I've used [Telegraf](https://telegraf.js.org/) package for the same purpose  and it works perfectly.

Now enter into Telegram programming and how we can use telepot API to interact with Linux OS using shell commands, all from Python.

## Modules installation
We need three modules to make this example to work:
* `telepot`: install with `pip3 install`
* `time`: default installation module
* `subprocess`: default installation module

## The code
Let's examine the following example:
```python
import telepot
import time
import subprocess

def on_chat_message(msg):
    content_type, chat_type, chat_id = telepot.glance(msg)
    print("Ricevuto messaggio da Telegram!")
    percorso = msg['text']  #percorso di cui vogliamo visualizzare ls
    
    processo = subprocess.Popen(['ls', percorso], stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    stdout, stderr = processo.communicate()
    
    elenco = stdout.decode("utf-8").split("\n")
    
    lista = ""
    for x in elenco:
        lista += "\n" + x
    print(lista)
    bot.sendMessage(chat_id, 'ho ricevuto questo: %s'%lista)      

TOKEN = 'yourTokenFromBOTfather'

bot = telepot.Bot(TOKEN)
bot.message_loop(on_chat_message)

print('Listening ...')

while True:
    pass


```

## Prepare our BOT
We have to create a BOT using BOT Father (a particular Telegram BOT).
We won't see how it could be accomplished, you can find a lot of tutorials online that clearly show that.
During creating process take note of name you are giving to your BOT. That will be necessary when it'll be time to send messages to BOT using smart phone (or Telegram application on your PC).
At the end of BOT creation Telegram will send us a token, and we have to copy and paste it as value of string TOKEN above.

## How to make it work
Let's run above script, for example with name ```telgramTest.py```, then run it as python3 ```telegramTest.py```.
If always gos the right way our script prompts telling that it's ```Listening...```. Now it's time to connect to our BOT with smart phone and then send a message to it. That message is be the path whose we want to retrive files list.
That list we'll be promptef back to our smart phone.
