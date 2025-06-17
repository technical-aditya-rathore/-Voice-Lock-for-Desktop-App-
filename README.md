# Voice-Lock-for-Desktop-App-
------------------------------------------------------------------
## 🔐🎙️ Voice Lock for Desktop App – Overview

### ✅ Features:

* Set your **voice password** once (e.g., “Open my system”)
* Every time you run the program, it asks you to **speak the passphrase**
* If the voice matches, you get access (opens a secret message/app)
* If not, it denies access

---

## 🛠️ Technologies & Libraries Used:

* `speech_recognition` – for converting speech to text
* `pyaudio` – to access microphone
* `os` – to open a program/file after access
* `pickle` – to save and load your voice password as text

---

## ✅ Step-by-Step Code (Console-based version)

### 1. Install Dependencies First:

```bash
pip install SpeechRecognition pyaudio
```

---

### 2. Python Code: `voice_lock.py`

```python
import speech_recognition as sr
import pickle
import os

def record_voice(prompt):
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print(prompt)
        r.adjust_for_ambient_noise(source)
        audio = r.listen(source)
        try:
            voice_text = r.recognize_google(audio)
            print("You said:", voice_text)
            return voice_text
        except sr.UnknownValueError:
            print("Sorry, I couldn't understand your voice.")
            return None
        except sr.RequestError:
            print("Network error.")
            return None

def set_password():
    voice_pass = record_voice("Speak your voice password to set:")
    if voice_pass:
        with open("voice_password.pkl", "wb") as f:
            pickle.dump(voice_pass, f)
        print("Voice password saved successfully!")

def authenticate():
    try:
        with open("voice_password.pkl", "rb") as f:
            saved_pass = pickle.load(f)
    except FileNotFoundError:
        print("No password set. Please run and set your voice password first.")
        return
    
    voice_input = record_voice("Speak your voice password to unlock:")
    if voice_input == saved_pass:
        print("Access Granted ✅")
        # Example action: open a secret file or app
        print("Welcome to your secure zone.")
        # os.startfile("secret.txt")  # optional
    else:
        print("Access Denied ❌")

# Main Menu
print("\n--- Voice Lock System ---")
print("1. Set Voice Password")
print("2. Unlock with Voice")
choice = input("Enter your choice: ")

if choice == "1":
    set_password()
elif choice == "2":
    authenticate()
else:
    print("Invalid choice.")
```

---

## 🔏 How It Works:

1. **User sets a voice passphrase** (like "unlock the door").
2. It saves the phrase text using `pickle`.
3. When run again, it compares new speech to stored phrase.
4. If it matches — user is authenticated.

---

## 🚀 Next Steps (Optional Advanced Ideas):

* 🔒 Add **encryption** to the stored voice password.
* 🎨 Create a **GUI** with `Tkinter`.
* 🎙️ Add retry limit & lockout system.
* 🖥️ Launch actual software (e.g., Notepad or secret folder) after success.

---

Owner Name:- ADITYA KUMAR JHA
If you like our projects then follow for more such like.
Feel free to ask any doubt queries regarding projects.
Thanks for Watching'.
