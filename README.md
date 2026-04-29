# ScalerChat — Persona-Based AI Chatbot

Have real conversations with **Anshuman Singh**, **Abhimanyu Saxena**, and **Kshitij Mishra** from Scaler Academy — powered by Groq (Llama 3.3 70B) and carefully researched system prompts.

**Live App:** _[Add your Render frontend URL here after deployment]_  
**Backend API:** https://scalerchat.onrender.com

---

## Features

- **3 distinct AI personas** — each with a unique voice, background, and communication style
- **Persona switcher** — switching tabs resets the conversation and loads the persona's system prompt
- **4 suggestion chips per persona** — tailored quick-start questions for each person
- **Typing indicator** — animated dots while the API call is in progress
- **Multi-turn conversation** — chat history is passed with each request for context
- **Error handling** — graceful fallback messages if the API is unavailable
- **Claude-style UI** — clean dark theme with sidebar layout, per-persona accent colors
- **Mobile responsive** — off-canvas sidebar drawer with hamburger toggle

---

## Tech Stack

| Layer    | Tech                              |
|----------|-----------------------------------|
| Frontend | React 19, custom CSS              |
| Backend  | Node.js, Express 5                |
| LLM API  | Groq — Llama 3.3 70B Versatile    |
| Deploy   | Render (Web Service + Static Site)|

---

## Local Setup

### Prerequisites
- Node.js 18+
- A Groq API key (get one free at [console.groq.com](https://console.groq.com))

### 1. Clone and install

```bash
git clone https://github.com/RajPrakash681/scalerchat.git
cd scalerchat
```

### 2. Set up the backend

```bash
cd backend
cp .env.example .env
# Edit .env and add your GROQ_API_KEY
npm install
npm start
```

The backend runs on `http://localhost:5000`.

### 3. Set up the frontend

```bash
cd frontend
cp .env.example .env
# .env already points to http://localhost:5000 — no changes needed for local dev
npm install
npm start
```

The app opens at `http://localhost:3000`.

---

## Deployment

Both services are deployed on **Render**.

### Backend → Render Web Service

1. Go to [render.com](https://render.com) → New → **Web Service**
2. Connect repo: `RajPrakash681/scalerchat`
3. Set **Root Directory** to `backend`
4. Build command: `npm install`
5. Start command: `npm start`
6. Under **Environment Variables**, add:
   - `GROQ_API_KEY` → your Groq API key
7. Deploy — Render gives you a public URL (e.g. `https://scalerchat.onrender.com`)

### Frontend → Render Static Site

1. Go to Render → New → **Static Site**
2. Connect the same repo
3. Set **Root Directory** to `frontend`
4. Build command: `npm install && npm run build`
5. Publish directory: `build`
6. Under **Environment Variables**, add:
   - `REACT_APP_API_URL` → your backend Render URL
7. Deploy

---

## Project Structure

```
scalerchat/
├── backend/
│   ├── server.js          # Express API + system prompts + Groq integration
│   ├── .env.example       # Environment variable template
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── App.js         # Main React component (full UI + chat logic)
│   │   └── index.css      # Global styles + animations
│   ├── public/
│   │   └── index.html     # HTML template with Google Fonts
│   └── package.json
├── prompts.md             # All system prompts with design annotations
├── reflection.md          # 400-word assignment reflection
└── README.md
```

---

## Prompt Engineering Techniques Used

Each system prompt applies:

1. **Persona description** — verified background, values, and communication style
2. **Few-shot examples** — 3 Q&A pairs embedded directly in each system prompt
3. **Chain-of-Thought instruction** — persona-specific internal reasoning framing
4. **Output format** — 4-5 sentences, flowing prose, ends with a question
5. **Constraints** — explicit prohibitions that prevent generic AI behavior

See [prompts.md](./prompts.md) for the full prompts with inline design annotations.

---

## Environment Variables

**Backend** (`backend/.env`):
```
GROQ_API_KEY=your_groq_api_key_here
PORT=5000
```

**Frontend** (`frontend/.env`):
```
REACT_APP_API_URL=http://localhost:5000
```

No API keys are committed to this repository. The `.gitignore` excludes all `.env` files.
