# Lab 01 — Sentiment Analysis Using Traditional Machine Learning

## 1. Laboratory Session
- **Lab number:** 01
- **Title:** Text Preprocessing, TF-IDF, and Machine Learning
- **Dataset:** UCI Sentiment Labelled Sentences (IMDb, Amazon, Yelp)
- **Environment:** Python 3, Pandas, Scikit-learn, NLTK, Matplotlib, Google Colab

## 2. Objective
The objective of this laboratory activity was to build a baseline sentiment classifier using traditional Natural Language Processing (NLP) and machine learning techniques. By establishing a non-LLM baseline, this lab helps to demonstrate the limitations of traditional bag-of-words models, which motivates the need for more advanced architectures like Transformers (explored in Lab 03) and LLMs.

## 3. Tasks and Implementation

1. **Data Loading:** Loaded 2,748 sentences across three domains (IMDb, Amazon, Yelp) using Pandas. *(Note: The raw UCI text files contained formatting anomalies which caused standard CSV readers to skip ~252 lines; this was documented and accepted as a standard limitation of the raw dataset).*
2. **Text Preprocessing:** Implemented a cleaning pipeline that converted text to lowercase, removed URLs, stripped punctuation/numbers, and normalized whitespace. 
3. **Exploratory Data Analysis (EDA):** Plotted the most frequent words for positive and negative classes, revealing that while terms like "great" and "bad" were strong indicators, domain-specific words like "movie" and "phone" appeared heavily in both classes.
4. **Data Splitting:** Split the dataset using an 80/20 train-test split (`random_state=42`), stratified to maintain class balance.
5. **Feature Extraction:** Converted text to numerical features using two methods:
   - **BOW (Bag of Words):** Counts word frequencies (Vocabulary size: 4,388).
   - **TF-IDF:** Weights words by importance and includes bigrams (Vocabulary size: 5,000).
6. **Model Training:** Trained four model combinations: Logistic Regression and Linear SVM, evaluated on both BOW and TF-IDF representations.

## 4. Results and Evidence

The models were evaluated on a test set of 550 unseen sentences. The results table is as follows:

| Model | Accuracy | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- | :--- |
| **SVM - BOW** | **0.8073** | **0.8132** | **0.8014** | **0.8073** |
| SVM - TF-IDF | 0.8073 | 0.8178 | 0.7942 | 0.8059 |
| LogReg - BOW | 0.8073 | 0.8251 | 0.7834 | 0.8037 |
| LogReg - TF-IDF | 0.8055 | 0.8269 | 0.7762 | 0.8007 |

**Best Model Classification Report (SVM-BOW):**
- **Accuracy:** 81% (0.81)
- **Unhappy (0):** Precision 0.80, Recall 0.81, F1 0.81
- **Happy (1):** Precision 0.81, Recall 0.80, F1 0.81

*(Visual evidence of the top word charts, confusion matrix, and training outputs can be found in the `/screenshots` folder).*

## 5. Observations

- **Model Comparison:** The Linear SVM using basic Bag-of-Words (BOW) achieved the highest F1-score (0.8073). Surprisingly, TF-IDF did not significantly outperform BOW in this specific binary task, suggesting the frequency of words alone was highly discriminative. 
- **Class Balance:** The model performed equally well on both the "Happy" and "Unhappy" classes (0.81 F1-score for both), showing no bias toward a specific sentiment.
- **The Failure of "Bag-of-Words" (Contrast Sentences):** When tested on new, unseen sentences, the model correctly identified simple positive and negative sentences. However, it completely failed on contrast sentences.
  - *Test Sentence:* "I expected it to be bad, but actually it was great." 
  - *Model Prediction:* 😞 SAD (Incorrect).
  - *Reasoning:* Because BOW models discard word order, the model saw the word "bad" and heavily weighted the sentence as negative, completely missing the contrasting conjunction "but" and the word "great". 
- **Limitation:** This proves that traditional ML models lack contextual understanding and compositionality. They cannot understand negation (e.g., "not good") or complex syntax. This directly motivates the use of Transformer-based architectures (Lab 03) which use self-attention to understand the relationship between words in a sequence.

## 6. Learning Outcomes
- Developed a complete, reproducible NLP pipeline from raw text to model evaluation.
- Understand the critical difference between `fit_transform` on training data versus `transform` on test data to prevent data leakage.
- Can interpret Precision, Recall, and F1-scores in the context of a balanced binary classification task.
- Critically evaluated the fundamental limitations of Bag-of-Words models regarding word order and contextual meaning.
