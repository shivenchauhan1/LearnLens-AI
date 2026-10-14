# LearnLens AI — Track D MVP

A lightweight prototype for **Personalized Tutoring & Adaptive Learning**. It accepts text-based PDFs, PowerPoint files, and transcript files, preserves page/slide/timestamp source locations, retrieves relevant evidence, creates simple source-derived cloze questions, and tracks quiz accuracy during the current browser session.

> **Prototype honesty note:** This is a working baseline, not a completed implementation of every Track D requirement. The current retrieval is lexical and extractive. It does not call a generative LLM, OCR image-only pages/diagrams, transcribe raw video, or persist learner data across sessions. See “Known limitations” below.

## Run locally on macOS

Requires Python 3.10 or newer.

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

Streamlit prints a local URL, normally `http://localhost:8501`. Open it in your browser.

## How to use

1. Upload one or more text-based `.pdf`, `.pptx`, `.txt`, `.srt`, or `.vtt` files from the sidebar.
2. In **Ask your material**, type a question and inspect the matching passages with their citations.
3. In **Adaptive quiz**, generate questions derived from extracted course sentences. Check answers and use the cited source statement to revise.
4. In **Learning progress**, inspect observed accuracy by source/topic.
5. In **Source library**, inspect the extracted passages and location anchors.

For video content, export or obtain a `.srt`/`.vtt` transcript and upload it. Raw video transcription is not built into this MVP.

## Architecture

- **Ingestion:** `pypdf` extracts text per PDF page; `python-pptx` extracts text per slide; subtitle parsing retains transcript time ranges where present.
- **Source grounding:** passage records retain filename and page/slide/timestamp. A lexical term-frequency / inverse-document-frequency-style ranker finds source passages for a query.
- **Assessment:** a transparent cloze-question baseline blanks a distinctive word from an extracted sentence. Answers are checked against the source term.
- **Learner state:** per-source/topic correct and attempt counts are held in Streamlit session state and converted into observed accuracy. This is not yet Bayesian Knowledge Tracing and does not persist across sessions.

## Dependencies

- Python 3.10+
- Streamlit
- pypdf
- python-pptx

## Known limitations and next steps

1. Add OCR/vision support for diagrams and image-only slides.
2. Add direct video/audio transcription with timestamp alignment.
3. Add semantic embeddings + vector retrieval and a grounded LLM tutor with citations that open the exact passage.
4. Improve quiz generation with answer validation, difficulty/topic tags, duplicate tracking across sessions, and short-answer/numerical items.
5. Persist learner profiles in SQLite and implement/compare a principled mastery model.
6. Build a ground-truth evaluation set and report retrieval precision/recall, faithfulness, answer relevance, question repetition, and simulated student mastery changes.

## AI-tool disclosure

AI-assisted development: ChatGPT was used to help draft and organize parts of this prototype and its documentation. The project owner should review, test, understand, and take responsibility for all submitted code. Add any other AI coding tools actually used to this disclosure and to the Devpost **Built With** section.

## Track alignment

This MVP demonstrates a subset of Track D: source-linked ingestion, source-aware retrieval, baseline assessment, and session-level progress. It does **not** yet satisfy all requirements for multimodal image extraction, LLM explanation, durable learner modeling, or system evaluation. Do not claim these unfinished items are implemented.
