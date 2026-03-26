# Deepfake Guard

> **AI-Powered Deepfake Detection for Video & Audio + Audio Watermarking**

Advanced deepfake detection system using ResNeXt + LSTM neural networks. Full-stack application with SQLite authentication, built with React, TypeScript, Express, and Tailwind CSS.

---

## 🚀 Features

### Core Capabilities
- **Video Deepfake Detection** - Analyze video files for face manipulation and synthetic content
- **Audio Deepfake Detection** - Detect voice cloning and synthetic audio generation
- **Audio Watermarking (NEW)** - Embed and extract hidden watermark data in audio files using LSB-based lossless technique (WAV PCM only)
- **Frame Extraction** - Automatic sampling and thumbnail generation from video
- **Waveform & Spectrogram** - Real-time audio visualization with WaveSurfer.js
- **Analysis Settings** - Configurable frame rates and chunk sizes
- **User Authentication** - SQLite-based registration, login, and session management

---

## 🔐 Audio Watermarking Module

The system includes a robust **Audio Watermarking feature** that allows embedding and extraction of hidden data within audio files.

### 🎯 Key Functionalities
- **Watermark Embedding** - Hide text data inside audio signals
- **Watermark Extraction** - Retrieve hidden watermark from audio
- **Lossless Processing** - Ensures no perceptible audio quality degradation
- **CRC Validation** - Detects corruption using error-checking mechanism

### ⚙️ Working Principle
- Uses **LSB (Least Significant Bit)** technique on **PCM 16-bit WAV audio**
- Each audio sample stores 1 bit of watermark data
- Watermark format: [32-bit length][watermark data bits]
- Embedding: sample = (sample & ~1) | bit
- Extraction: bit = sample & 1


### 📌 Format Restriction
- Only **.wav (PCM 16-bit)** is supported  
- MP3/M4A are not supported due to lossy compression which corrupts watermark data

### 🛡️ Reliability Features
- Bit-level consistency between embedding and extraction
- Prevents overflow using capacity checks
- CRC-based validation ensures integrity of extracted watermark

---

## 🎨 Design System

### Color Palette
- **Primary**: Indigo (HSL: 239, 84%, 67%)
- **Secondary**: Cyan (HSL: 189, 94%, 43%)
- **Base**: Slate/Ink tones for backgrounds

---

## 📁 Project Structure
src/
├── components/
├── context/
├── layouts/
├── pages/
│ ├── AudioWatermark.tsx # NEW feature page
├── lib/
├── router.tsx
├── App.tsx
└── main.tsx
server/
├── watermark/
│ ├── embed.ts
│ ├── extract.ts
│ ├── routes.ts
├── index.ts
├── auth.ts
├── db.ts


---

## 🛠️ Tech Stack

### Frontend
- React 18
- TypeScript
- Vite
- Tailwind CSS
- react-router-dom
- react-dropzone
- wavesurfer.js
- lucide-react

### Backend
- Node.js + Express
- TypeScript
- SQLite (better-sqlite3)
- JWT Authentication
- bcryptjs
- zod validation

---

## 🚦 Getting Started

### Prerequisites
- Node.js 18+

### Installation

```bash
git clone <YOUR_GIT_URL>
cd deepfake-guard

npm install

cd server
npm install
cd ..

echo "JWT_SECRET=your_secret_key_here_min_32_chars" > .env
echo "NODE_ENV=development" >> .env
```

Run Application:
npm run dev:all
Frontend: http://localhost:8080
Backend: http://localhost:3001

🧭 Routes
Route	Description:
/	Home
/video	Video detection
/audio	Audio detection
/audio-watermark	Audio watermarking
/accounts	Authentication


🔐 API Endpoints
-Authentication:
Method	Endpoint
POST	/api/auth/register
POST	/api/auth/login
GET	/api/auth/me

-Watermarking
Method	Endpoint	Description
POST	/api/watermark/embed	Embed watermark into WAV audio
POST	/api/watermark/extract	Extract watermark from audio


📝 Usage Guide
- Audio Watermarking
1. Navigate to /audio-watermark
2. Upload a WAV file
3. Enter watermark text
4. Click "Embed Watermark"
5. Download processed audio
6. Upload watermarked audio
7. Click "Extract Watermark"

🔒 Important Notes
- Authentication
  -JWT stored in HTTP-only cookies
  -Password hashed using bcrypt

-Audio Watermarking Notes
  -Only WAV (PCM 16-bit) supported
  -MP3 not supported (lossy compression breaks watermark)
  -Watermark size limited by audio length
  -CRC validation ensures data integrity

🎯 Next Steps
- Integrate real deepfake detection models
- Add database for watermark tracking
- Improve watermark robustness (FFT/DCT-based methods)

📄 License
Educational use only