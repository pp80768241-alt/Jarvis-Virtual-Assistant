# 🤖 Jarvis Virtual Assistant

A Python-based **voice-controlled virtual assistant** inspired by JARVIS from Iron Man.

Jarvis listens for the wake word **"Jarvis"**, accepts voice commands, performs predefined actions such as opening websites, playing music, and fetching news, and can use the **OpenAI API** to answer general questions through AI-generated responses.

---

## ✨ Features

- 🎙️ **Voice Recognition** — Understands spoken commands through the microphone.
- 🟢 **Wake Word Detection** — Activates when you say **"Jarvis"**.
- 🗣️ **Text-to-Speech** — Responds to the user using generated speech.
- 🌐 **Website Automation** — Opens websites such as Google, Facebook, YouTube, and LinkedIn.
- 🎵 **Music Playback** — Plays configured songs using links stored in the music library.
- 📰 **News Updates** — Fetches and reads top news headlines using NewsAPI.
- 🧠 **AI-Powered Responses** — Uses OpenAI to handle general questions and commands that aren't predefined.
- 🔊 **Audio Playback** — Uses `pygame` to play generated speech audio.

The current implementation uses SpeechRecognition/Google Speech Recognition for voice input, gTTS and Pygame for voice output, OpenAI for AI responses, and NewsAPI for headlines. citeturn0view0turn1view0

---

## 🧠 How It Works

The assistant follows this basic workflow:

```text
             🎙️ Microphone
                   │
                   ▼
        Speech Recognition
                   │
                   ▼
          Detect "Jarvis"
                   │
                   ▼
           Listen for Command
                   │
                   ▼
          ┌────────┴─────────┐
          │                  │
     Known Command      Unknown Command
          │                  │
          ▼                  ▼
   Perform Action       OpenAI API
          │                  │
          └────────┬─────────┘
                   ▼
            Generate Response
                   │
                   ▼
             Text-to-Speech
                   │
                   ▼
              🔊 Audio
```

The main control flow is implemented in `main.py`. It continuously listens through the microphone, checks for the wake word, captures a command, and passes it to the command-processing function. citeturn1view0

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Core programming language |
| **SpeechRecognition** | Converts spoken audio into text |
| **Google Speech Recognition** | Speech recognition backend |
| **gTTS** | Converts text into speech |
| **Pygame** | Plays generated audio |
| **OpenAI API** | Generates AI-powered responses |
| **NewsAPI** | Retrieves news headlines |
| **Webbrowser** | Opens websites |
| **python-dotenv** | Loads environment variables |
| **Requests** | Sends HTTP requests to APIs |

The repository's current README identifies Python, SpeechRecognition, Google Speech Recognition, gTTS, Pygame, OpenAI API, and NewsAPI as the project's technologies. citeturn0view0

---

## 📁 Project Structure

```text
Jarvis-Virtual-Assistant/
│
├── main.py
├── client.py
├── musicLibrary.py
├── test_voice.py
├── .gitignore
└── README.md
```

### `main.py`

The main application file.

It handles:

- Speech recognition
- Wake-word detection
- Voice commands
- Website opening
- Music playback
- News retrieval
- OpenAI requests
- Text-to-speech
- Continuous listening

The current `main.py` contains the main assistant loop and command-processing logic. citeturn1view0

### `client.py`

A small standalone OpenAI API example.

It creates an OpenAI client, sends a sample prompt, and prints the generated response. citeturn1view1

### `musicLibrary.py`

Contains the music dictionary used by the assistant when a user gives a `play` command. `main.py` looks up the requested song in `musicLibrary.music` and opens its associated link. citeturn1view2

### `test_voice.py`

A separate voice-related testing script used during development.

---

## ⚙️ Requirements

Before running Jarvis, make sure you have:

- Python 3.x
- A working microphone
- Speakers or headphones
- Internet connection
- OpenAI API access
- NewsAPI access
- Required Python packages

Because the assistant uses Google Speech Recognition and online APIs, an internet connection is required for the current implementation. citeturn1view0

---

## 📦 Installation

### 1. Clone the repository

