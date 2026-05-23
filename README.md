# AbiturAI 🎓

**AI-powered DTM exam preparation platform for Uzbek students.**

> Every year, 1 million+ students in Uzbekistan take the DTM exam. Only 18% get admitted. Quality tutors cost $50–120/month — unaffordable for most families, especially outside Tashkent. AbiturAI brings personalized AI tutoring to every abituriyent, in Uzbek, in DTM format.

🔗 **Backend repo:** https://github.com/kruzimatov/abitur_ai_backend

---

## What It Does

AbiturAI integrates four distinct AI systems, each solving a specific educational problem:

| Feature | Who uses it | What it does |
|---|---|---|
| 🔍 **AI Error Diagnosis** | Students | After a quiz, explains *why* each wrong answer was chosen — like a real tutor |
| 📚 **RAG Tutor** | Students | Answers questions grounded in actual DTM curriculum, not generic internet data |
| 🗣️ **Explain It Back** | Students | Student explains a topic to AI; AI evaluates understanding gaps (Feynman technique) |
| ✍️ **AI Question Generator** | Teachers | Paste topic text, get 5 DTM-format questions with answer keys instantly |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Laravel 12 (PHP) — REST API |
| Frontend | React (Vite) + Tailwind CSS |
| Database | MySQL (18 tables) |
| AI Model | Google Gemini 2.0 Flash |
| Vector Store | ChromaDB |
| RAG Service | Python FastAPI sidecar |
| Auth | JWT |

---

## Roles

| Role | Access |
|---|---|
| **Student** | Take quizzes, chat with AI tutor, track progress & streaks |
| **Teacher** | Create topics & questions, AI question generator, student analytics |
| **Admin** | Full access + delete operations |

---

## Project Structure

```
abiturai/
├── backend/        # Laravel 12 REST API (46 endpoints)
├── frontend/       # React + Vite (login, navbar, dashboard)
├── rag_service/    # Python FastAPI + ChromaDB
└── README.md
```

---

## Getting Started

### Prerequisites

- PHP 8.2+, Composer
- Node.js 18+, npm
- Python 3.10+
- MySQL
- Google Gemini API key

---

### 1. Backend (Laravel)

```bash
cd backend
composer install
cp .env.example .env   # configure DB + Gemini API key
php artisan migrate:fresh --seed
php artisan serve --port=8080
```

Edit `.env`:

```env
DB_DATABASE=abiturai
DB_USERNAME=your_db_user
DB_PASSWORD=your_db_password

GEMINI_API_KEY=your_gemini_api_key
RAG_SERVICE_URL=http://localhost:8001
```

Backend runs at `http://localhost:8080`  
API docs: `http://localhost:8080/api/documentation`

---

### 2. RAG Service (Python)

```bash
cd rag_service
pip install -r requirements.txt
python seed.py
uvicorn main:app --port=8001
```

RAG service runs at `http://localhost:8001`

---

### 3. Frontend (React)

```bash
cd frontend
npm install
cp .env.example .env
```

Edit `.env`:

```env
VITE_API_URL=http://localhost:8080/api
```

```bash
npm run dev
```

Frontend runs at `http://localhost:5173`

---

## Environment Variables

| Variable | Required | Description |
|---|---|---|
| `GEMINI_API_KEY` | ✅ | Google Gemini API key |
| `RAG_SERVICE_URL` | ✅ | Python sidecar URL (default: `http://localhost:8001`) |
| `DB_DATABASE` | ✅ | MySQL database name |
| `DB_USERNAME` | ✅ | MySQL username |
| `DB_PASSWORD` | ✅ | MySQL password |

---

## Seeded Content

| Subject | Topics | Questions |
|---|---|---|
| Matematika | 3 (Logarifm, Trigonometriya, Hosilalar) | 30 |
| Fizika | 2 | 10 |
| Kimyo | 2 | 10 |

---

## AI Disclosure

| Tool | Usage |
|---|---|
| **Google Gemini 2.0 Flash** | Error diagnosis, RAG tutor, Feynman evaluation, question generation |
| **ChromaDB** | Vector store for DTM curriculum content |
| **pypdf / python-docx** | Textbook parsing for RAG pipeline |
| **google-genai** | Gemini API title refinement for document splitting |

All prompts are written in Uzbek, optimized for DTM exam format and curriculum.

---

## Demo Notes

- Student login: `student@abiturai.uz` / `password`
- Teacher login: `teacher@abiturai.uz` / `password`
- All AI responses are in Uzbek

---

## Team

| Name | Role |
|---|---|
| Xayrullo | Laravel Backend — core API, auth, CRUD, dashboard, chat, teacher features |
| Lilly | Python RAG — AI service, ChromaDB, document processing, Docker |

**Track:** General Education  
**Event:** Build with AI EdTech Hackathon, May 23–24, 2026, New Uzbekistan University
