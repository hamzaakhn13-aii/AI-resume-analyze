# AI-resume-analyze# 📄 AI Resume ATS Checker

A Streamlit app that scores a resume for Applicant Tracking System (ATS) friendliness and suggests concrete improvements, powered by Google's **Gemini Flash** model.

## Features
- Upload a resume as **PDF or DOCX**
- Optionally paste a **job description** for role-specific keyword matching
- **Overall ATS score (0–100)**, calculated from weighted category scores
- Category breakdown: Keywords, Experience & Impact, Formatting, Skills, Education & Contact, Readability
- Strengths, missing keywords, prioritized improvements, and example bullet rewrites
- Shows the plain text extracted from your resume (what an ATS actually "sees")

## Project structure
```
app.py            # the Streamlit app
requirements.txt  # Python dependencies
README.md         # this file
```

## Run locally
1. Install Python 3.10+.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Get a free Gemini API key at https://aistudio.google.com/apikey
4. Provide the key (pick one):
   - Paste it into the app's sidebar, **or**
   - Set an environment variable: `export GEMINI_API_KEY="your-key"` (Windows PowerShell: `$env:GEMINI_API_KEY="your-key"`)
5. Start the app:
   ```bash
   streamlit run app.py
   ```

## Configuration
| Setting | Where | Purpose |
|---|---|---|
| `GEMINI_API_KEY` | env var or Streamlit secret | Your Gemini API key |
| `GEMINI_MODEL` | env var or Streamlit secret (optional) | Model name. Default: `gemini-flash-latest` |

You can also change the model name in the app sidebar (e.g. `gemini-2.5-flash`).

## Deploy on Streamlit Community Cloud
1. Push this project to a public GitHub repository.
2. Go to https://share.streamlit.io and sign in with GitHub.
3. Click **Create app** → choose your repo, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and add:
   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```
5. Click **Deploy**.

> **Never commit your API key to GitHub.** Use Streamlit Secrets or the sidebar field.

## How scoring works
Gemini rates each category from 0–100. The overall score is a weighted average computed in code:

| Category | Weight |
|---|---|
| Keywords & Relevance | 25% |
| Experience & Impact | 25% |
| Formatting & Structure | 20% |
| Skills | 15% |
| Education & Contact Info | 10% |
| Readability & Grammar | 5% |

## Limitations
- This is an **AI estimate**, not the score of any real ATS (Workday, Greenhouse, Lever, etc. all work differently).
- Scanned/image-only resumes can't be read. Use a text-based PDF or DOCX.
- Very long resumes are truncated to ~15,000 characters.
- Your resume text is sent to Google's Gemini API. Don't upload documents you aren't comfortable sharing.
