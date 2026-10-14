# LearnLens AI — Your Course Material, Cited and Personalized

## Inspiration
Students often have to switch between lecture slides, textbook chapters, and lecture transcripts. Generic chatbot answers may not be tied to the material used in class. LearnLens AI explores a more verifiable study workflow: retrieve evidence from uploaded sources, keep citations attached to passages, and turn those passages into revision questions.

## What it does
LearnLens AI accepts text-based PDFs, PowerPoint slides, and transcript files (`.txt`, `.srt`, `.vtt`). It extracts passages while retaining page, slide, or transcript timestamp information. Students can ask questions and inspect the passages most relevant to their query. The assessment tab generates simple fill-in-the-blank questions from source sentences, checks responses against the source term, and records per-source accuracy for the current session.

## How we built it
The prototype uses Python and Streamlit. `pypdf` extracts PDF text, `python-pptx` extracts slide text, and a small lexical ranking function retrieves candidate passages. Quiz questions use a transparent extractive heuristic. Session-level mastery is represented by observed quiz accuracy.

## What is implemented today
- PDF, PPTX, TXT, SRT, and VTT ingestion
- Page, slide, and transcript timestamp citation anchors
- Evidence passage retrieval
- Source-derived cloze quiz baseline
- Cited answer feedback and session-level accuracy dashboard

## Limitations
This time-boxed MVP does not yet implement direct video transcription, OCR/vision for diagrams, generative LLM explanations, persistent student profiles, validated Bayesian knowledge tracing, or the full Track D evaluation framework. Retrieval and quiz quality require broader testing. We do not claim these features are completed.

## Built With
Python, Streamlit, pypdf, python-pptx, ChatGPT (AI-assisted development; code reviewed by the project owner).

## Try it
Instructions to run locally are in the public GitHub repository README. Add a public demo URL and demo video link once available.
