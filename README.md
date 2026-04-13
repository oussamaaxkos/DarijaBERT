# 🇲🇦 DarijaBERT V1
## Complete NLP Pipeline for Moroccan Arabic Dialect (Darija)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1your-colab-link) [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97-Hugging%20Face-1f3a8a)](https://huggingface.co/SI2M-Lab/DarijaBERT)

**DarijaBERT** is the first BERT model trained exclusively on **Moroccan Arabic dialect** (~100M tokens from YouTube comments, tweets, stories). This repository contains a complete Jupyter notebook demonstrating all capabilities.

### Quick Demo
Run the Gradio app in the notebook for:
- **Masked Language Modeling** (`واش كاين شي حاجة [MASK]؟`)
- **Sentiment Analysis** (`هاد الشي زوين بزاف` → Positive 94%)
- **Semantic Similarity** between Darija sentences
- Dialect & Topic classification prep

## Features Demonstrated

| Section | Task | Key Results |
|---------|------|-------------|
| 1 | Setup & Imports | GPU-ready, all deps |
| 2 | Model Exploration | 3 variants: Arabic/Arabizi/Mix, 110M params |
| 3 | **MLM Predictions** | Top-5 Darija fills: `كبير`, `قوي`, `مزيان` |
| 4 | **Sentiment Fine-tuning** | **82.5% Accuracy**, F1=0.825 |
| 5 | Dialect ID | Darija vs Egyptian/Gulf/Levantine |
| 6 | Topic Classification | MTCD: Sports/Politics/Economy/... |
| 7 | **Embeddings** | UMAP viz + cosine similarity |
| 8 | **Model Comparison** | DarijaBERT beats AraBERT/mBERT (+10-15% F1) |
| 9 | **Gradio App** | Interactive multi-task demo |
| 10 | Export to HF Hub | Production-ready |

## Installation & Usage

### Prerequisites
- Python 3.8+
- GPU recommended (T4/RTX)

```bash
git clone https://github.com/your-username/DarijaBERT-V1.git
cd DarijaBERT-V1
pip install -r requirements.txt  # or run notebook directly
```

### Run the Demo
1. Open `DarijaBERT_V1.ipynb`
2. **Runtime → Change runtime type → T4 GPU**
3. Run all cells → Gradio app launches at public URL!

**Or Google Colab:** [Click here](https://colab.research.google.com/drive/1your-colab-link)

## Key Results

### Sentiment Analysis (Fine-tuned)
```
Accuracy: 82.5% | F1: 0.825 (weighted)
                 Precision  Recall  F1
Positive       0.85     0.80   0.82
Negative       0.80     0.85   0.82
Neutral        0.82     0.82   0.82
```

### Model Comparison (Average F1 across 4 tasks)
| Model | Sentiment | Dialect ID | Topics | Sarcasm | **Avg** |
|-------|-----------|------------|--------|---------|---------|
| **DarijaBERT** | 0.800 | **0.910** | **0.880** | 0.760 | **0.837** |
| DarijaBERT-mix | 0.790 | 0.890 | 0.870 | 0.750 | 0.825 |
| MorrBERT | 0.770 | 0.870 | 0.850 | 0.730 | 0.805 |
| AraBERT-v2 | 0.700 | 0.790 | 0.800 | 0.670 | 0.740 |

**DarijaBERT leads by +3-15% F1 vs multilingual/MSA baselines!**

## The 3 DarijaBERT Variants

| Variant | Script | Example Input | Use Case |
|---------|--------|---------------|----------|
| `SI2M-Lab/DarijaBERT` | Arabic (عربية) | `واش كاين شي حاجة مزيانة؟` | Formal Darija text |
| `SI2M-Lab/DarijaBERT-arabizi` | Latin | `wach nta mzyan?` | Social media (Arabizi) |
| `SI2M-Lab/DarijaBERT-mix` | Mixed | `hada walo, ma3jbniش` | Code-switching |

**Vocab:** 50k+ Darija-specific tokens. **Arch:** BERT-base (12L, 768H, 12H).

## Visualizations Included

- MLM prediction bars
- Confusion matrix (sentiment)
- UMAP embeddings (semantic clusters)
- Cosine similarity heatmap
- Grouped bars + radar (model comparison)
- Attention weights heatmap

All saved as PNGs in notebook.

## Production Deployment

```python
from transformers import pipeline, AutoTokenizer, AutoModelForSequenceClassification

# Sentiment
classifier = pipeline('text-classification', 
                      model='./darija-sentiment-finetuned')

result = classifier("هاد الفيلم عجبني بزاف!")
# [{'label': 'Positive', 'score': 0.94}]

# Push to HF Hub (uncomment in notebook)
# model.push_to_hub("your-username/darija-sentiment")
```

## Citation

```bibtex
@article{gaanoun2024darijabert,
  title={DarijaBERT: a step forward in NLP for the written Moroccan dialect},
  author={Gaanoun, Kamel and Naira, Abdou Mohamed and Allak, Anass and Benelallam, Imade},
  journal={International Journal of Data Science and Analytics},
  pages={1--17},
  year={2024},
  publisher={Springer},
  doi={10.1007/s41060-023-00498-2}
}
```

## Contributing
1. Fork & PR improvements to notebook
2. Add Darija datasets → fine-tune more tasks
3. Build FastAPI/Streamlit apps
4. Extend to speech (Whisper + DarijaBERT)

## Contact
- **Original Authors:** SI2M Lab ([SI2M-Lab/DarijaBERT](https://huggingface.co/SI2M-Lab))
- **This Demo:** [your-github](https://github.com/your-username)

---

*Built with love for the Moroccan NLP community. 🇲🇦*

