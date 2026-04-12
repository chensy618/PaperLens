# PaperLens · AI Paper Annotation

> Give your literature reading **structure and depth**

PaperLens is a fully client-side academic paper annotation tool. It calls the Anthropic API directly from your browser, transforming PDF papers into professional dual-column annotation pages.

---

## Features

- **Two input methods** — Upload a local PDF or paste a direct link from arXiv / bioRxiv
- **Two annotation modes** — Logic analysis or reading question checklist
- **UI language toggle** — Switch the entire interface between Chinese and English with one click
- **Bilingual annotations** — Annotation output language is independently configurable (Chinese or English)
- **Streaming generation** — Real-time progress display, no waiting for the full response
- **Export results** — Download the annotated output as a self-contained HTML file
- **History** — Automatically saves the last 8 analyses; reopen any of them instantly
- **Privacy-first** — API Key and history are stored only in local browser storage; no data passes through any intermediate server

---

## Quick Start

### 1. Get an Anthropic API Key

Go to [console.anthropic.com](https://console.anthropic.com), create an account, and add credits to obtain an API Key (format: `sk-ant-...`).

> **Note:** A Claude.ai Plus subscription and Anthropic API credits are two separate billing systems. You need to add credits in the console independently. Minimum top-up is $5; each paper costs roughly $0.20–0.35.

### 2. Open PaperLens

Open `index.html` directly in your browser, or visit [chensy618.github.io/PaperLens](https://chensy618.github.io/PaperLens).

### 3. Set your API Key

Click the **API Key** button in the top-right corner, enter your key, and save. The green dot indicates the key is ready.

### 4. Analyze a paper

Choose an input method, annotation mode, and output language, then click **Start Analysis**. Results appear in 1–2 minutes.

---

## Annotation Modes

### Mode A — Question Checklist

Auto-generates (or uses custom) reading questions and color-codes passages in the original text that relate to each question.

**Best for:** Focused close reading, literature reviews, seminar presentation prep.

Page structure:
1. Top nav bar (paper title)
2. Section jump bar
3. Question card list (Q1–Q5+, each with a color indicator)
4. Dual-column body (left: original text with color highlights, right: analysis cards per question)
5. Bottom answer worksheet (core argument, key evidence, and potential limitations for each question)

**Custom questions:** After selecting this mode, enter one question per line in the "Custom reading questions" box. Leave it blank to auto-generate 5 standard questions.

### Mode B — Logic Analysis

Focuses on the paper's argumentative structure rather than predefined questions — identifying core claims, evidence, concessions, and rebuttals.

**Best for:** Evaluating argument quality, critical reading, writing reference.

Highlight color guide:

| Color | Meaning |
|-------|---------|
| Yellow | Core claim / thesis |
| Pink | Key defined terms |
| Blue | Data / statistics / experimental results |
| Green | Concessions / rebuttals |
| Purple | Methodology choices |

Page structure:
1. Top nav bar (paper title + legend)
2. Section jump bar
3. Argument flow chain (Problem → Claim → Evidence → Rebuttal → Conclusion)
4. Dual-column body (left: highlighted text, right: logic position + argumentation technique cards)
5. Bottom overview (core thesis, argument skeleton, strongest evidence, weakest point)

---

## Input Methods

### Local Upload
- Supported format: `.pdf`
- Maximum file size: 10 MB
- Supports drag-and-drop or click-to-browse

> If your file exceeds 10 MB, compress it first with [smallpdf.com](https://smallpdf.com) or [ilovepdf.com](https://ilovepdf.com).

### URL Input
- Supports direct PDF links from arXiv, bioRxiv, and similar platforms
- arXiv abstract URLs (`arxiv.org/abs/...`) are automatically converted to PDF links
- Multiple CORS proxies are tried automatically if a direct fetch fails

---

## Cost Reference

Using the `claude-3-5-sonnet-20241022` model:

| Item | Rate |
|------|------|
| Input | $3 / 1M tokens |
| Output | $15 / 1M tokens |

**Each paper costs approximately $0.20–0.35** (depending on PDF size and analysis depth). $5 covers roughly 15–20 papers.

Track your usage at [console.anthropic.com/usage](https://console.anthropic.com/usage).

---

## File Reference

| File | Description |
|------|-------------|
| `index.html` | Main application |
| `graphcast_logic_analysis.html` | Example output: GraphCast paper, Logic Analysis mode |
| `graphcast_question_list.html` | Example output: GraphCast paper, Question Checklist mode |
| `paper_annotator.html` | Earlier prototype (kept for reference) |

---

## Running Locally

PaperLens is a static page with no backend or build tools required:

```bash
# Open directly in your browser
open index.html

# Or start a local server (recommended to avoid browser cross-origin restrictions)
python3 -m http.server 8080
# Then visit http://localhost:8080
```

---

## Privacy

- API Key is stored in browser `localStorage` and is only valid on your machine
- Analysis history is stored in browser `localStorage`, capped at 8 entries
- PDF content is sent directly from your browser to the Anthropic API — no third-party servers involved
- Clearing browser data removes both the key and history

---

## Tech Stack

- Pure HTML / CSS / JavaScript — no framework dependencies
- [Anthropic Messages API](https://docs.anthropic.com/en/api/messages) with streaming
- Google Fonts: Playfair Display, DM Sans, DM Mono
