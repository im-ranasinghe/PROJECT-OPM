# 💻 Office Posture Monitor

A real-time computer vision application that helps users maintain healthy sitting posture using webcam-based pose estimation. The app detects poor posture, provides instant visual feedback, and alerts you with a screen warning and audio alarm before discomfort develops.

This project ships **two independent implementations** of the same idea, built with different tech stacks:

| | Web App | Python App |
|---|---|---|
| Folder | `src/` | `opmotitor/` |
| Stack | React + TypeScript + Vite | Python + Streamlit + OpenCV |
| Pose engine | MediaPipe Pose (runs in-browser, client-side) | MediaPipe Pose (runs locally via OpenCV) |
| Run with | `npm run dev` | `streamlit run app.py` |

You can use either one on its own — they don't depend on each other.

## ✨ Features

* 📷 Real-time webcam posture monitoring
* 🦴 Live MediaPipe pose skeleton visualization overlaid on your video feed
* ⚠️ Detects three posture problems:
  * Neck bent forward
  * Slouching / rounded shoulders
  * Sitting too close to the screen
* 🎯 Personal calibration — set your own "good posture" baseline instead of relying on fixed defaults
* 🔔 Audio alarm when poor posture is held for a few seconds
* 🟢 Green indicator for good posture · 🔴 Red warning for incorrect posture
* ⚡ Lightweight, responsive interface — works down to mobile screen sizes (web app)

## 🛠️ Tech Stack

**Web App** (`src/`)
* React 19 + TypeScript
* Vite 6
* Tailwind CSS v4
* MediaPipe Pose & Camera Utils (loaded via CDN, runs entirely client-side)
* Web Audio API for synthesized alarm sounds (no audio files needed)

**Python App** (`opmotitor/`)
* Python 3.9–3.11
* Streamlit (UI)
* OpenCV (webcam capture)
* MediaPipe Pose (server/desktop-side pose detection)
* Pygame (alarm playback)

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/im-ranasinghe/PROJECT-OPM.git
cd PROJECT-OPM
```

### 2. Run the Web App

```bash
cd src
npm install
npm run dev
```

Open the local URL printed in your terminal (typically `http://localhost:3000`). Click **Start Webcam Feed** and allow camera access when prompted.

### 3. Run the Python App

In a separate terminal, from the repo root:

```bash
cd opmotitor
pip install -r requirements.txt
streamlit run app.py
```

Streamlit will open `http://localhost:8501` automatically. Click **Start Monitor** in the sidebar and allow camera access when prompted.

> **Note:** if you hit `AttributeError: module 'mediapipe' has no attribute 'solutions'`, a recent MediaPipe release changed its packaging. Fix it by pinning to a known-working version:
> ```bash
> pip install mediapipe==0.10.9 --force-reinstall
> ```

## 🧠 How It Works

Both apps use MediaPipe Pose to detect body landmarks (nose, ears, shoulders) from the webcam feed, then analyze posture in real time by checking:

* **Proximity** — shoulder width relative to the frame; growing significantly larger than your baseline means you've leaned in too close
* **Neck angle** — the angle between your ear and shoulder relative to vertical; a larger angle means your neck is bent forward
* **Slouch ratio** — the vertical distance from your nose to your shoulder midpoint, normalized by shoulder width; a shrinking ratio means your upper body is rounding forward

If any of these cross a threshold and stay there for a few seconds (default 3s), the app shows a red warning border and plays an audio alert. Once you correct your posture, the warning clears automatically after a short grace period.

You can calibrate the app to your own body and preferred sitting position, or adjust the trigger thresholds manually, instead of relying on the built-in defaults.

## 📌 Future Improvements

* Posture history and analytics dashboard
* Daily/weekly posture reports
* Break reminders (Pomodoro-style)
* Multi-user profiles
* Combine both apps into a single unified stack

## 🙏 Credits & Inspiration

This project was built as a learning exercise, inspired by [Office Posture Monitor](https://github.com/vaishnavib17/Office-Posture-Monitor) by **Vaishnavi Bagmar**. The core posture-detection concept (neck angle, slouch ratio, proximity checks) traces back to that project; this repository is an independent rebuild with a redesigned, mobile-friendly UI and additional configuration options.

## 👨‍💻 Author

**im-ranasinghe**

If you found this project interesting, feel free to star ⭐ the repository or share your feedback.
