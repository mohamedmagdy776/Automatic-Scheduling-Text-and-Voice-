# 🗓️ Automatic Scheduling (Text & Voice)

An intelligent scheduling automation built with n8n that handles both **text and voice** 
inputs via Telegram, powered by an AI Agent connected to Google Calendar, 
Google Sheets, and Gmail.

---

## 🚀 Features

### 🔤 Text Mode
- Receives text messages via Telegram
- AI Agent processes scheduling requests using natural language
- Creates events in Google Calendar automatically
- Logs scheduling data to Google Sheets
- Sends confirmation emails via Gmail
- Replies with a text message on Telegram

### 🎙️ Voice Mode
- Receives voice messages via Telegram
- Downloads the audio file automatically
- Transcribes the recording using OpenAI Whisper
- AI Agent processes the transcribed scheduling request
- Generates an audio response using OpenAI TTS
- Sends the audio reply back via Telegram

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| n8n | Workflow automation |
| Telegram Bot | Input/output interface (text & voice) |
| OpenAI (Whisper) | Voice transcription |
| OpenAI (TTS) | Audio response generation |
| OpenAI Chat Model | AI scheduling agent |
| Simple Memory | Conversation context retention |
| Google Calendar | Event creation |
| Google Sheets | Data logging |
| Gmail | Email notifications |

---

## 🔄 Workflow Overview
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
                  │
          [If: Response Type?]
                  │                    │
              [Text]               [Voice]
                  │                    │
         Send Text Message      Generate Audio
                                       │
                               Send Audio File
```

---

## ⚙️ Setup

1. Clone or import the workflow into your n8n instance
2. Configure the following credentials:
   - Telegram Bot Token
   - OpenAI API Key
   - Google Calendar OAuth
   - Google Sheets OAuth
   - Gmail OAuth
3. Set your Google Sheet ID and Calendar ID in the relevant nodes
4. Activate the workflow
5. Start chatting or sending voice notes to your Telegram bot!

---

## 📌 Notes

- The AI Agent uses **Simple Memory** to retain context across messages
- Voice messages are transcribed before being passed to the AI Agent
- Both text and voice responses are supported depending on input type
- This is the v1.0.0 initial release
