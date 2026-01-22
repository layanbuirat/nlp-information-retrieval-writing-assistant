# Intelligent Writing Assistant for Lab Experiments  
**ENCS5141 — Intelligent Systems Laboratory — Case Study 2**

---

## 📌 Project Overview  
This project implements an **intelligent writing assistant** tailored for engineering students writing laboratory experiment reports. The system integrates:

- **NLP Sentence Classification** – Detects grammar and spelling errors in user input.  
- **Information Retrieval (IR)** – Retrieves relevant sections from technical documents to assist with writing and correction.  

The assistant helps students improve their technical writing by identifying errors and suggesting relevant content from a curated database of lab experiment documents.

---

## 🎯 Key Objectives  
1. Build a balanced dataset with realistic grammatical and spelling errors.  
2. Implement and compare multiple classification models (Random Forest, LSTM, DistilBERT).  
3. Develop an effective IR system using TF-IDF and BM25.  
4. Perform in-depth error analysis and evaluate model performance.  
5. Create a fully integrated prototype that combines classification with retrieval.

---

## 🛠️ Tools & Technologies  
| Category           | Tool/Library         | Purpose                          |
|--------------------|----------------------|----------------------------------|
| Framework          | PyTorch              | Neural network implementation    |
| NLP                | Transformers         | Pre-trained language models      |
| Machine Learning   | scikit-learn         | Traditional ML models            |
| Data Handling      | pandas, NumPy        | Data manipulation                |
| Text Processing    | NLTK                 | Text cleaning and preprocessing  |
| Visualization      | matplotlib, seaborn  | Results visualization            |
| Information Retrieval | rank_bm25        | BM25-based retrieval             |

---

## 📂 Dataset  
- **Source:** JFLEG corpus (grammatical errors) + synthetically generated spelling errors.  
- **Classes:** OK, GRAMMAR_ERROR, SPELLING_ERROR  
- **Size:** 900 sentences (300 per class)  
- **Splits:**  
  - Train: 630 sentences  
  - Validation: 135 sentences  
  - Test: 135 sentences  

Balanced and cleaned to prevent data leakage.

---

## 🧠 Models Implemented  

### 1. **Baseline Model**  
- **Algorithm:** Random Forest + TF-IDF  
- **Accuracy:** 66.67% (validation), 63.70% (test)  
- **Key Feature:** Bigrams helped capture short-range error patterns.

### 2. **LSTM Model**  
- **Architecture:** Bidirectional LSTM with self-attention  
- **Best Validation Accuracy:** 72.59%  
- **Strength:** Excellent at detecting spelling errors (97.78% accuracy in validation).

### 3. **Transformer Model**  
- **Model:** DistilBERT-base-uncased  
- **Fine-tuning:** 3 epochs, LR = 2e-5  
- **Performance:** Underperformed (27.41% test accuracy) likely due to limited data.

---

## 📊 Evaluation Results  

### Classification Performance (Test Set)  
| Model               | Accuracy | Precision | Recall | F1-Score |
|---------------------|----------|-----------|--------|----------|
| Random Forest       | 63.70%   | 0.6871    | 0.6370 | 0.6492   |
| LSTM                | 50.37%   | 0.5437    | 0.5037 | 0.4945   |
| DistilBERT          | 27.41%   | 0.2746    | 0.2741 | 0.2737   |

### Per-Class Accuracy  
| Model               | OK       | Grammar Error | Spelling Error |
|---------------------|----------|---------------|----------------|
| Random Forest       | 53.33%   | 66.67%        | 71.11%         |
| LSTM                | 80.00%   | 31.11%        | 40.00%         |
| DistilBERT          | 31.11%   | 24.44%        | 26.67%         |

**Key Insight:** All models struggled significantly with **grammatical errors**, which are more subtle and context-dependent than spelling errors.

---

## 🔍 Information Retrieval System  

### Document Collection  
10 simulated lab experiment PDFs (3–8 pages each), chunked into ~74-word segments.

### Retrieval Methods  
1. **TF-IDF** with cosine similarity  
2. **BM25** (k1=1.5, b=0.75)  
3. **Hybrid** (60% TF-IDF + 40% BM25)

### IR Performance (Precision@3 / Recall@3)  
| Method  | Precision@3 | Recall@3 |
|---------|-------------|----------|
| TF-IDF  | 0.400       | 0.382    |
| BM25    | **0.467**   | **0.471**|
| Hybrid  | 0.444       | 0.438    |

**BM25 performed best**, especially for specific technical queries like *"troubleshooting circuit problems"*.

---

## 🧩 Integrated System Workflow  
1. **Input:** User writes a sentence (e.g., *"The transistor amplify the signal."*).  
2. **Classification:** System detects error type (e.g., GRAMMAR_ERROR).  
3. **Query Formulation:** Automatically generates a search query (e.g., *"subject verb agreement errors lab reports"*).  
4. **Retrieval:** Searches document corpus for relevant sections.  
5. **Output:** Presents error correction + retrieved reference material.

---

## 📈 Key Findings & Insights  
- **Grammar errors are the hardest** to detect (error rates >70% across models).  
- **Sentence length correlates positively** with detection accuracy (longer sentences = better performance).  
- **Stopword removal hurt performance** (−8.9% accuracy), suggesting function words carry grammatical signals.  
- **BM25 outperformed TF-IDF** in retrieving relevant technical content.

---

## 🚧 Limitations & Future Work  

### Limitations  
- Small and synthetic dataset limits generalization.  
- Transformer models underperformed due to data size.  
- IR system constrained by limited document collection.  

### Future Directions  
- Collect larger, real-world datasets from student lab reports.  
- Experiment with ensemble models (Random Forest + LSTM).  
- Test advanced transformers (RoBERTa, ELECTRA).  
- Expand IR corpus with more lab manuals and textbooks.  

---

## 📚 References  
1. Napoles, C., Sakaguchi, K., & Tetreault, J. (2017). JFLEG: A Fluency Corpus for Grammatical Error Correction.  
2. Wolf, T., et al. (2020). Transformers: State-of-the-Art Natural Language Processing.  
3. Internal course materials: *Introduction to NLP* and *Information Retrieval* (BZU, 2026).

---

## 👤 Author  
**Layan Buirat** – 1211439  

--- 

📌 *This project is part of the ENCS5141 Intelligent Systems Laboratory at the Faculty of Engineering and Technology, Department of Electrical and Computer Engineering.*