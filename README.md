# 🎙️ AI Podcast Co-Host

**Human-like conversational AI podcast co-host with GPT-4, ElevenLabs voice synthesis, real-time interaction, and Riverside.fm integration**

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/thehillfire/ai-podcast-cohost.git
cd ai-podcast-cohost

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your API keys

# Run the application
python app/main.py

# Open browser
http://localhost:8000
```

## ✨ Features

- **🗣️ Human-like AI Co-Host**: Meet Alex - warm, quirky, conversationally natural
- **📝 Script Ingestion**: Upload CSV/Excel spreadsheets with segment questions
- **🤖 Real-Time Adaptation**: GPT-4 powered follow-ups within 1.5s latency
- **🎵 Studio-Quality Voice**: ElevenLabs TTS with -16 LUFS stereo / -19 LUFS mono
- **🔄 Live Interaction**: WebSocket-based real-time dialogue management
- **📊 Control Dashboard**: Browser-based UI for episode management
- **🎬 Riverside.fm Ready**: Audio outputs integrate seamlessly
- **🔓 No Vendor Lock-in**: Full source code, customize everything

## 📋 Deliverables

✅ **Character Brief**: Complete Alex personality guide ([CHARACTER_BRIEF.md](CHARACTER_BRIEF.md))  
✅ **Voice Model**: ElevenLabs configuration with usage instructions  
✅ **Script Ingestion**: CSV parser turns spreadsheets into AI prompts  
✅ **Real-Time Logic**: Adaptive follow-ups with fallback phrases  
✅ **Quick-Start Guide**: This README + full documentation  
✅ **Demo-Ready**: Test first episode flow immediately

## 🎯 Acceptance Criteria Met

- ✅ AI asks every pre-scripted question
- ✅ Follow-ups generated within 1.5s latency
- ✅ Audio output: −16 LUFS stereo / −19 LUFS mono
- ✅ Full code, prompts, settings supplied
- ✅ No vendor lock-in - complete source access

## 🏗️ Project Structure

```
ai-podcast-cohost/
├── app/
│   ├── main.py                 # FastAPI application entry point
│   ├── models.py               # Data models for episodes, questions, sessions
│   ├── ai_engine.py            # GPT-4 conversation logic
│   ├── voice_synthesis.py      # ElevenLabs integration
│   ├── audio_processing.py     # LUFS normalization
│   ├── script_parser.py        # CSV/Excel question ingestion
│   └── websocket_handler.py    # Real-time communication
├── frontend/
│   ├── index.html              # Control dashboard UI
│   ├── script.js               # Dashboard logic
│   └── style.css               # UI styling
├── audio_output/               # Generated audio files
├── scripts/                    # Uploaded question spreadsheets
├── CHARACTER_BRIEF.md          # Alex personality documentation
├── requirements.txt            # Python dependencies
├── .env.example                # Environment configuration template
└── README.md                   # This file
```

## 🔧 Installation

### Prerequisites

- Python 3.9 or higher
- OpenAI API key (for GPT-4)
- ElevenLabs API key (for voice synthesis)
- FFmpeg (for audio processing)

### Step 1: Clone Repository

```bash
git clone https://github.com/thehillfire/ai-podcast-cohost.git
cd ai-podcast-cohost
```

### Step 2: Install Python Dependencies

```bash
pip install fastapi uvicorn openai elevenlabs pandas openpyxl ffmpeg-python pydub websockets python-multipart
```

Or use the requirements file:

```bash
pip install -r requirements.txt
```

### Step 3: Install FFmpeg

**Windows:**
```bash
choco install ffmpeg
```

**macOS:**
```bash
brew install ffmpeg
```

**Linux:**
```bash
sudo apt-get install ffmpeg
```

### Step 4: Configure Environment

Create `.env` file:

```env
OPENAI_API_KEY=your_openai_key_here
ELEVENLABS_API_KEY=your_elevenlabs_key_here
VOICE_ID=your_selected_voice_id
PORT=8000
TARGET_LUFS=-16
```

## 🎤 Meet Alex - Your AI Co-Host

See [CHARACTER_BRIEF.md](CHARACTER_BRIEF.md) for complete personality documentation.

**Quick Personality Summary:**
- Former indie DJ with warm, quirky energy
- Conversational and genuinely curious
- Uses natural language, never robotic
- Adapts follow-ups based on guest responses
- Light humor without being overwhelming

## 📚 How to Use

### 1. Prepare Your Episode Script

Create a CSV file with your segment questions:

**example_episode.csv:**
```csv
Segment,Question,Notes
Opening,What inspired you to start this journey?,Warm opener
Challenge,What was your biggest obstacle?,Dig deeper here
Success,Tell us about your proudest moment,Celebrate wins
Future,Where do you see this going next?,Forward-looking
```

### 2. Upload Script via Dashboard

1. Run the application: `python app/main.py`
2. Open http://localhost:8000
3. Click "Upload Script"
4. Select your CSV file
5. Review parsed questions

### 3. Start Episode Recording

1. Click "Start Episode"
2. Alex will open with the first question
3. System listens for guest response
4. Alex generates contextual follow-up
5. Audio saved to `audio_output/`

### 4. Export for Riverside.fm

Generated audio files are automatically normalized to:
- **Stereo**: −16 LUFS
- **Mono**: −19 LUFS

Import directly into Riverside.fm or Adobe Audition.

## ⚙️ Configuration

### Voice Settings (ElevenLabs)

Edit `app/voice_synthesis.py`:

```python
VOICE_SETTINGS = {
    "stability": 0.70,        # Natural variation
    "clarity": 0.80,          # Clear but not robotic  
    "style_exaggeration": 0.35  # Subtle personality
}
```

### Conversation Behavior

Edit `app/ai_engine.py` to customize:
- Follow-up generation logic
- Fallback phrases
- Clarification triggers
- Transition styles

## 📡 API Reference

### Upload Script
```http
POST /api/upload-script
Content-Type: multipart/form-data

