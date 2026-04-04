# Orbital Intelligence Dashboard 🚀🛰️

**Video Explanation:** [Watch on YouTube](https://www.youtube.com/watch?v=aZkzsfCLcwg)

# **[★ VISIT THE LIVE GITHUB PAGE ★](https://itsmilindsahu.github.io/Axiom-Labs_-IIT-DELHI-/)**

Hey guys, this is the final repo for the Orbital Intelligence dashboard we built for the hackathon. It's basically a mission-control-grade interface for satellite tracking and collision avoidance using AI. The UI went through a bunch of iterations, but the final version we landed on is this premium white/blue theme that honestly looks like something SpaceX or NASA would use. 

I've documented the setup and architecture below. Huge shoutout to the team for grinding on the Three.js optimizations! We literally stayed up until 4 AM fixing the CSS animations, but it was worth it.

## What It Actually Does

Instead of just showing blinking dots on a map, this system actively monitors satellite trajectories and predicts conjunctions (space crashes). It has two main modes:

1. **Immersive 3D Mode**: A full 3D viewport of Earth with the satellite fleet, plus a live AI Reasoning Panel on the left that literally walks through its math step-by-step (SCAN → PREDICT → EVALUATE → PLAN → EXECUTE) in real-time.
2. **2D Analytics Hub**: A mission-critical intelligence center featuring 7 dedicated analytics modules: Fleet Overview, Ground Track, Conjunction Analysis, Maneuver & Fuel, System Performance, Pre-Path CDMs, and AI Reasoning logic.

## Tech Stack

- **Frontend**: React + Vite (running on port 5173). Custom CSS (no Tailwind here, wanted absolute control over the animations and it paid off—the CSS file is massive but highly optimized).
- **3D Visualization**: Three.js & React-Three-Fiber.
- **Backend**: Python FastAPI (running on port 8000). Handles the orbital mechanics math, real-time threat generation, and simulation state. 

## How to Run This Thing

I wrote two startup scripts so you don't have to manually start everything.

**If you're on Windows:**
Just double-click `start.bat` or run it in your terminal. It handles the Python virtual environment, PIP installs, and firing up the Vite server in separate command windows. Super easy.

**If you're on Mac/Linux (or using Git Bash):**
Run `bash start.sh` or `./start.sh`.

If you prefer doing it manually because you don't trust my scripts:

1. **Backend**:
```bash
cd backend
python -m venv .venv
source .venv/bin/activate  # OR .venv\Scripts\activate on Windows
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

2. **Frontend**:
```bash
npm install
npm run dev
```

Then literally just open `http://localhost:5173` in your browser. 

## Architecture Notes & Quirks

- **AI Logic Panel**: The math shown in the AI panel isn't just for show. It actually pulls from the backend `snapshot` endpoint. The Tsiolkovsky equation, TCA (Time of Closest Approach), and Delta-v calculations are actively running based on the simulated telemetry.
- **State Management**: We kept it relatively simple using React state and polling the backend every ~2 seconds. No Websockets needed yet since 2-sec polling is fast enough for orbital mechanics (things move fast but they are very far away, so it doesn't look laggy).
- **CSS Animations**: All the glowing dots, pulsing risk indicators, and smooth metric bar growths are 100% CSS. I avoided JS-heavy animation libraries to keep the bundle size down. Trust me, it runs butter smooth even when rendering the 3D earth.
- **Responsive**: It breaks down decently well to smaller screens, but honestly, it's a mission control dashboard... you're supposed to view this on a massive 4K monitor to get the full effect. 

Hit me up if the backend throws CORS errors, sometimes the Uvicorn host/port combination acts weird depending on your environment. Oh, and make sure you have Python 3.9+ installed!

Peace! ✌️
