# Kreuzberg vs Gemini PDF Processing Benchmark

A benchmark comparing two different resume-processing pipelines using the Google Gemini API and Kreuzberg.

The goal of this experiment was to test whether preprocessing PDFs before sending them to an LLM can reduce latency and improve overall pipeline efficiency.

---

# Pipelines Compared

## 1. Raw PDF → Gemini

```text
PDF Resume → Gemini API → Structured Information Extraction
```

In this setup, Gemini directly receives the PDF and internally performs:
- PDF parsing
- OCR
- layout understanding
- multimodal document indexing

---

## 2. Kreuzberg → Gemini

```text
PDF Resume → Kreuzberg → Clean Text → Gemini API
```

In this setup:
1. Kreuzberg extracts text from the PDF
2. The text is lightly cleaned
3. Gemini only processes plain text

This removes the need for Gemini to handle document parsing internally.

---

# Information Extracted

Both pipelines extracted the following information:

- Full Name
- Location
- Years of Experience
- Skills
- Education
- Previous Companies

The same:
- PDF
- prompt
- Gemini model

were used for both tests to keep the benchmark fair.

---

# Objective

This experiment focuses on comparing:

- End-to-end latency
- Processing overhead
- LLM document ingestion efficiency
- Benefits of document preprocessing

---

# Tech Stack

- Python
- Google Gemini API
- Kreuzberg
- Google Colab
- Pandas
- Matplotlib

---

# Installation

```bash
pip install google-generativeai kreuzberg pandas matplotlib
```

---

# Benchmark Workflow

## Raw PDF Pipeline

```text
Upload Resume
      ↓
Gemini API
      ↓
PDF Parsing + OCR + Layout Understanding
      ↓
Structured JSON Output
```

---

## Kreuzberg Pipeline

```text
Upload Resume
      ↓
Kreuzberg Extraction
      ↓
Text Cleaning
      ↓
Gemini API
      ↓
Structured JSON Output
```

---

# Key Observation

Even though the Kreuzberg pipeline sends more visible text to Gemini, it significantly reduces overall execution time.

This suggests that:
- multimodal PDF parsing introduces hidden overhead
- document preprocessing can improve inference speed
- plain-text inference is often faster than raw document ingestion

---

# Why This Matters

Many production AI systems avoid sending raw documents directly to LLMs.

Instead, they:
- preprocess documents
- extract text separately
- clean content before inference
- optimize for lower latency and scalability

This benchmark demonstrates a simplified version of that production architecture.

---

# Example Use Cases

- Resume Parsing
- AI Recruitment Systems
- RAG Pipelines
- Enterprise Search
- Document Intelligence
- Automated Form Processing

---

# Author

Samuel Hanok

MSc Applied Data Science & Analytics

Interested in:
- AI Infrastructure
- LLM Systems
- Production AI Engineering
- Data Engineering
- Machine Learning Systems
