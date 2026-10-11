# AI Usage Log

Document Autopilot · ITAI 1378 Computer Vision and AI. Each entry shows what I asked or the problem I had, what the AI suggested, what I learned and how I applied it. I keep adding entries through the Final Work.

## 1. Choosing models for reading ID documents
**Date**: September 20, 2026

**Tool Used**: ChatGPT, Claude and Gemini (deep research)

**Question Asked**: Which free, open-source OCR and vision-language models can read passports and ID cards, and how do the ICAO Doc 9303 check digits work?

**What the AI Suggested**: An overview of open-source OCR engines and small vision-language models, and the ICAO check-digit rules for the machine-readable code lines.

**What I Learned**: No single model reads an ID safely. The machine-readable code lines can be checked exactly with check digits, while the printed fields come in several alphabets and need OCR.

**How I Applied It**: I designed the pipeline with exact readers first and AI only for the gaps, and kept a model only after checking its licence on the official model card.

## 2. Measuring accuracy and confidence
**Date**: September 20, 2026

**Tool Used**: ChatGPT, Claude and Gemini (deep research)

**Question Asked**: How should I measure the accuracy of a document reader, and how can I tell when its confidence scores can be trusted?

**What the AI Suggested**: Ways to measure field accuracy and to calibrate confidence scores.

**What I Learned**: Every value needs a confidence score and a second check, and a model's score only means something once it is calibrated on data the model has not seen.

**How I Applied It**: I treated every model and benchmark number as unverified until measured on my own test split. My primary metric is exact-match accuracy of five critical fields on 150 unseen test documents, and confidence is calibrated on a separate validation split.

## 3. Reviewing my written design
**Date**: October 4, 2026

**Tool Used**: Codex

**Problem**: I wanted an independent check of my written design before turning it into slides.

**What the AI Suggested**: In each of five review rounds, a list of weak points and open questions in the design.

**What I Learned**: A design is easier to defend when every weak point is either fixed or recorded as a deliberate decision.

**How I Applied It**: Every finding was fixed or turned into an explicit decision, and each fix was re-checked in the next round.

## 4. Designing the Midterm slides
**Date**: October 5, 2026

**Tool Used**: Claude Code

**Problem**: I wrote the content of my 8 Midterm slides in my design notes and wanted a clean visual design for it. Building slides in code is a skill outside this course.

**What the AI Suggested**: A JavaScript slide script (pptxgenjs) that lays out my content in PowerPoint with cards, icons and a workflow diagram. It also helped me turn my design notes into first drafts of the README and data plan.

**What I Learned**: How a slide deck can be generated from code instead of drawn by hand.

**How I Applied It**: I edited the slide wording myself in PowerPoint, and checked the dataset facts against the MIDV-2020 paper and the model licences on Hugging Face (PaddleOCR-VL-1.6 and Qwen3-VL-4B: Apache-2.0).

## 5. Understanding MRZ check digits
**Date**: October 5, 2026

**Tool Used**: Claude Code

**Question Asked**: How do ICAO check digits work, and which OCR misreads can they catch or miss?

**What the AI Suggested**: It assisted with drafting the early notebook `notebooks/00_mrz_check_digits.ipynb`, which checks the two official ICAO specimen documents and simulates 10,000 one-character OCR misreads.

**What I Learned**: Check digits caught every wrong digit but only about 92% of wrong letters, because some letter swaps change the weighted sum by a multiple of 10. A passing check digit proves a line is consistent, not that it was read correctly.

**How I Applied It**: The design reads the code lines first, re-reads every value with a second OCR engine, and accepts an OCR repair only when exactly one candidate passes, with a person still confirming it.

## Rules I follow
- AI suggestions are proposals; I run, test and understand every line before it goes in.
- I review every slide and README line myself before I submit.
- No real person's document is ever given to an AI tool, only the mock, synthetic and specimen data in `data/README.md`.
- Code adapted from tutorials or AI output is attributed in a comment or in this log.
