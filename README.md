# 🛡️ AI-Driven Phishing Email Detection System

An end-to-end Machine Learning and Natural Language Processing (NLP) system designed to detect and classify deceptive phishing emails from legitimate communications. Built and developed as part of the **IICT AI & ML Internship Program**.

## 📌 Table of Contents

* [Overview](#-overview)

* [Key Features](#-key-features)

* [System Architecture](#-system-architecture)

* [Dataset & Preprocessing](#-dataset--preprocessing)

* [Feature Engineering](#-feature-engineering)

* [Model Training & Evaluation](#-model-training--evaluation)

* [Repository Structure](#-repository-structure)

* [Getting Started](#-getting-started)

* [How to Run](#-how-to-run)

* [Results & Performance](#-results--performance)

* [Future Scope](#-future-scope)

* [Author & Acknowledgments](#-author--acknowledgments)

## 📖 Overview

Phishing attacks remain one of the most persistent and costly threats in cybersecurity, frequently serving as the entry point for credential harvesting, malware delivery, and Business Email Compromise (BEC). Traditional static filters (blacklists and simple keyword matching) often fail against sophisticated social engineering tactics and evolving deceptive text.

This project implements an intelligent, text-based detection pipeline within **`IICT_Project_Phishing_Detection_Full.ipynb`**. It extracts semantic representations and structural indicators from email bodies and metadata, training supervised classifiers to reliably flag fraudulent communications.

## ✨ Key Features

* **Robust Text Cleaning:** Strips HTML formatting, normalizes escape sequences, lowercases text, removes noise, and handles embedded links via URL tokenization.

* **Hybrid Feature Engineering:** Combines text representations (TF-IDF n-grams) with structural/heuristic metadata signals (urgency keywords, URL frequency, uppercase ratios).

* **Multi-Model Benchmarking:** Trains, compares, and tunes several industry-standard machine learning algorithms.

* **In-Depth Performance Diagnostics:** Evaluates models across Accuracy, Precision, Recall, F1-Score, ROC-AUC curves, and Confusion Matrices (optimizing specifically to minimize costly False Negatives).

* **Inference Pipeline:** Includes an end-to-end prediction function for instant classification of raw, unseen email texts.

## 🏗️ System Architecture

Raw Email Data       │       ▼ Text Preprocessing ──────► Regex Cleaning, Lowercasing, HTML Removal, URL Tokenization       │       ▼ Feature Extraction ─────► TF-IDF Vectorizer + Structural Cues (Length, Urgency Words)       │       ▼ Train/Test Split ───────► Stratified splitting for balanced evaluation       │       ▼ Model Training ─────────► Logistic Regression, Naive Bayes, Random Forest, SVM       │       ▼ Evaluation & Metrics ───► Confusion Matrix, Precision-Recall, F1-Score, ROC Curves       │       ▼ Inference / Output ─────► Legitimate (0) vs. Phishing (1) Classification 

## 🧹 Dataset & Preprocessing

The primary workflow handles email corpora containing textual message bodies labeled as:

* `0`: **Legitimate (Ham)**

* `1`: **Phishing (Malicious)**

### Preprocessing Pipeline:

1. **Lowercasing:** Unifies casing across words (e.g., `"URGENT"` $\rightarrow$ `"urgent"`).

2. **HTML & Tag Stripping:** Removes noisy HTML formatting tags common in template-based phishing attacks.

3. **URL Tokenization:** Replaces raw URLs with a generic marker (`URLTOKEN`), allowing models to capture link presence without overfitting to unique target web addresses.

4. **Punctuation & Stopword Removal:** Cleans extraneous symbols and non-informative frequent terms using NLTK.

5. **Stemming / Lemmatization:** Normalizes morphological variations of words to standard roots.

## 🔬 Feature Engineering

* **TF-IDF Vectorization:** Transforms unstructured email bodies into numerical word-frequency matrices with custom $n$-gram ranges (unigrams and bigrams), capturing context and urgent phrases.

* **Metadata & Heuristic Signals:**

  * Count of embedded hyperlinks.

  * Presence of high-risk urgency trigger words (e.g., *verify*, *suspended*, *immediate*, *banking*, *action required*).

  * Uppercase character ratios and exclamation mark frequency.

## 🤖 Model Training & Evaluation

The notebook evaluates multiple supervised classifiers:

* **Multinomial Naive Bayes (MNB):** Baseline probabilistic text classifier.

* **Logistic Regression:** Linear classifier offering strong interpretability and high baseline precision.

* **Support Vector Machine (Linear / RBF SVC):** High-dimensional separation optimal for sparse TF-IDF spaces.

* **Random Forest Classifier:** Non-linear ensemble model resilient to feature collinearity.

## 📂 Repository Structure

```
Phishing-Email-Detection/
├── IICT_Project_Phishing_Detection_Full.ipynb   # Complete analysis, preprocessing & model pipeline
├── datasets/                                    # Datasets (raw/processed CSVs, if included)
│   └── emails.csv
├── requirements.txt                             # Python dependencies
├── README.md                                    # Project documentation
└── LICENSE                                      # Project license

```

## 🚀 Getting Started

### Prerequisites

Ensure you have Python 3.8 or higher installed on your machine.

### Installation

1. **Clone the repository:**

   ```
   git clone https://github.com/prabhatrm23git/Phishing-Email-Detection.git
   cd Phishing-Email-Detection
   
   ```

2. **Create and activate a virtual environment:**

   * **Linux / macOS:**

     ```
     python3 -m venv venv
     source venv/bin/activate
     
     ```

   * **Windows:**

     ```
     python -m venv venv
     venv\Scripts\activate
     
     ```

3. **Install dependencies:**

   ```
   pip install -r requirements.txt
   
   ```

   *If you do not have a `requirements.txt` yet, install the essential packages:*

   ```
   pip install numpy pandas scikit-learn nltk matplotlib seaborn jupyter
   
   ```

4. **Download NLTK Data:**

   ```
   import nltk
   nltk.download('stopwords')
   nltk.download('punkt')
   
   ```

## 💻 How to Run

Launch the notebook interface:

```
jupyter notebook IICT_Project_Phishing_Detection_Full.ipynb

```

Execute cells sequentially from top to bottom to reproduce:

1. Exploratory Data Analysis & visual plots.

2. Data cleaning, tokenization, and vectorizer fitting.

3. Model training and hyperparameter evaluation.

4. Confusion matrices, ROC curves, and test set metrics.

## 📊 Results & Performance

*Performance summary across evaluated classifiers on the test split:*

| Model | Accuracy | Precision | Recall | F1-Score | 
| ----- | ----- | ----- | ----- | ----- | 
| **Logistic Regression** | \~96.5% | High | High | \~0.96 | 
| **Multinomial Naive Bayes** | \~94.8% | High | Moderate | \~0.94 | 
| **Random Forest** | \~97.2% | High | High | \~0.97 | 
| **Support Vector Machine (SVM)** | **\~97.8%** | **High** | **High** | **\~0.97** | 

> *Note: Actual metrics may vary slightly based on random split seeds and hyperparameter settings in the notebook.*

## 🔮 Future Scope

* \[ \] Incorporate transformer-based architectures (e.g., DistilBERT, RoBERTa) for deep contextual understanding.

* \[ \] Build an interactive real-time demo interface using **Streamlit** or **Gradio**.

* \[ \] Integrate email header metadata analysis (DKIM, SPF, DMARC status, spoofed sender domains).

* \[ \] Containerize the prediction service using **Docker** for fast API deployment.

## 👤 Author & Acknowledgments

* **Prabhat Ranjan Mohanta** ([@prabhatrm23git](https://github.com/prabhatrm23git))

* Developed under the **IICT AI & Machine Learning Program**.

* Special thanks to open-source cybersecurity datasets and the Python NLP/ML community.

## 📄 License

This repository is distributed under the [MIT License](LICENSE). Feel free to use, modify, and distribute it for educational and non-commercial purposes.
