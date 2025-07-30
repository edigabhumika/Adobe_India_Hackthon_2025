
# 📚 Adobe India Hackathon 2025 - Connecting the Dots Challenge

**Theme:** *Rethink Reading. Rediscover Knowledge.*

In an age where documents overwhelm more than they inform, this challenge focuses on *context over content*. This repository presents solutions that turn static PDFs into intelligent, interactive research companions — fully offline and containerized.

---

## 🧩 Challenge Overview

This repository includes solutions to both parts of **Round 1** of the hackathon:

- **Challenge 1A:** Structured PDF Outline Extraction  
- **Challenge 1B:** Multi-Document, Persona-Driven Content Analysis

All solutions:
- Run in **CPU-only environments**
- Require **no internet access**
- Are fully **Dockerized**

---

## 🗂 Challenge 1A – Structured PDF Processing

### 🔍 Approach
- Extract document title by identifying the **largest font size** in the top third of the first page.
- Analyze font sizes throughout the document to **build a structured outline**.
- Use heuristics to map font sizes to heading levels (**H1, H2, H3**).

### 🛠 Libraries Used
- `PyMuPDF (fitz)` – for PDF parsing
- `Python 3.10` – language runtime

### ▶️ How to Build & Run (Docker)

**Navigate to Challenge 1A directory:**
```bash
cd Challenge_1a
```

**Build Docker image:**
```bash
docker build --platform linux/amd64 -t challenge1a .
```

**Run the container:**

**Windows:**
```bash
docker run --rm `
  -v "${PWD}\sample_dataset\pdfs:/app/input:ro" `
  -v "${PWD}\sample_dataset\outputs\challenge1a:/app/output" `
  --network none `
  challenge1a
```

**Linux/macOS:**
```bash
docker run --rm   -v $(pwd)/sample_dataset/pdfs:/app/input:ro   -v $(pwd)/sample_dataset/outputs/challenge1a:/app/output   --network none   challenge1a
```

**📤 Output:**  
Structured `JSON` files in `sample_dataset/outputs/`, each containing:
- `title`
- `outline` with heading hierarchy

---

## 🧠 Challenge 1B – Multi-Collection Persona-Based PDF Analysis

### 🔍 Approach
- Parse input persona and task from JSON
- Process all PDFs in the collection
- Match headings/paragraphs with persona task
- Rank and extract **relevant sections** by importance
- Generate structured summary with metadata

### 🛠 Libraries Used
- `PyMuPDF (fitz)` – PDF parsing
- `json`, `os`, `re` – standard Python libraries

### ▶️ How to Build & Run (Docker)

**Navigate to Challenge 1B directory:**
```bash
cd ../Challenge_1b
```

**Build Docker image:**
```bash
docker build --platform linux/amd64 -t challenge1b .
```

**Run the container for a collection (example: Collection 1):**

**Windows:**
```bash
docker run --rm -v "${PWD}\Collection 1:/app/input:ro" -v "${PWD}\Collection 1:/app/output" --network none challenge1b
```

**Linux/macOS:**
```bash
docker run --rm   -v "$(pwd)/Collection 1:/app/input:ro"   -v "$(pwd)/Collection 1:/app/output"   --network none   challenge1b
```

📤 **Output:**  
- `challenge1b_output.json` in the same collection folder  
- Contains:  
  - Extracted sections with **titles**, **page numbers**, and **refined content**

🔁 Repeat for `Collection 2` and `Collection 3` by adjusting volume paths.

---

## 📁 Folder Structure

```
Adobe-India-Hackathon25/
├── Challenge_1a/
│   ├── Dockerfile
│   ├── process_pdfs.py
│   ├── requirements.txt
│   └── sample_dataset/
│       ├── pdfs/
│       ├── outputs/
│       └── schema/
├── Challenge_1b/
│   ├── Dockerfile
│   ├── challenge1b.py
│   ├── Collection 1/
│   ├── Collection 2/
│   └── Collection 3/
└── README.md
```

---

## ✅ Constraints Satisfied

- ✅ Offline execution only (no internet required)
- ✅ Pure CPU-based (no GPU needed)
- ✅ Fully containerized (Docker)
- ✅ Deterministic output formats adhering to Adobe schemas

---

Let’s **connect the dots** — and redefine how we **read, analyze, and learn** from documents.

🚀 Happy Hacking!
