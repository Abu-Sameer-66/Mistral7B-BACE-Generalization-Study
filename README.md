<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&ColorList=896A15,6E8915,98351F&height=200&section=header&text=BACE%20%7C%20Generalization%20Study&fontSize=50&fontColor=DEE2D9&animation=fadeIn&fontAlignY=35&desc=Mistral-7B%20%7C%20Scaffold%20Split%20%7C%20Peak%20ROC-AUC:%200.8034&descAlignY=60&descAlign=50" width="100%"/>
</div>

<div align="center">
  <img 
    src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=22&pause=1000&color=DEE2D9&center=true&vCenter=true&width=1000&lines=Fine-tuning+Mistral-7B+on+BACE-1+Inhibitors;Achieving+0.8034+Peak+ROC-AUC;Optimizing+Generalization+via+Low-Rank+Adapters;Scaffold+Split+Validation+for+Scientific+Rigor."
    alt="Typing SVG"
  />
</div>

<br/>

### 🧬 Scientific Mission
Achieving high generalization on **Scaffold Splits** is the gold standard for drug discovery. This study optimizes **Mistral-7B** for BACE-1 inhibitor prediction using a high-regularization approach (LoRA rank $r=8$) to prevent memorization and capture structural chemical signals.

### 📊 Performance Benchmark
- **Peak ROC-AUC:** **0.8034** (Captured at Step 500).
- **Methodology:** Low-Rank Adaptation + 5x Label Balancing + Early Stopping.
- **Framework:** Native integration prototype for **DeepChem GSoC 2026**.

---





### 🔍 Evidence of Peak Generalization
![Optimization Curve](bace_optimization_curve.jpeg)
*Figure: The model hits peak generalization before the onset of scaffold-split overfitting at Step 500.*

---

### 🛠️ Production Tech Stack
<div align="center">
  <img src="https://img.shields.io/badge/DeepChem-Scientific_AI-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black"/>
  <img src="https://img.shields.io/badge/LoRA_&_PEFT-Optimization-green?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/GitHub_Actions-CI%2FCD-success?style=for-the-badge&logo=githubactions"/>
</div>

---

### 📂 File Index
- `bace_benchmark.py`: Core fine-tuning script with peak detection logic.
- `requirements.txt`: Environment dependencies.
- `benchmark_evidence.jpeg`: Terminal logs confirming the 0.8034 ROC-AUC.

### 💻 Execution
```bash
# Ensure dependencies are installed
pip install -r requirements.txt

# Run the benchmark
python bace_benchmark.py
