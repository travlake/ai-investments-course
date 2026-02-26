# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Public-facing** course repository for **Finance 372T/397: "AI Powered Investments"** at McCombs School of Business, UT Austin. Contains Jupyter notebook homework assignments, example code, and supporting data (CSV, PDF, TXT) for teaching financial analysis using AI tools. Students and the general public can see this repo. Licensed under MIT (Travis Lake Johnson).

A separate **private** repository (`ai-investments-dev`) is used for development, solution authoring, and other instructor-only materials.

## Repository Structure

- `Homework1/` through `Homework4/` — Assignment notebooks with accompanying data files
- `Examples/` — Demonstration notebooks (e.g., `StructuringText.ipynb`) and reference documents
- Solution notebooks (`*_solution*.ipynb`) exist locally but are not linked from the README; be careful not to commit or push solutions to this public repo

## Execution Environment

All notebooks are designed to run on **Google Colab**. There is no local build system, requirements.txt, or test framework. Dependencies are installed inline within notebooks (e.g., `!pip install`). The primary AI API used is **Google Gemini** via the `google-genai` library; students supply their own API keys.

## Key Libraries

pandas, scikit-learn (CountVectorizer), nltk (VADER sentiment), sentence-transformers, PyPDF2, google-genai

## Notebook Conventions

- Each homework follows a task-based structure (Task 1, Task 2, etc.) with markdown instructions and code cells
- Bracketed placeholders mark student input: `[*your name here*]`, `[*prompt*]`
- Grading criteria are stated in markdown at the top
- Notebooks include an "Open in Colab" badge linking to `colab.research.google.com/github/travlake/ai-investments-course/blob/main/...`
- Students convert completed notebooks to HTML for submission via Canvas

## API Key Safety

API keys have been accidentally committed before (see commit `7974ffd`). Never commit API keys; use placeholder text like `api_key="YOUR KEY HERE"`.