file: CSV/Excel file
```

### Start Episode
```http
POST /api/episodes/start
Content-Type: application/json

{
  "script_id": "uuid",
  "episode_name": "Episode 1"
}
```

### WebSocket Connection
```javascript
const ws = new WebSocket('ws://localhost:8000/ws/episode/{episode_id}');

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  // Handle AI response, audio URL, etc.
};
```

## 🔍 Troubleshooting

### Latency > 1.5s

- Check OpenAI API rate limits
- Verify ElevenLabs streaming is enabled
- Reduce GPT-4 max_tokens if needed

### Audio Quality Issues

- Verify FFmpeg installation: `ffmpeg -version`
- Check LUFS normalization logs
- Ensure 44.1kHz sample rate

### Voice Sounds Robotic

- Lower `stability` setting (0.60-0.70)
- Increase `style_exaggeration` (0.4-0.5)
- Try different ElevenLabs voice models

## 🛣️ Roadmap

- [ ] Multi-language support
- [ ] Voice cloning for custom co-hosts
- [ ] Automatic transcript generation
- [ ] Spotify/Apple Podcasts direct upload
- [ ] Advanced emotion detection

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open Pull Request

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details.

## 📧 Support

- **Issues**: [GitHub Issues](https://github.com/thehillfire/ai-podcast-cohost/issues)
- **Discussions**: [GitHub Discussions](https://github.com/thehillfire/ai-podcast-cohost/discussions)

## 🎓 Credits

- **GPT-4**: OpenAI
- **Voice Synthesis**: ElevenLabs
- **Audio Processing**: FFmpeg
- **Web Framework**: FastAPI

---

**Built with ❤️ for podcasters who want AI co-hosts that feel genuinely human.**

GitHub: [thehillfire/ai-podcast-cohost](https://github.com/thehillfire/ai-podcast-cohost)
