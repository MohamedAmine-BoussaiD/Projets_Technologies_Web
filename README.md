# EDU-MIND-PLUS

A smart learning platform where students upload their course materials and interact with an AI tutor. Think of it like NotebookLM but focused on education - upload PDFs, ask questions, generate quizzes, and track your progress.

## What it does

- Upload your course documents (PDF, DOCX, TXT, MD)
- Chat with an AI that answers based on YOUR materials
- Generate practice quizzes (QCM) adapted to your level
- Get instant feedback and explanations on your answers
- Track your learning progress over time

## Stack

**Frontend:** Next.js 16, React 19, TypeScript, Tailwind CSS

**Backend:** FastAPI, MongoDB (Beanie ODM), JWT auth

**AI:** Groq (Llama 3.3), LangChain, LangGraph, ChromaDB

## Setup

### Backend

```bash
cd backend
cp .env.example .env   # add your MongoDB + GROQ_API_KEY
uv sync                # or pip install -e .
uv run uvicorn app.main:app --reload
```

### Frontend

```bash
cd frontend
npm install
echo "NEXT_PUBLIC_API_URL=http://localhost:8000" > .env.local
npm run dev
```

## Project structure

```
├── frontend/          # Next.js app
│   └── src/
│       ├── app/       # pages (login, sessions, profile)
│       ├── components/
│       └── lib/       # api client, auth context
│
├── backend/           # FastAPI
│   └── app/
│       ├── api/       # endpoints
│       ├── models/    # MongoDB models
│       └── services/  # AI logic
│
└── agents/            # LangGraph agents
    ├── qcm_agents.py  # quiz generation & grading
    ├── orchestrator.py
    └── rag.py         # document retrieval
```

## How it works

1. User creates a session and uploads documents
2. Documents get chunked and stored in ChromaDB (vector DB)
3. When chatting, relevant chunks are retrieved (RAG)
4. AI responds using only the uploaded materials
5. Quizzes are generated from the same materials
6. Answers are graded with detailed feedback

## Environment variables

Backend `.env`:
```
DB_HOST=your-mongodb-host
DB_USER=user
DB_PASSWORD=password
DB_NAME=edu_mind
JWT_SECRET_KEY=your-secret
GROQ_API_KEY=gsk_xxx
```

Frontend `.env.local`:
```
NEXT_PUBLIC_API_URL=http://localhost:8000
```
