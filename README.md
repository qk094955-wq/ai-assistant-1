# ai-assistant-1# 📄 ATS Resume Checker

A Streamlit app that scores a resume for Applicant Tracking System (ATS) compatibility and suggests concrete improvements, powered by Google's Gemini Flash model.

## Features

- Upload a resume as **PDF, DOCX or TXT**
- Optional **job description** field for a tailored keyword match
- Overall **ATS score (0-100)** plus a 5-category breakdown
- Strengths, prioritized improvements with rewritten example lines
- Missing keywords and formatting issues
- Download the report as JSON

## Project structure

```
.
├── app.py              # Streamlit app
├── requirements.txt    # Python dependencies
└── README.md
```

## Run locally

1. Get a free Gemini API key at https://aistudio.google.com/apikey
2. Install and run:

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

export GEMINI_API_KEY="your-key"   # Windows PowerShell: $env:GEMINI_API_KEY="your-key"
streamlit run app.py
```

Alternatively create `.streamlit/secrets.toml` (do **not** commit it):

```toml
GEMINI_API_KEY = "your-key"
```

If no key is configured, the app shows a password field in the sidebar.

## Configuration

| Setting | How | Default |
|---|---|---|
| API key | `GEMINI_API_KEY` env var or Streamlit secret | none |
| Model | `GEMINI_MODEL` env var or sidebar field | `gemini-2.5-flash` |

## Deploy on Streamlit Community Cloud

1. Push this repo to GitHub (see below).
2. Go to https://share.streamlit.io and sign in with GitHub.
3. Click **Create app** → choose your repo, branch `main`, main file `app.py`.
4. Open **Advanced settings → Secrets** and add:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**.

## Push to GitHub

Add a `.gitignore` containing:

```
venv/
__pycache__/
.streamlit/secrets.toml
.env
```

Then:

```bash
git init
git add .
git commit -m "Initial commit: ATS resume checker"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

(Create the empty repo on github.com first.)

## Notes and limitations

- The score is an AI estimate of ATS-friendliness, not the output of a real ATS.
- Scanned/image-only resumes can't be read; export a text-based PDF or DOCX.
- Resume text is sent to the Gemini API; avoid uploading data you don't want processed by a third party.
