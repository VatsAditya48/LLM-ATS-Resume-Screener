# AI Resume Analyser

Screens a folder of resumes against a job description using an LLM, and
returns a ranked shortlist of the strongest and weakest candidates.

Given a job description and a batch of resumes (PDF or DOCX), the tool:

1. Extracts structured requirements from the job description (required skills,
   preferred skills, minimum experience, education requirements).
2. Parses each resume into a structured profile (skills, experience,
   education, projects, certifications) — regardless of how the resume is
   formatted or which section headings it uses.
3. Scores each candidate against the job description and produces a
   0–100 match percentage with a breakdown of matching/missing skills and
   a short verdict.
4. Ranks all candidates and prints the top and bottom performers.

## Why this exists

Manually screening dozens of resumes against a job description is slow and
inconsistent. This tool automates the first-pass screen so a recruiter can
focus their time on the shortlist, not the pile.

## Tech stack

- [Groq](https://groq.com/) (`llama-3.3-70b-versatile`) for fast, low-cost LLM inference
- [Pydantic](https://docs.pydantic.dev/) for structured, validated LLM outputs (JSON schema-constrained generation)
- `pypdf` / `python-docx` for resume text extraction

## Setup

```bash
git clone https://github.com/<your-username>/resume-analyser.git
cd resume-analyser
pip install -r requirements.txt
cp .env.example .env
# then edit .env and add your Groq API key
```

Get a free Groq API key at [console.groq.com](https://console.groq.com/).

## Usage

1. Put resumes (`.pdf` or `.docx`) in the `resumes/` folder.
2. Put your job description in `job_description.txt` (a sample Amazon SDE-I
   posting is included so the repo runs out of the box).
3. Run:

```bash
python resume_analyser.py
```

### Options

```bash
python resume_analyser.py \
  --resumes ./resumes \
  --job-description ./job_description.txt \
  --top 3 \
  --bottom 3 \
  --output results.json
```

| Flag | Description | Default |
|---|---|---|
| `--resumes` | Folder of resume files | `./resumes` |
| `--job-description` | Path to job description text file | `./job_description.txt` |
| `--top` | Number of top candidates to display | `2` |
| `--bottom` | Number of lowest-scoring candidates to display | `2` |
| `--output` | Save full results as JSON | (not saved) |
| `--sleep` | Seconds between LLM calls, to stay under rate limits | `5` |

## Sample output

```
Job role detected: Software Development Engineer I
Minimum experience: None
Education requirements: ["Bachelor's degree in Computer Science or related STEM field"]

Processing: jane_doe.pdf
  Score: 82.0
Processing: john_smith.docx
  Score: 45.0

========================================
TOP CANDIDATES
========================================

Jane Doe — 82.0%
{
  "candidate_name": "Jane Doe",
  "matching_skills": ["Python", "AWS", "distributed systems"],
  "missing_skills": ["Go"],
  "experience_requirement_met": true,
  "verdict": "Strong match, recommend for interview."
}
```

## Notes

- Scanned/image-only PDFs with no extractable text are skipped automatically.
- If one resume fails to process (bad file, malformed LLM output), the tool
  logs the error and continues with the rest of the batch.
- Real resumes contain personal data — the `resumes/` folder is gitignored
  so you don't accidentally commit anyone's PII.

## Possible extensions

- Swap the CLI for a small web UI (FastAPI + simple frontend)
- Add per-category scoring (skills / experience / projects / education) with
  matched vs. missing items, similar to a structured rubric
- Support multiple job descriptions run against the same resume pool
- Add an eval harness comparing LLM scores against human-labeled ground truth

## License

MIT
