# Lang2Query: Text-to-SQL Converter

## 📌 Overview
**Lang2Query** is an advanced **Text-to-SQL** translation system that enables users to query relational databases using natural language. It leverages state-of-the-art **language modeling techniques** to generate **syntactically correct SQL queries**, bridging the gap between intuitive user inputs and structured database retrieval.

## 🚀 Features
- **Fine-Tuned Mistral Model**: Optimized for SQL query generation using **Low-Rank Adaptation (LoRA)** and **Retrieval-Augmented Generation (RAG)**.
- **Multiple Baseline Models**: Includes **N-Gram**, **Seq2Seq LSTM**, and **Pre-trained Mistral** for comparative evaluation.
- **Efficient Data Preprocessing**: Utilizes **FAISS-based vector retrieval** and **UnSloth library** for optimized tokenization.
- **Evaluation Metrics**: Assessed using **ROUGE-1, ROUGE-L, BLEU, and BERTScore**.

## 📊 Model Performance
| Model                  | ROUGE-1 | ROUGE-L | BLEU  | BERTScore |
|------------------------|---------|---------|-------|-----------|
| N-Gram                | 0.060   | 0.050   | 0.0001 | 0.7800    |
| Seq2Seq LSTM         | 0.090   | 0.090   | 0.0030 | 0.7900    |
| Baseline Mistral      | 0.130   | 0.130   | 0.0070 | 0.8000    |
| **Fine-Tuned Mistral** | **0.230** | **0.200** | **0.0230** | **0.8100** |

## 📚 Dataset
- **Source**: [Clinton/Text-to-SQL-v1 (HuggingFace)](https://huggingface.co/datasets/Clinton/Text-to-sql-v1)
- **Size**: 262,208 entries (~635 MB)
- **Train-Validation-Test Split**: **80%-10%-10%**

## 🛠️ Data Processing & Model Training
- **Vector Store Setup**: FAISS-based indexing for similarity search.
- **LoRA & RAG Integration**: Enhances model adaptability to unseen SQL structures.
- **Quantization**: 4-bit weight compression for memory efficiency.
- **Training Configuration**:
  - **Batch Size**: 4 (Gradient Accumulation: 8)
  - **Learning Rate**: 0.0001
  - **Precision**: FP16 (Half-Precision)
  - **Checkpoints**: Saved every 50 steps (max 2 checkpoints)

## 🏆 Sample Prediction
| **Input Query** | *"What is the listed date of the Warren pony truss bridge built in 1925?"* |
|-----------------|-------------------------------------------|
| **Database Schema** | `table_8098 (Name, Built, Listed, Location, County, Type)` |
| **Ground Truth SQL** | `SELECT "Listed" FROM table_8098 WHERE "Built" = '1925' AND "Type" = 'warren pony truss'` |
| **Model Prediction** | `SELECT "Listed" FROM table_8098 WHERE "Incumbent" = 'john randolph redistricted from the 1'` |
| **BLEU Score** | 0.0245 |
| **ROUGE-L Score** | 0.3077 |

## 📜 Installation & Usage
### 🔧 Prerequisites
- Python 3.8+
- Install dependencies:
  ```bash
  pip install -r requirements.txt

## 🚀 Running the Notebook
1️⃣ **Clone the repository**
  git clone https://github.com/oberoiharshith/Lang2Query.git
  cd Lang2Query

2️⃣ **Start Jupyter Notebook**
Open Lang2Query.ipynb and run the cells step by step.

## 📜 References
- TypeSQL (Yu et al., 2018)
- Dataset Decomposition for LLMs (Pouransari et al., 2024)
- Mistral-7B-Instruct
