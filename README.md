# Cognitive Labyrinth (Single-File Web App)

A **single-file** (HTML + CSS + JS) reflective maze experience that combines **procedural maze navigation** with **journaling prompts** and an optional **LLM “coach”**. It supports **seeded, shareable mazes**, **fog-of-war**, **hints + solver overlays**, **autosave**, **export/import**, and an **offline Local Coach** mode. For OpenAI integration it uses the modern **Responses API** (proxy recommended). 

---

## Features

### Maze + Navigation
- **Procedural maze generation** (DFS carving) with guaranteed **solvable end**
- **Desktop + mobile** support:
  - Buttons (↑ ← ↓ →)
  - **Arrow key** movement
  - **Swipe** movement on touch screens
- **Seeded randomness**: same seed ⇒ same maze (shareable via URL parameters)
- **Difficulty / topology control**:
  - Maze size (10×10 up to 32×32)
  - Node count
  - “Loopiness” (% extra connections carved into the maze)

### Gameplay Tools
- **Fog-of-war** toggle + adjustable **vision radius**
- **Hint**: highlights the next step toward the end
- **Solution overlay**: shows shortest path from current position

### Reflection + Coaching
- **Reflection nodes** trigger prompts
- **Journal**:
  - Stores prompt + user reflection + coach response
  - Scrollable history with timestamps and positions
- Coaching modes:
  - **Local Coach (offline)**: heuristic feedback, no network required
  - **OpenAI Coach** via:
    - **Proxy mode (recommended)** — secure and avoids CORS
    - **Direct mode (unsafe + often CORS-blocked)**

### Persistence + Portability
- **Autosave** to `localStorage` (toggleable)
- **Export session** to JSON (maze + run + journal)
- **Import session** from JSON
- **Undo** (step back)

### UX / Polish
- Modern glassy UI (dark/light themes)
- WebAudio feedback + haptics (optional)
- Stats: steps, time, nodes completed, hints used

---

## Quick Start (Run Locally)

1. Save the entire file as `cognitive-labyrinth.html`
2. Open it in a browser (Chrome/Edge/Firefox)

That’s it — **Local Coach** works immediately offline.

> Tip: If audio doesn’t play, click/tap once to allow AudioContext activation (browser policy).

---

## URL Parameters (Shareable Mazes)

The app updates the address bar with a share link like:

- `?seed=your-seed&size=20&nodes=5&loops=10&theme=dark`

Parameters:
- `seed` — deterministic maze seed (string)
- `size` — maze dimension (10..32)
- `nodes` — reflection node count
- `loops` — loopiness percent (0..60)
- `theme` — `dark` or `light`

---

## OpenAI Integration (Recommended Setup)

### Why a Proxy?
Putting an OpenAI API key in a browser app is unsafe (easy to steal), and direct browser calls often fail due to CORS. Use a small server/worker as a relay. 

### Option A — Cloudflare Worker Proxy
- Deploy the Worker code included in the app (Settings → Proxy section)
- Set secret `OPENAI_API_KEY`
- Put the worker URL into **Proxy URL** in the app
- Select **Coach mode → OpenAI via Proxy**

### Option B — Node/Express Proxy
- Run the Node proxy included in the app
- Set environment variable `OPENAI_API_KEY`
- Point the app Proxy URL to `http://localhost:8787/openai`

### Models / Endpoint
This project uses the OpenAI **Responses API** (`POST /v1/responses`), which is the modern endpoint for text responses. 

---

## Data Storage

- Autosave uses `localStorage` under a single key (e.g. `cognitive_labyrinth_v2026`)
- Export JSON includes:
  - maze grid
  - player state, steps, visited cells
  - nodes completed
  - journal entries

**Security note:** This implementation intentionally does **not** persist API keys in autosave.

---

## Controls

### Movement
- Buttons: ↑ ← ↓ →
- Keyboard: Arrow keys
- Touch: Swipe on maze

### Shortcuts
- `H` — Hint
- `U` — Undo
- `Ctrl+Enter` / `Cmd+Enter` — Submit reflection

---

## Project Structure

Single file only:

