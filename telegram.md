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
#temperature della CPU di Rapsberry: /opt/vc/bin/vcgencmd measure_temp        

TOKEN = '798563573:AAFNDB44IQXK0LQz1xSo-CBHv_Llw3i423k'

bot = telepot.Bot(TOKEN)
bot.message_loop(on_chat_message)

print('Listening ...')

while True:
    pass


```