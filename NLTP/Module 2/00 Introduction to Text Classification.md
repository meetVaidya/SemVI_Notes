## What is Text Classification?
Text classification (also known as text categorization) is the task of assigning a predefined category or label to a piece of text. It's a fundamental task in Natural Language Processing (NLP) with numerous applications.

## Examples of Text Classification
*   **Spam Detection:** Identifying whether an email is spam or not.
*   **Subject Categorization of Articles:** Assigning topics to medical articles (e.g., using MeSH - Medical Subject Headings).
*   **Sentiment Analysis:** Determining the sentiment (e.g., positive, negative, neutral) expressed in a piece of text, like a movie or product review.
    *   **Positive Examples:**
        *   > "...zany characters and richly applied satire, and some great plot twists"
        *   > "...awesome caramel sauce and sweet toasty almonds. I love this place!"
    *   **Negative Examples:**
        *   > "It was pathetic. The worst part about it was the boxing scenes..."
        *   > "...awful pizza and ridiculously overpriced..."
*   **Authorship Attribution:** Identifying the author of a given text (e.g., determining if a document was written by Hamilton or Madison).
*   **Language Identification:** Determining the language a text is written in.
## Why Sentiment Analysis?
Sentiment analysis is crucial for:
*   **Movies:** Is a review positive or negative?
*   **Products:** What do people think about the new iPhone?
*   **Public Sentiment:** How is consumer confidence?
*   **Politics:** What do people think about a candidate or issue?
*   **Prediction:** Predict election outcomes or market trends from sentiment.
## Basic Sentiment Classification
*   Sentiment analysis is the detection of **attitudes**.
*   The simple task often focused on is determining if the attitude of a text is **positive or negative**.

## Summary of Text Classification Tasks
*   Sentiment analysis
*   Spam detection
*   Authorship identification
*   Language Identification
*   Assigning subject categories, topics, or genres

## Classification Methods
### 1. Hand-coded Rules
*   Rules are based on combinations of words or other features.
    *   Example (spam): `black-list-address OR ("dollars" AND "you have been selected")`
*   **Accuracy:** Can be high if rules are carefully refined by an expert.
*   **Drawback:** Building and maintaining these rules is expensive and time-consuming.
### 2. Supervised Machine Learning
*   **Input:**
    *   A document `d`
    *   A fixed set of classes `C = {c₁, c₂, ..., cJ}`
    *   A training set of `m` hand-labeled documents: `(d₁, c₁), ..., (dm, cm)`
*   **Output:**
    *   A learned classifier `γ: d → c`
*   **Types of Classifiers:**
    *   Naive Bayes
    *   Logistic Regression
    *   Neural Networks
    *   k-Nearest Neighbors (k-NN)
    *   ...and many others.