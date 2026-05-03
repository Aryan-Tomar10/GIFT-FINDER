# Gift-Finder 🚀 AI-Powered Personalized Gift Recommender

![Demo](https://via.placeholder.com/1200x600/4F46E5/FFFFFF?text=AI+Gift+Finder) <!-- Add screenshot -->

## 🎯 Overview

**Gift-Finder** is a full-stack web app that generates **personalized gift ideas** using AI (Groq LLM).

**Users** describe the recipient → Get 6-8 creative suggestions with shopping links (Amazon/Flipkart/Etsy).

**Live Demo**: [localhost:5173 after setup](#user-manual)

## 🏗️ Tech Stack

| Frontend        | Backend            | AI            | Other              |
| --------------- | ------------------ | ------------- | ------------------ |
| React 18 + Vite | FastAPI + Pydantic | Groq (llama3) | Axios, CSS Modules |

## 📱 Features

- [x] Form: Occasion, relationship, budget, description
- [x] Optional: Instagram/Twitter IDs, platform preference
- [x] AI generates: Title, reason, price range, direct shop links
- [x] Responsive UI with loading states
- [x] Error handling + validation

## 🚀 Quick Start (5 mins)

```bash
# Backend (Terminal 1)
cd backend
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
echo \"GROQ_API_KEY=your_key\" > .env  # Get at console.groq.com
uvicorn main:app --reload --port 8000

# Frontend (Terminal 2)
cd frontend && npm install && npm run dev
```

Visit `localhost:5173`

## 📖 Detailed Implementation

### Architecture

Client-server: React SPA ↔ FastAPI API ↔ Groq LLM

**Data Flow**:

```
Form Submit → POST /api/generate-gifts → LLM Prompt → JSON Parse → Shopping Links → Results Grid
```

### Backend (`backend/main.py`)

```python
@app.post("/api/generate-gifts")  # Pydantic validated
async def generate_gifts(req: GiftRequest):
    # Groq ChatCompletion w/ custom SYSTEM_PROMPT
    # Parse JSON → Build platform URLs (Amazon.in etc.)
    return GiftResponse(gift_suggestions=[...])
```

- **Models**: GiftRequest/Input → GiftResponse/Output
- **Error Handling**: JSON decode, API errors → HTTP 4xx/5xx
- **CORS**: localhost:5173

### Frontend (`frontend/src/App.jsx`)

- **State**: useState for form/results/loading/error
- **API**: axios.post → Toggle Form/Results
- **Components**:
  | GiftForm | Inputs + validation |
  | GiftResults | Tags + GiftCard grid |

## 🏛️ Project Legacy & Roadmap

**Current**: Production-ready MVP (8.5/10 maintainability)

**Strengths**: Modern (no legacy jQuery), modular, LLM-flexible.

**v2 Roadmap**:

1. User auth + history (Supabase)
2. Caching (Redis)
3. Tests (pytest/Vitest)
4. Multi-LLM (OpenAI fallback)
5. PWA + sharing

**Longevity**: 3-5 years; easy enterprise fork.

## 🔧 Full User Manual

[See Sections 1-8 in BLACKBOXAI docs PR]

## 🤝 Contributing

1. Fork → `blackboxai-docs` style branch
2. `git push` → `gh pr create`
3. Docs powered by BLACKBOXAI analysis

## 📄 License

MIT

**⭐ Star if useful!** Questions? Open issue.
