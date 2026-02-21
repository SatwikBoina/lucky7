# 🃏 Lucky 7 — Multiplayer Card Game

A full-stack multiplayer card game built with Python (Flask) backend and a beautiful vanilla HTML/CSS/JS frontend, deployable via GitHub Actions.

---

## 🎮 How to Play

**Lucky 7** is played with a standard 52-card deck (no jokers), ideally with 4–6 players.

1. Cards are dealt equally among all players
2. The player holding **Diamond 7** goes first — it's automatically placed on the board
3. On your turn, you can play a card if:
   - It's a **7 of any suit** (opens that suit's row on the board)
   - It **extends** an existing suit row by ±1 (e.g., if diamonds has 6–7, you can play 5♦ or 8♦)
4. If you have **no valid moves**, you must **pass**
5. First player to **discard all their cards** wins! 🏆

---

## 🚀 Quick Start (Local)

### 1. Clone & Run Backend
```bash
git clone https://github.com/YOUR_USERNAME/lucky7.git
cd lucky7

# Install dependencies
pip install -r backend/requirements.txt

# Run the backend
cd backend && python app.py
```
Backend runs at `http://localhost:5000`

### 2. Open Frontend
Open `frontend/index.html` in your browser directly, **or** serve it:
```bash
cd frontend && python -m http.server 8080
# Visit http://localhost:8080
```

---

## 🌐 Deploy to the Web (Play with Friends!)

### Step 1: Deploy the Backend

**Option A — Render (Recommended, Free)**
1. Go to [render.com](https://render.com) → New → Web Service
2. Connect your GitHub repo
3. It auto-detects `render.yaml` and deploys!
4. Copy your service URL: `https://lucky7-backend.onrender.com`

**Option B — Railway**
1. Go to [railway.app](https://railway.app) → New Project → GitHub repo
2. Set start command: `cd backend && gunicorn app:app --bind 0.0.0.0:$PORT`
3. Copy the Railway URL

**Option C — Fly.io**
```bash
brew install flyctl
flyctl auth login
flyctl launch  # in the project root
flyctl deploy
```

---

### Step 2: Deploy Frontend to GitHub Pages

1. Go to your repo **Settings → Pages**
   - Source: **GitHub Actions**

2. Add a secret: **Settings → Secrets and variables → Actions**
   - Name: `BACKEND_URL`
   - Value: `https://your-backend-url.onrender.com` (from Step 1)

3. Push to `main` — the workflow runs automatically!

4. Your game is live at:
   `https://YOUR_USERNAME.github.io/lucky7/`

---

## 📁 Project Structure

```
lucky7/
├── backend/
│   ├── app.py              # Flask game server
│   └── requirements.txt    # Python dependencies
├── frontend/
│   └── index.html          # Full game UI (single file)
├── .github/
│   └── workflows/
│       ├── deploy-frontend.yml   # Auto-deploy to GitHub Pages
│       └── backend-ci.yml        # Test + deploy backend
├── Procfile                # For Heroku/Render/Railway
├── render.yaml             # Render one-click config
├── fly.toml                # Fly.io config
└── README.md
```

---

## 🔧 GitHub Actions Workflows

| Workflow | Trigger | What it does |
|----------|---------|--------------|
| `deploy-frontend.yml` | Push to `main` (frontend changes) | Injects backend URL, deploys to GitHub Pages |
| `backend-ci.yml` | Push to `main` (backend changes) | Runs game logic tests, optionally deploys backend |

---

## 🎨 Features

- ✅ Real-time multiplayer (2–6 players)
- ✅ Share-a-code lobby system
- ✅ Beautiful casino-felt themed UI
- ✅ Sorted hand with valid move highlighting
- ✅ Animated card board
- ✅ Auto-polling for live game state
- ✅ Pass turn validation
- ✅ Winner detection & celebration screen

---

## 🛠️ API Reference

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/create_game` | POST | Create a new game room |
| `/api/join_game` | POST | Join with a game code |
| `/api/start_game` | POST | Host starts the game |
| `/api/play_card` | POST | Play a card from hand |
| `/api/pass_turn` | POST | Pass when no valid moves |
| `/api/game_state` | GET | Poll current game state |

---

## 💡 Tips

- **Backend sleep**: Free Render instances spin down after inactivity. The first load may take 30s.
- **Multiple rooms**: The backend supports multiple simultaneous games!
- **Production**: For serious use, replace the in-memory `games` dict with Redis.

---

Made with ♦ ♥ ♣ ♠ — Have fun!
