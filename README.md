# Grade 6-9 Math & English Practice Generator

A Streamlit web app that generates fresh **Grade 6-9 (US middle school → Algebra 1)**
multiple-choice practice questions for English and Math, powered by Google Gemini,
and exports them to **Word (.docx)** and **PDF**.

Pick a **Skill Domain**, set how many **Easy / Medium / Hard** questions you want,
and generate a ready-to-print practice set (with auto-rendered figures for Math).

## Why the domains match the Placement Test report

The subject dropdowns are loaded from [`curriculum.json`](curriculum.json), which uses
the **exact same 10 Skill Domains** shown on the Elite Prep Placement Diagnostic Report.
So when a student's report flags a weak domain, you select that **same domain name** here
to generate targeted practice.

| Subject | Skill Domains |
|---------|---------------|
| **English** | Grammar & Usage · Sentence Structure · Reading: Main Idea & Inference · Reading: Evidence & Detail · Vocabulary in Context |
| **Math** | Number & Operations · Ratio & Proportion · Algebra · Geometry · Data & Word Problems |

Difficulty is aligned to the curriculum: **Easy → foundational**, **Medium → intermediate**,
**Hard → advanced** skills of the chosen domain.

## Setup (local)

Requires Python 3.10+.

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate   |   macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt

cp .env.example .env        # then paste your Google Gemini API key into .env
streamlit run app.py
```

Get a free Gemini API key at https://aistudio.google.com/apikey.

Math figures are rendered with matplotlib (bundled in `requirements.txt`) — no extra setup.

## Deploy (Streamlit Community Cloud)

1. Push this repo to GitHub (public).
2. On https://share.streamlit.io, create a new app pointing at this repo, `app.py`.
3. In the app's **Settings → Secrets**, add:
   ```toml
   GOOGLE_API_KEY = "your_key_here"
   ```
4. Deploy. The resulting public URL can be linked from your website.

## Notes

- **Never commit your API key.** `.env` and `.streamlit/secrets.toml` are git-ignored.
- Question text, choices, and explanations are generated in English only.
- This tool is a standalone problem generator; it does **not** run the placement test
  or read student results — it only shares the same domain taxonomy for consistency.
