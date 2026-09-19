<div align="center">

# 📚 Book Recommender

*Find your next favourite read — just describe what you're in the mood for.*

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Gradio](https://img.shields.io/badge/Gradio-6.24-FF7C00?style=for-the-badge&logo=gradio&logoColor=white)](https://www.gradio.app/)
[![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/)
[![ChromaDB](https://img.shields.io/badge/Vector_Store-ChromaDB-6B3FA0?style=for-the-badge)](https://www.trychroma.com/)
[![LangChain](https://img.shields.io/badge/LangChain-0.4-1C3C3C?style=for-the-badge)](https://www.langchain.com/)

<br/>

> A semantic book recommendation engine powered by vector search, zero-shot classification, and emotion analysis — wrapped in a beautiful Gradio UI.

</div>

---

## ✨ What it Does

Type something like *"a dark psychological thriller with an unreliable narrator"* or *"a heartwarming story about family and belonging"* — and get 16 book recommendations that match the **meaning** of your words, not just the keywords.

On top of that, you can narrow results by:

| Filter | Options |
|--------|---------|
| 📂 **Category** | All · Fiction · Nonfiction · Children's Fiction · Children's Nonfiction |
| 🎭 **Emotional Tone** | All · 😊 Happy · 😢 Sad · 😮 Surprising · 😨 Suspenseful · 😠 Angry |

---

## 🧠 How it Works

The system runs a three-stage AI pipeline to enrich the book dataset before serving recommendations:

```
Raw Dataset (Kaggle)
      │
      ▼
┌─────────────────────────┐
│  1. Data Cleaning       │  Filter short descriptions, normalise fields
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  2. Text Classification │  facebook/bart-large-mnli (zero-shot)
│     Fiction / Nonfiction│  → books_with_categories.csv
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  3. Emotion Analysis    │  j-hartmann/emotion-english-distilroberta-base
│  anger·joy·fear·sadness │  → books_with_emotions.csv
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  4. Vector Embeddings   │  all-MiniLM-L6-v2 → ChromaDB
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  5. Gradio Dashboard    │  Semantic search + filter + cover gallery
└─────────────────────────┘
```

---

## 🗂️ Project Structure

```
book-recommender/
│
├── 📓 Notebooks (run in order)
│   ├── data-exploration.ipynb       ← Download & clean the Kaggle dataset
│   ├── text-classification.ipynb    ← Zero-shot Fiction/Nonfiction labelling
│   ├── sentiment-analysis.ipynb     ← Emotion scoring per book
│   └── vector-search.ipynb          ← Build & test the ChromaDB vector store
│
├── 🚀 App
│   └── gradio-dashboard.py          ← Main app entry point
│
├── �️ Assets
│   └── cover-not-found.jpg          ← Fallback cover image
│
├── 📄 Documentation
│   ├── README.md                    ← Project overview and setup steps
│   └── requirements.txt             ← Python dependencies
│
├── 🔐 Config
│   └── .env.example                 ← Sample environment variables
│
├── .gitignore                       ← Ignore local caches and generated artifacts
└── .env                             ← Local API keys (never commit this!)
```

---

## 🤖 Models

| Model | Source | Task |
|-------|--------|------|
| `all-MiniLM-L6-v2` | sentence-transformers | Semantic embeddings for vector search |
| `facebook/bart-large-mnli` | Meta AI | Zero-shot Fiction / Nonfiction classification |
| `j-hartmann/emotion-english-distilroberta-base` | Jochen Hartmann | Emotion scoring across 7 emotions |

---

## ⚡ Quick Start

### 1 — Clone & install

```bash
git clone https://github.com/your-username/book-recommender.git
cd book-recommender
pip install -r requirements.txt
```

### 2 — Set up environment variables

Create a `.env` file in the project root:

```env
HF_TOKEN=your_huggingface_token_here
HF_HUB_DISABLE_XET=1
```

> Get your free token at [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

### 3 — Run the notebooks in order

| # | Notebook | Output |
|---|----------|--------|
| 1 | `data-exploration.ipynb` | `books_cleaned.csv` |
| 2 | `text-classification.ipynb` | `books_with_categories.csv` |
| 3 | `sentiment-analysis.ipynb` | `books_with_emotions.csv` |
| 4 | `vector-search.ipynb` | `tagged_description.txt` |

> **GPU recommended** for notebooks 2 and 3 — they run large transformer models.  
> The Gradio app itself runs fine on CPU.

### 4 — Launch the app

```bash
python gradio-dashboard.py
```

Open [http://localhost:7860](http://localhost:7860) in your browser. 🎉

---

## 📦 Tech Stack

| Layer | Technology |
|-------|-----------|
| Data processing | `pandas` · `numpy` |
| Visualisation | `matplotlib` · `seaborn` |
| ML / NLP | `transformers` · `torch` · `sentence-transformers` |
| Vector store | `chromadb` · `langchain-chroma` |
| Orchestration | `langchain-community` · `langchain-huggingface` · `langchain-text-splitters` |
| UI | `gradio` |
| Utilities | `python-dotenv` · `kagglehub` · `tqdm` |

---

## 📄 Dataset

[**7k Books with Metadata**](https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata) by Dylan Castillo — ~6,810 books with titles, authors, descriptions, ratings, and cover thumbnails sourced from Google Books.

---

<div align="center">

Made with ❤️ and way too many book recommendations

</div>
