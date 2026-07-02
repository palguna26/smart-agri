# SmartAgri AI

SmartAgri AI is a full-stack agriculture decision-support application with a FastAPI backend and a React/Vite frontend. It combines crop, yield, fertilizer, stress, plant disease, fruit disease, weather/location, authentication, and AI-assisted advisory features in one project.

## Project Structure

```text
smart-agri/
├── backend/              # FastAPI services, ML inference, auth, data helpers
├── frontend/             # React + Vite web application
├── docker-compose.yml    # Local multi-service startup
├── .env.example          # Root environment variable template
└── START_BACKEND.ps1     # Windows helper script for backend startup
```

## Features

- Crop recommendation and crop prediction APIs
- Yield prediction service
- Fertilizer recommendation and nutrient guidance
- Plant and fruit disease detection services
- Crop stress prediction
- Weather and location helpers
- Authentication with MongoDB-backed user data
- Groq-powered chatbot/remedy generation integration
- React dashboard with routing, map support, and API integration

## Prerequisites

- Python 3.10+
- Node.js 18+
- npm
- MongoDB connection string for persistent auth/data features
- Optional Groq API key for AI chatbot/remedy features

## Environment Configuration

Copy the example environment files before running locally:

```bash
cp .env.example .env
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env
```

Common backend variables include:

```env
MONGODB_URL=mongodb+srv://user:password@cluster.example.mongodb.net/smartagri
GROQ_API_KEY=your_groq_api_key
LOW_MEMORY_MODE=true
ENVIRONMENT=development
PORT=8000
```

Common frontend variables include:

```env
VITE_API_URL=http://localhost:8000
```

## Backend Setup

```bash
cd backend
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\\Scripts\\activate
pip install -r requirements.txt
uvicorn main_fastapi:app --host 0.0.0.0 --port 8000 --reload
```

Health checks:

```bash
curl http://localhost:8000/health
curl http://localhost:8000/health/models
```

## Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

The frontend is served by Vite, typically at `http://localhost:5173`.

## Docker Startup

```bash
docker compose up --build
```

Use Docker when you want the frontend and backend to run together with a consistent local environment.

## Development Commands

Backend:

```bash
cd backend
python -m py_compile main_fastapi.py
uvicorn main_fastapi:app --reload
```

Frontend:

```bash
cd frontend
npm run lint
npm run build
```

## Deployment Notes

- The backend is optimized for constrained production environments and lazy-loads heavier ML services where possible.
- Configure production CORS origins in `backend/main_fastapi.py` before deploying to new domains.
- Set secrets such as `MONGODB_URL`, OAuth credentials, and `GROQ_API_KEY` in the hosting provider dashboard instead of committing them.
- Build the frontend with `npm run build` and serve the generated `dist/` directory from your frontend hosting provider.

## Maintenance

This repository intentionally keeps documentation consolidated in this README to reduce stale duplicate guides. Update this file whenever setup, deployment, or major feature behavior changes.
