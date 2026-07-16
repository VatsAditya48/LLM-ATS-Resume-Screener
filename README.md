# 🤖 LLM ATS Resume Screener

An AI-powered Applicant Tracking System (ATS) that automatically analyzes and ranks resumes against a job description using Large Language Models (LLMs).

The project extracts structured information from both job descriptions and resumes, compares candidates against hiring requirements, and ranks them based on their overall suitability.

---

## 🚀 Features

- 📄 Extracts text from PDF and DOCX resumes
- 🧠 Uses Groq LLM for intelligent resume parsing
- 📋 Parses job descriptions into structured data
- 🎯 Matches resumes against job requirements
- 📊 Generates an overall match score (0–100)
- 🏆 Ranks all candidates from best to worst
- 📌 Displays top and lowest matching candidates
- ⚡ Supports processing multiple resumes in one run

---

## 🛠 Tech Stack

- Python 3.11+
- Groq API
- Pydantic
- python-docx
- pypdf

---

## 📂 Project Structure

```
LLM-ATS-Resume-Screener/
│
├── resume_analyser.py
├── requirements.txt
├── .env
├── README.md
└── Resumes/
    ├── Resume1.pdf
    ├── Resume2.pdf
    └── Resume3.docx
```

---

## ⚙️ Installation

Clone the repository

```bash
git clone https://github.com/yourusername/LLM-ATS-Resume-Screener.git

cd LLM-ATS-Resume-Screener
```

Create a virtual environment

```bash
python -m venv .venv
```

Activate it

### Windows

```bash
.venv\Scripts\activate
```

### Linux / macOS

```bash
source .venv/bin/activate
```

Install dependencies

```bash
pip install -r requirements.txt
```

---

## 🔑 Environment Variables

Create a `.env` file in the project root.

```env
GROQ_API_KEY=your_groq_api_key
```

---

## ▶️ Usage

Place all resumes inside your resume folder.

Run the application

```bash
python resume_analyser.py
```

The application will:

- Parse the job description
- Parse every resume
- Compare resumes against the job requirements
- Generate an overall score
- Rank candidates from highest to lowest

---

## 📊 Sample Output

```
Minimum Experience: 1.0

Education Requirements:
['Bachelor's Degree']

Processing: John_Doe.pdf
Score: 92

Processing: Jane_Smith.pdf
Score: 84

Processing: Alex.pdf
Score: 61

TOP CANDIDATES

John Doe - 92%
Jane Smith - 84%

LOWEST CANDIDATES

Alex - 61%
```

---

## 📌 Future Improvements

- Export results to CSV/Excel
- Streamlit web interface
- Upload resumes through UI
- ATS keyword highlighting
- Semantic similarity using embeddings
- Deterministic scoring algorithm
- Support for scanned PDFs using OCR

---

## 📄 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

**Aditya**

If you found this project useful, consider giving it a ⭐ on GitHub.
