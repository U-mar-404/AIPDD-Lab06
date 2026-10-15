# University Academic Helpdesk

A small semantic FAQ retrieval prototype built with **Gradio** and a pretrained **sentence embedding model**. Students ask questions in everyday language, and the app returns the most relevant answer from a fixed FAQ list.

> The FAQ answers are illustrative lab content, not official university policy.

## Features

- Semantic search using `all-MiniLM-L6-v2` (no training or fine-tuning)
- Shows matched FAQ, suggested answer, cosine similarity and a status (Matched / Needs clarification)
- Input validation for empty or whitespace-only questions
- Configurable similarity threshold with an out-of-scope fallback
- Example queries for quick testing
- Blocks interface with two tabs: **Ask a Question** and **Browse FAQs**

## Setup

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

python -m pip install --upgrade pip
pip install -r requirements.txt
```

An internet connection is needed the first time to download the model. After it is cached, the app can run offline.

## Run

```bash
python app.py
```

Then open the local URL shown in the terminal (usually http://127.0.0.1:7860).

If you are using the notebook instead, open `Lab_06.ipynb` and run all cells from top to bottom.

## How it works

1. The FAQ questions are encoded **once** at startup.
2. Each user question is encoded and compared with the FAQ vectors using cosine similarity.
3. The best match is returned if its score is above `THRESHOLD`; otherwise the app asks the user to rephrase.

## Model

- `all-MiniLM-L6-v2` from [sentence-transformers](https://www.sbert.net/)

## Limitations

- Cosine similarity is **not** a probability or a measure of correctness.
- The top result can still be wrong, and out-of-scope questions can sometimes score above the threshold.
- The FAQ list is very small (6 entries), and the threshold is a hand-tuned value.
- Only English questions are supported.

## Possible improvements

- Show the top-3 matching FAQs and let the user choose
- Use a larger FAQ set
- Tune the threshold with more test cases, or compare the top-1 and top-2 scores
- Add user feedback on whether the answer helped

## Project files

| File | Purpose |
|---|---|
| `app.py` | Gradio application |
| `Lab_06.ipynb` | Notebook version with tests and written answers |
| `requirements.txt` | Dependencies and tested versions |
| `README.md` | This file |
