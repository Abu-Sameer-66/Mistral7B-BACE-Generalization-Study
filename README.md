<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&ColorList=896A15,6E8915,98351F&height=200&section=header&text=BACE%20%7C%20Generalization%20Study&fontSize=50&fontColor=DEE2D9&animation=fadeIn&fontAlignY=35&desc=Mistral-7B%20%7C%20Scaffold%20Split%20%7C%20Best%20ROC-AUC:%200.8371&descAlignY=60&descAlign=50" width="100%"/>
</div>

<div align="center">
  <img 
    src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=22&pause=1000&color=DEE2D9&center=true&vCenter=true&width=1000&lines=Fine-tuning+Mistral-7B+on+BACE-1+Inhibitors;Best+ROC-AUC:+0.8371+on+Scaffold+Split;Low-Rank+Adapters+for+Chemical+Generalization;DeepChem+GSoC+2026+Pre-Proposal+Research."
    alt="Typing SVG"
  />
</div>

<br/>

## 🧬 Scientific Mission

Achieving high generalization on **Scaffold Splits** is the gold standard for drug discovery. Standard random splits leak structural information — the model memorizes scaffolds rather than learning chemistry. This study optimizes **Mistral-7B** for BACE-1 inhibitor prediction using two distinct training strategies, isolating the exact conditions that produce peak generalization on unseen molecular scaffolds.

---

## 📊 Results — Both Experiments

| Experiment | Strategy | ROC-AUC | Split |
|------------|----------|---------|-------|
| Experiment 1 (`bace_mistral_benchmark.py`) | Step-based, 2500 steps, peak at Step 500 | 0.8034 | Scaffold |
| Experiment 2 (`mistral-bace-epoch5.ipynb`) | Epoch-based, 5 epochs, peak at Epoch 4 | **0.8371** ✅ | Scaffold |

**Final Best: 0.8371 ROC-AUC — Epoch 4, Scaffold Split, Kaggle T4**

Key finding: Epoch-based training with explicit overfitting detection outperforms fixed step-based training. The model peaks at Epoch 4 (0.8371) and begins overfitting at Epoch 5 (0.8042) — confirming the importance of early stopping tied to scaffold-split evaluation rather than training loss.

---

## 🔬 Experiment Details

### Experiment 1 — Step-Based Peak Detection
- **File:** `bace_mistral_benchmark.py`
- **Strategy:** Evaluate every 250 steps, capture peak before overfitting
- **LoRA:** r=8, lora_alpha=16, dropout=0.2
- **Balancing:** 5x oversampling of positive class
- **Peak:** Step 500 → ROC-AUC **0.8034**

### Experiment 2 — Epoch-Based with Overfitting Guard ✅ Final
- **File:** `mistral-bace-epoch5.ipynb`
- **Strategy:** 5 epochs, save checkpoint on every improvement
- **LoRA:** r=8, lora_alpha=16, target q_proj + v_proj
- **Training curve:**

| Epoch | ROC-AUC | Status |
|-------|---------|--------|
| 1 | 0.6933 | Learning |
| 2 | 0.7908 | Improving ↑ |
| 3 | 0.8167 | New record ↑ |
| 4 | **0.8371** | **BEST** ✅ |
| 5 | 0.8042 | Overfitting ↓ |

**Scientific insight:** Overfitting begins exactly at Epoch 5 — this validates that scaffold-split evaluation must be used as the early-stopping criterion, not training loss.

---

## 🛠️ Tech Stack

<div align="center">
  <img src="https://img.shields.io/badge/DeepChem-Scientific_AI-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black"/>
  <img src="https://img.shields.io/badge/LoRA_&_PEFT-Optimization-green?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Mistral--7B-4bit_NF4-purple?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/RDKit-Chemistry-red?style=for-the-badge"/>
</div>

---

## 📂 File Index

| File | Description |
|------|-------------|
| `bace_mistral_benchmark.py` | Experiment 1 — step-based training, ROC-AUC 0.8034 |
| `mistral-bace-epoch5.ipynb` | Experiment 2 — epoch-based, best ROC-AUC **0.8371** |
| `requirements.txt` | Environment dependencies |

---

## 💻 Execution
```bash
pip install -r requirements.txt

# Experiment 1 — step based
python bace_mistral_benchmark.py

# Experiment 2 — open in Kaggle
# kaggle.com/sameernadeem66/mistral-bace-epoch5
```

---

## 🔗 Part of DeepChem GSoC 2026 Research

This benchmark is part of a complete pre-proposal research suite:

| Task | Model | Result | Link |
|------|-------|--------|------|
| BACE Classification | Mistral-7B QLoRA | **0.8371** ROC-AUC | This repo |
| ClinTox Classification | Mistral-7B QLoRA | 0.9913 ROC-AUC | [ClinTox Repo] |
| BBBP Classification | OLMo-7B QLoRA | 0.7100 ROC-AUC | [BBBP Repo] |
| ESOL Regression | OLMo-7B + Reg Head | 0.8582 RMSE | [ESOL Repo] |
| SMILES Generation | OLMo-7B + RDKit TSM | 20/20 = 100% valid | [Generation Repo] |
