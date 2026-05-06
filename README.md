# 🎙️ CORTEX — Multilingual Voice Agent

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python"/>
  <img src="https://img.shields.io/badge/Whisper-Faster--Whisper-orange?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/NLU-Rasa-purple?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Vision-OpenCV-green?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Backend%20Complete-brightgreen?style=for-the-badge"/>
</p>

> A privacy-focused, **100% offline** multilingual desktop voice agent that understands **English, Malayalam & Hindi** — powered by Whisper, Rasa NLU, OpenCV, and PyAutoGUI for hands-free desktop automation.

---

## 🧠 What is CORTEX?

CORTEX is a local-first AI voice agent built for Linux desktops. Unlike cloud-based assistants (Google Assistant, Siri), CORTEX runs **entirely on your machine** — no internet required, no data sent to any server.

It listens for a wake word, understands your voice commands in Malayalam, Hindi, or English, and automates desktop tasks like sending WhatsApp messages and emails — all hands-free.

---

## ✨ Features

- 🎙️ **Wake Word Detection** — Say *"Nova"* or press `Left Shift` to activate
- 🌐 **Multilingual** — Natively understands Malayalam, Hindi & English
- 🔒 **100% Offline** — Zero cloud dependency for core processing
- 🧠 **Smart NLU** — Rasa-powered intent & entity recognition
- 🖥️ **Desktop Automation** — Controls any GUI app via OpenCV + PyAutoGUI
- 📧 **Email Automation** — Drafts and sends emails hands-free
- 💬 **WhatsApp Messaging** — Sends WhatsApp messages via automation
- 🔊 **Audio Pipeline** — Noise reduction, bandpass filtering, VAD gating
- ⚡ **Optimized** — Runs on standard consumer hardware (CPU, int8)

---

## 🏗️ Architecture

```
Voice Input (Mic)
      ↓
Wake Word Detection (SpeechRecognition / Left Shift)
      ↓
Audio Recording (PyAudio)
      ↓
Audio Pre-processing Pipeline
  ├── Bandpass Filter (80Hz – 7.8kHz)
  ├── Noise Reduction (noisereduce)
  └── VAD Gate (webrtcvad)
      ↓
Speech-to-Text + Translation (Faster-Whisper)
  └── Malayalam / Hindi → English
      ↓
Intent Classification (Rasa NLU)
      ↓
Desktop Automation
  ├── WhatsApp (PyAutoGUI + OpenCV)
  └── Email (PyAutoGUI + OpenCV)
```

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Speech-to-Text | OpenAI Whisper (fine-tuned, via Faster-Whisper) |
| NLU / Intent | Rasa 3.6 |
| Desktop Automation | PyAutoGUI + OpenCV |
| Audio Processing | PyAudio, noisereduce, webrtcvad, scipy |
| Language | Python 3.10 |
| Platform | Linux |

---

## 📁 Project Structure

```
voice-agent/
│
├── main.py                  # Main execution loop
├── audio_pipeline.py        # Audio recording, cleaning & transcription
├── config.yaml              # Rasa / project configuration
├── requirements.txt         # All dependencies
├── Dataset_training_code.py # Whisper fine-tuning script (Google Colab)
├── training_data_set.txt    # Malayalam training sentences + translations
│
└── src/
    └── automation/
        ├── whatsapp.py      # WhatsApp automation logic
        └── email.py         # Email automation logic
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- Linux OS
- Rasa server running locally
- Microphone

### Installation

```bash
# Clone the repo
git clone https://github.com/mshahinn/voice-agent.git
cd voice-agent

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Run

```bash
# Start Rasa server (in a separate terminal)
rasa run --enable-api

# Start CORTEX
python main.py
```

### Usage

1. Run `main.py`
2. Say **"Nova"** or press `Left Shift` to wake CORTEX
3. Speak your command in Malayalam, Hindi, or English
4. Press `Right Shift` to finish speaking
5. CORTEX will process and execute your command

**Example commands (Malayalam):**
> *"ദീപക്കിന് ഒരു മെസ്സേജ് അയക്കുക, ഞാൻ ട്രാഫിക്കിൽ പെട്ടു"*
> → Sends WhatsApp message to Deepak: *"I am stuck in traffic"*

---

## 🔧 Configuration

Edit `main.py` to set up your contact book:

```python
CONTACT_BOOK = {
    "name": "email@example.com",
}
```

Edit `audio_pipeline.py` to change language:

```python
LANGUAGE = "ml"   # "ml" = Malayalam | "hi" = Hindi | "en" = English
```

---

## 📊 Model Training

The custom Malayalam Whisper model was fine-tuned using:
- **Base model:** `openai/whisper-medium`
- **Method:** LoRA (Low-Rank Adaptation) + 8-bit quantization
- **Task:** Malayalam → English translation
- **Platform:** Google Colab (T4 GPU)
- **Output format:** CTranslate2 (int8) for fast CPU inference

Training code: [`Dataset_training_code.py`](./Dataset_training_code.py)

---

## 🔮 Roadmap

- [x] Audio pipeline with noise reduction & VAD
- [x] Multilingual STT (Malayalam, Hindi, English)
- [x] Rasa NLU integration
- [x] WhatsApp & Email automation
- [ ] Frontend dashboard (coming soon)
- [ ] Mobile platform support
- [ ] More language support (Tamil, Telugu)

---

## 👨‍💻 Author

**Mohamad Shahin Nechithadayan**
B.Tech Computer Science & Engineering
Cochin University College of Engineering Kuttanad (CUCEK), CUSAT

---

## 📄 License

This project is licensed under the [MIT License](./LICENSE).
