# ATS Resume Optimizer

A production-ready ATS Resume Optimizer platform using MERN stack (MongoDB, Express, React, Node.js) with Python ML service.

## Features

- **Resume Upload**: Supports PDF and DOCX formats
- **Job Description Analysis**: Paste job descriptions for analysis
- **ATS Scoring**: Comprehensive ATS score with semantic and keyword matching
- **Keyword Analysis**: Identifies missing and matching keywords
- **User Approval**: Never fabricates experience - all keyword additions require user approval
- **Resume Optimization**: Generate optimized resumes with approved keywords
- **LaTeX Generation**: Multiple ATS-friendly templates (Simple, Professional, Naman)
- **Export Options**: Download as TXT, LaTeX (.tex)

## Architecture

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Frontend  │────▶│   Backend   │────▶│ ML Service  │
│   (React)   │     │  (Express)  │     │  (FastAPI)  │
└─────────────┘     └─────────────┘     └─────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │  MongoDB    │
                    └─────────────┘
```

## Tech Stack

- **Frontend**: React, Vite, Tailwind CSS
- **Backend**: Node.js, Express, MongoDB, Mongoose
- **ML Service**: Python, FastAPI, Sentence Transformers, scikit-learn
- **Resume Parsing**: PyMuPDF, python-docx
- **LaTeX Generation**: Jinja2

## Prerequisites

- Node.js 18+
- Python 3.11+
- MongoDB (local or Atlas)
- npm or yarn

## Quick Start (Docker Compose)

The easiest way to run the application:

```
bash
# Clone the repository
git clone <repository-url>
cd ats-resume-optimizer

# Start all services with Docker Compose
docker-compose up -d
```

This will start:
- Frontend: http://localhost:5173
- Backend: http://localhost:5000
- ML Service: http://localhost:8000
- MongoDB: localhost:27017

## Manual Setup

### 1. ML Service (Python)

```
bash
cd ml-service

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the service
uvicorn main:app --reload
```

### 2. Backend (Node.js)

```
bash
cd backend

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env

# Update .env with your MongoDB URI
# MONGODB_URI=mongodb://localhost:27017/ats_resume_db
# ML_SERVICE_URL=http://localhost:8000

# Run the server
npm run dev
```

### 3. Frontend

```
bash
cd frontend

# Install dependencies
npm install

# Run the development server
npm run dev
```

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/upload` | POST | Upload and parse resume |
| `/api/analyze` | POST | Analyze resume against JD |
| `/api/optimize` | POST | Optimize with approved keywords |
| `/api/generate` | POST | Generate LaTeX resume |
| `/api/resumes/:id` | GET | Get resume by ID |
| `/api/resumes` | GET | List all resumes |

## Usage Flow

1. **Upload Resume**: Upload a PDF or DOCX resume file
2. **Paste Job Description**: Enter the target job description
3. **View Analysis**: See ATS score, semantic match, and keyword analysis
4. **Approve Keywords**: Select which keywords to add to your resume
5. **Generate**: Create optimized resume with LaTeX templates
6. **Download**: Export as TXT, LaTeX, or PDF

## Safety Rules

The system **NEVER** fabricates experience:
- ✅ Allowed: Add approved keywords, improve wording, add skills section
- ❌ Not Allowed: Invent projects, companies, or experience

All keyword additions must come from:
- Job description keywords (approved by user)
- Manual skills input (provided by user)

## Project Structure

```
ats-resume-optimizer/
├── docker-compose.yml
├── package.json
├── README.md
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── api/
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   ├── vite.config.js
│   └── Dockerfile
├── backend/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── server.js
│   ├── package.json
│   └── Dockerfile
└── ml-service/
    ├── main.py
    ├── ats_model.py
    ├── resume_parser.py
    ├── latex_generator.py
    ├── requirements.txt
    └── Dockerfile
```

## License

MIT