```bash
git clone https://github.com/pp80768241-alt/Jarvis-Virtual-Assistant.git
```

### 2. Enter the project directory

```bash
cd Jarvis-Virtual-Assistant
```

### 3. Install dependencies

If the repository contains a `requirements.txt` file in your local working version:

```bash
pip install -r requirements.txt
```

Otherwise, install the packages used by the current source:

```bash
pip install SpeechRecognition
pip install pyttsx3
pip install requests
pip install openai
pip install gTTS
pip install pygame
pip install python-dotenv
pip install PyAudio
```

> **Note:** PyAudio installation can require additional setup on some Windows systems.

---

## 🔑 API Configuration

Jarvis uses external APIs for AI responses and news.

### OpenAI API

The current source creates an OpenAI client and sends requests to:

```text
gpt-3.5-turbo
```

The API key in the repository is represented as a placeholder rather than a real secret. citeturn1view0turn1view1

For local development, use an environment variable rather than placing a real API key directly in your source code.

Example `.env`:

```env
OPENAI_API_KEY=your_openai_api_key
NEWS_API_KEY=your_newsapi_key
```

Then load the values in Python:

```python
import os
from dotenv import load_dotenv

load_dotenv()

openai_api_key = os.getenv("OPENAI_API_KEY")
news_api_key = os.getenv("NEWS_API_KEY")
```

> ⚠️ **Never commit your real API keys to GitHub.**

---

## ▶️ Running Jarvis

Start the assistant with:

```bash
python main.py
```

When the program starts, Jarvis initializes and begins listening.

Say:

```text
Jarvis
```

The assistant will respond and then listen for your command.

For example:

```text
You: Jarvis

Jarvis: Ya

You: Open YouTube
```

Jarvis will open YouTube in the browser.

---

## 🎤 Voice Commands

The current implementation supports several predefined commands.

### 🌐 Open Websites

Say:

```text
Jarvis
Open Google
```

Supported websites currently include:

```text
Google
Facebook
YouTube
LinkedIn
```

These commands are handled directly by `processCommand()` in `main.py`. citeturn1view0

---

### 🎵 Play Music

The assistant supports commands beginning with:

```text
play
```

For example:

```text
Play <song>
```

The song name is looked up in `musicLibrary.py`, and the associated link is opened in the browser. citeturn1view0turn1view2

To add another song, add it to the music dictionary in `musicLibrary.py`.

Example:

```python
music = {
    "song_name": "https://example.com/song"
}
```

---

### 📰 News

Say:

```text
Jarvis
News
```

Jarvis sends a request to NewsAPI, retrieves the available top headlines, and reads the article titles aloud. The current implementation requests top headlines for the United States. citeturn1view0

---

### 🧠 General Questions

If a command doesn't match one of the predefined actions, Jarvis sends the command to OpenAI.

For example:

```text
Jarvis
What is artificial intelligence?
```

The assistant sends the question to the configured OpenAI model and speaks the generated answer. citeturn1view0

---

## 🔄 Command Processing

The assistant uses a command-processing function that roughly follows this logic:

```text
User speaks
     │
     ▼
Speech → Text
     │
     ▼
Is it a known command?
     │
 ┌───┴────┐
 │        │
Yes       No
 │        │
 ▼        ▼
Action   OpenAI
 │        │
 └───┬────┘
     ▼
Text Response
     │
     ▼
Voice Output
```

Known commands are handled locally, while other requests are passed to the AI model. citeturn1view0

---

## 🔊 Text-to-Speech

The project currently contains two `speak()` implementations in `main.py`.

The active implementation uses:

```text
gTTS → temp.mp3 → Pygame → Audio
```

The generated speech is temporarily saved as `temp.mp3`, played through Pygame, and then removed after playback. citeturn1view0

---

## 🔐 Security

API keys should **never** be hard-coded into a public repository.

Recommended `.gitignore` entries:

```gitignore
.env
.env.local
__pycache__/
*.pyc
temp.mp3
```

If a real API key has previously been committed to a public GitHub repository:

1. Revoke the exposed key.
2. Generate a new key.
3. Store the new key using environment variables.
4. Remove the secret from the repository history if necessary.

---

## ⚠️ Current Limitations

This project is a **learning-focused virtual assistant**, and the current implementation has some limitations.

### 1. Internet dependency

Speech recognition, AI responses, and news retrieval rely on online services.

### 2. Limited predefined commands

Only a small number of actions are currently recognized directly:

- Open Google
- Open Facebook
- Open YouTube
- Open LinkedIn
- Play music
- Fetch news

Other commands are sent to OpenAI. citeturn1view0

### 3. Music library lookup

Songs must exist in the configured `musicLibrary` dictionary.

### 4. Wake-word recognition

The current implementation relies on Google Speech Recognition to recognize the word `"Jarvis"` rather than using a dedicated offline wake-word engine. citeturn1view0

### 5. API configuration

The current source still contains placeholder API-key values that need to be replaced with properly configured environment variables before the application can use the APIs. citeturn1view0

---

## 🧪 Example Session

```text
Jarvis: Initializing Jarvis....

Listening...

User: Jarvis

Jarvis: Ya

Jarvis Active...

User: Open YouTube

→ YouTube opens in the browser
```

Another example:

```text
User: Jarvis

Jarvis: Ya

User: What is machine learning?

→ Command is sent to OpenAI

Jarvis: Machine learning is...
```

---

## 🚀 Future Improvements

The project can be expanded into a much more capable desktop AI assistant.

### 🔹 Better Wake-Word Detection

Use dedicated wake-word technology such as:

- Porcupine
- OpenWakeWord
- Custom wake-word models

This would reduce unnecessary API calls and improve responsiveness.

### 🔹 Offline Speech Recognition

Add an offline speech-to-text engine such as Whisper.

This would reduce dependency on online speech recognition.

### 🔹 More System Controls

Add commands for:

- Opening applications
- Closing applications
- Volume control
- System information
- Battery status
- Wi-Fi/Bluetooth control
- Taking screenshots
- File management

### 🔹 Better AI Integration

Upgrade the AI layer to support:

- Conversation history
- Context-aware responses
- Tool/function calling
- Multiple AI models
- Streaming responses

### 🔹 GUI

Create a desktop interface showing:

```text
┌─────────────────────────────┐
│          JARVIS             │
│                             │
│   🎙️ Listening...           │
│                             │
│   User: Open YouTube        │
│   Jarvis: Opening YouTube   │
│                             │
└─────────────────────────────┘
```

### 🔹 Personalized Commands

Allow users to define their own commands and actions through a configuration file.

### 🔹 Better Error Handling

Improve handling for:

- Microphone failures
- API failures
- Network problems
- Unknown songs
- Speech recognition errors
- Missing API keys

---

## 📚 Learning Outcomes

This project demonstrates practical experience with:

- Python programming
- Functions
- Conditional statements
- Loops
- Exception handling
- API integration
- Speech recognition
- Text-to-speech
- HTTP requests
- JSON/API responses
- Environment variables
- Browser automation
- AI integration
- Modular Python code

---

## 🎯 Project Goal

The main goal of this project is to explore how Python can combine:

```text
Voice Recognition
       +
AI
       +
APIs
       +
Automation
       +
Text-to-Speech
       ↓
Virtual Assistant
```

The project serves as a foundation for building a more advanced personal AI assistant capable of interacting with both the user and the computer.

---

## ⚠️ Disclaimer

This project is an independent educational project inspired by the fictional JARVIS assistant from the Iron Man universe.

It is **not affiliated with Marvel, Disney, OpenAI, Google, NewsAPI, or any other third-party service used by the project**.

Use third-party APIs according to their respective terms and policies.

---

## 👨‍💻 Author

**Prince Panwar**

B.Tech Computer Science & Engineering — Data Science

GitHub:  
https://github.com/pp80768241-alt

---

## ⭐ Support

If you found this project useful or interesting, consider giving the repository a ⭐ on GitHub.

---

## 📄 License

This repository currently does not specify a license.

If you intend to distribute the project as open source, consider adding an appropriate license such as the MIT License.
