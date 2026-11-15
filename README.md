# JBoard ⌨️✨
### Jarvis Keyboard Typing Assistance — 100% Offline On-Device AI

[![Android 9.0+](https://img.shields.io/badge/Android-9.0%2B-3DDC84.svg?style=flat&logo=android&logoColor=white)](https://android.com)
[![Offline AI](https://img.shields.io/badge/AI-100%25%20Offline%20(Gemma%203%201B)-F9973E.svg?style=flat)](https://ai.google.dev/gemma)
[![Engine: llama.cpp](https://img.shields.io/badge/Engine-llama.cpp%20Embedded-blue.svg?style=flat)](https://github.com/ggerganov/llama.cpp)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg?style=flat)](https://www.gnu.org/licenses/gpl-3.0)
[![Privacy First](https://img.shields.io/badge/Privacy-Zero%20Telemetry%20%7C%20No%20Cloud-red.svg?style=flat)]()

**JBoard** (Jarvis Keyboard) is an intelligent, privacy-first Android keyboard with an on-device Large Language Model directly embedded into the application. It delivers instant grammar correction, proofreading, and tone rephrasing **completely offline**—no internet connection, no cloud servers, no subscriptions, and no API keys required.

Powered by Google's **Gemma 3 (1B)** model running locally on-device through an embedded `llama.cpp` engine, JBoard keeps your keystrokes and data 100% private on your phone.

---

## ⚡ Highlights

- 🔒 **100% Offline & Private**: Zero network traffic. Your text never leaves your device. No cloud APIs, no external Ollama servers required, and zero telemetry.
- ⚡ **RAM-Resident Instant Inference**: Gemma 3 (1B) weights are kept resident in memory with foreground service persistence for lightning-fast rewrite generation with zero reload lag.
- ✨ **One-Tap AI Rewrite**: A clean, single amber-orange (`#F9973E`) sparkles button on your keyboard toolbar. Tap to instantly improve, fix, or rephrase whatever you are typing.
- 🎯 **Strict Proofreading Mode**: Engineered specifically for typing assistance. It corrects spelling, grammar, punctuation, and phrasing. If you type a question (e.g. *"what is meaning of life?"*), it fixes the question into *"What is the meaning of life?"* without answering questions philosophically or echoing prompts.
- 🎨 **Adaptive Tone Chips**: Adjust rewritten text on the fly using built-in tone chips: `Formal`, `Casual`, `Friendly`, `Shorter`, `Longer`, and `Translate`.
- ⌨️ **Rock-Solid Keyboard Foundation**: Forked from HeliBoard. Key borders enabled by default, customizable layouts, glide typing, clipboard history, dark/light themes, and multilingual dictionaries.

---

## 📸 Screenshots & Workflow

```
┌────────────────────────────────────────────────────────┐
│  WhatsApp / Telegram / Messages                        │
│  "what is meaning of life?"                            │
└────────────────────────────────────────────────────────┘
                            │
               [ ✨ Tap AI Rewrite Key ]
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│  JBoard AI Preview Panel                               │
│  "What is the meaning of life?"                        │
│                                                        │
│  [Formal]  [Casual]  [Friendly]  [Shorter]  [Longer]   │
│                                                        │
│  [📋 Copy]  [🔄 Retry]            [✏️ Edit]  [ APPLY ]  │
└────────────────────────────────────────────────────────┘
```

---

## 🧠 Under the Hood

| Component | Technology |
|---|---|
| **Base Keyboard** | HeliBoard (Clean open-source AOSP IME foundation) |
| **On-Device LLM** | Google **Gemma 3 (1B Instruct)** (`gemma-3-1b-it.gguf`) |
| **Inference Engine** | `llama.cpp` Android JNI runtime (`dev.ffmpegkit-maintained:llama-android`) |
| **Memory Architecture** | Preloaded resident model in RAM with Android Foreground Service notification |
| **Inference Mode** | 4-thread CPU NEON-accelerated quantized matrix multiplication |
| **Prompt Template** | Native Gemma 3 Jinja chat template formatting (`<start_of_turn>user / model`) |

---

## 🚀 Getting Started

### Prerequisites
- Android 9.0 (Pie / API 28) or higher
- Device Architecture: `arm64-v8a` (most modern Android phones)
- Minimum Free RAM: ~1.5 GB free memory for model residency

### Installation

1. Download the latest **`JBoard_1.3.1.apk`** from the [Releases](https://github.com/your-username/jboard/releases) page.
2. Install the APK on your device:
   ```bash
   adb install -r -t JBoard_1.3.1.apk
   ```
   *(Note: Enable "Install from unknown sources" if installing directly on the phone).*
3. Open **Settings → System → Languages & Input → On-screen Keyboard → Manage Keyboards**.
4. Enable **JBoard** and select it as your default input method.
5. Grant Notification permission so JBoard can keep the Gemma 3 model loaded in RAM for instantaneous responses.

---

## 🛠️ Building from Source

### Prerequisites
- **Android Studio** Hedgehog / Ladybug or newer
- **JDK 17** or **JDK 21** (e.g., JetBrains Runtime 21)
- **Android SDK & NDK** (`ndkVersion = "28.0.13004108"` or standard NDK r27+)
- **Model Weights**: `gemma-3-1b-it-UD-IQ1_S.gguf` placed in `app/src/main/assets/models/gemma3-1b-it.gguf`

### Build Steps

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/jboard.git
   cd jboard
   ```

2. **Place the Gemma 3 GGUF model**:
   Place your quantized `gemma-3-1b-it` GGUF file inside:
   ```
   app/src/main/assets/models/gemma3-1b-it.gguf
   ```

3. **Compile the Debug APK**:
   ```bash
   # Windows PowerShell / CMD
   .\gradlew.bat assembleDebug --no-configuration-cache

   # macOS / Linux
   ./gradlew assembleDebug --no-configuration-cache
   ```

4. **The compiled APK will be output at**:
   ```
   app/build/outputs/apk/debug/JBoard_1.3.1.apk
   ```

5. **Deploy to connected device**:
   ```bash
   adb install -r -t app/build/outputs/apk/debug/JBoard_1.3.1.apk
   ```

---

## 🛡️ Privacy & Security

JBoard is built with zero tolerance for data leaks:
- ❌ **No Internet Permission for AI**: The AI inference pipeline runs natively inside the keyboard process via local JNI code.
- ❌ **No Cloud Telemetry**: Zero tracking SDKs, no Google Analytics, no Firebase Crashlytics.
- ❌ **Password Fields Protected**: AI assistance and clipboard history are strictly disabled in secure password/PIN fields.
- 🔐 **Air-Gapped Operation**: Turn on Airplane mode—JBoard functions with 100% feature parity.

---

## 🤝 Acknowledgments & Credits

- [HeliBoard](https://github.com/Helium314/HeliBoard) — Outstanding open-source Android keyboard foundation.
- [llama.cpp](https://github.com/ggerganov/llama.cpp) by Georgi Gerganov — The state-of-the-art LLM inference engine.
- [llama-android](https://github.com/arthenica/ffmpeg-kit) — Android JNI bindings for llama.cpp.
- [Google Gemma](https://ai.google.dev/gemma) — Google's lightweight open weights language model family.

---

## 📄 License

This project is licensed under the **GNU General Public License v3.0 (GPLv3)**. See the [LICENSE](LICENSE) file for details.
