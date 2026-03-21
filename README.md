# 🗓️ Automatic Scheduling (Text & Voice)

An intelligent scheduling automation built with n8n that handles both **text and voice**
inputs via Telegram, powered by an AI Agent connected to Google Calendar,
Google Sheets, and Gmail.

---

## 🔍 Overview

Automatic Scheduling is an AI-powered workflow automation that acts as your
personal scheduling assistant on Telegram. Instead of manually opening your
calendar and creating events, you simply send a message — by text or voice —
and the system handles everything for you.

The workflow is built on **n8n**, an open-source automation platform, and
leverages **OpenAI** for natural language understanding, voice transcription,
and audio response generation. It integrates seamlessly with **Google Calendar**
for event creation, **Google Sheets** for record keeping, and **Gmail** for
sending confirmation emails — all triggered from a single Telegram message.

Whether you prefer typing or talking, the bot understands your request,
creates the event, logs it, notifies you, and replies back — all in seconds.

---

## 🔄 Workflow Structure
```
Telegram Trigger
      │
      ▼
   [If: Text or Voice?]
      │                  │
   [Text]             [Voice]
      │                  │
      │           Get Audio File
      │                  │
      │        Transcribe Recording
      │                  │
      └──────► AI Agent ◄┘
          │        │       │
    Calendar     Sheets   Gmail
                  │
          [If1: Response Type?]
                  │                    │
              [Text]               [Voice]
                  │                    │
         Send Text Message      Generate Audio
                                       │
                               Send Audio File
```

### 🔵 The workflow operates in the following sequence:

**1. Telegram Trigger**
Listens for any incoming message from the Telegram bot — either a text message
or a voice note. This is the entry point of the entire workflow.

**2. If (Text or Voice?)**
The first decision node. It checks whether the incoming message is:
- **True → Text:** Routes directly to the AI Agent for processing
- **False → Voice:** Routes to the voice processing branch (Get a file → Transcribe)

**3. Get a File** *(Voice branch only)*
Downloads the voice message audio file sent by the user on Telegram,
making it available for transcription in the next step.

**4. Transcribe a Recording** *(Voice branch only)*
Uses **OpenAI Whisper** to convert the downloaded audio file into text,
so the AI Agent can understand and process the spoken scheduling request.

**5. AI Agent**
The brain of the workflow. Receives the text (either directly or transcribed
from voice) and processes the scheduling request using natural language.
It is connected to three tools:
- 🗓️ **Google Calendar** — to create events
- 📊 **Google Sheets** — to log scheduling data
- 📧 **Gmail** — to send confirmation emails

It also uses:
- **OpenAI Chat Model** — as the underlying language model
- **Simple Memory** — to retain conversation context across messages,
  allowing it to remember previous interactions in the same session

**6. If1 (Response Type?)**
The second decision node. After the AI Agent processes the request, it decides
how to respond:
- **True → Text:** Sends a text reply back via Telegram
- **False → Voice:** Generates an audio response and sends it as a voice message

**7. Send a Text Message** *(Text response branch)*
Sends the AI Agent's reply back to the user as a **text message** on Telegram.

**8. Generate Audio** *(Voice response branch)*
Uses **OpenAI TTS (Text-to-Speech)** to convert the AI Agent's text response
into a natural-sounding audio file.

**9. Send an Audio File** *(Voice response branch)*
Sends the generated audio file back to the user as a **voice message** on Telegram,
completing the voice interaction loop.

---

## ⚙️ How It Works

1. You send a **text or voice message** to the Telegram bot with a scheduling request
   (e.g., *"Schedule a meeting with Ahmed tomorrow at 3pm"*)
2. If it's a **voice message**, the workflow downloads the audio and transcribes it
   using OpenAI Whisper into text
3. The **AI Agent** receives the text and understands the scheduling intent using
   natural language processing
4. The AI Agent automatically:
   - Creates the event in **Google Calendar**
   - Logs the details in **Google Sheets**
   - Sends a confirmation email via **Gmail**
5. The AI Agent then generates a response and sends it back to you either as a
   **text message** or a **voice message** depending on how you communicated

---

## 💡 Use Cases

- **Busy professionals** who want to schedule meetings by simply sending a voice note
- **Teams** that need automated event creation without manual calendar management
- **Individuals** who prefer talking or texting to schedule their day naturally
- **Businesses** that want to log all scheduled events automatically in Google Sheets
- **Anyone** who wants a smart personal assistant available 24/7 on Telegram

---

## 🛠️ Setup

1. Clone or import the workflow into your n8n instance
2. Configure the following credentials:
   - Telegram Bot Token
   - OpenAI API Key (Whisper + TTS + Chat Model)
   - Google Calendar OAuth
   - Google Sheets OAuth
   - Gmail OAuth
3. Set your Google Sheet ID and Calendar ID in the relevant nodes
4. Activate the workflow
5. Start chatting or sending voice notes to your Telegram bot!

---

## 🌟 Benefits

- **⚡ Saves Time** — No need to manually open Google Calendar and create events;
  just send a message and it's done automatically
- **🎙️ Hands-Free Scheduling** — Voice support means you can schedule while driving,
  walking, or doing anything else
- **🧠 Naturally Smart** — The AI Agent understands natural language, so you don't
  need to use any specific commands or formats
- **📋 Automatic Logging** — Every scheduled event is logged in Google Sheets,
  giving you a full record of all appointments
- **📧 Instant Confirmation** — Automatic Gmail notifications keep you and others
  informed right after an event is created
- **💬 Conversational Memory** — The bot remembers context within a session,
  so you can follow up or modify requests naturally
- **🔄 Flexible Input & Output** — Supports both text and voice in both directions,
  adapting to however you prefer to communicate
- **📱 Always Accessible** — Works directly inside Telegram, an app you already use,
  with no extra tools or interfaces needed

---

| Tool | Purpose |
|------|---------|
| n8n | Workflow automation |
| Telegram Bot | Input/output interface (text & voice) |
| OpenAI Whisper | Voice transcription |
| OpenAI TTS | Audio response generation |
| OpenAI Chat Model | AI scheduling agent |
| Simple Memory | Conversation context retention across messages |
| Google Calendar | Event creation |
| Google Sheets | Data logging |
| Gmail | Email notifications |
| v1.0.0 | Initial release |
