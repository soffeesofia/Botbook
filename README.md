# Botbook: A Graph-Based Framework for Classification of Bot Accounts on Facebook

A research implementation of Botbook, a modular graph-based framework for detecting and classifying malicious social bot accounts on Facebook. The framework distinguishes between human users and three bot types — Trolls, Cyborgs, and Spam Bots — through a pipeline of feature engineering, traditional machine learning, and Graph Neural Networks.

Published as a Final Thesis Project for the Computer Science - Computer Applications Department, Saint Louis University, Baguio City.

---

## Authors

- Rona Domantay
- Leovide Daniel Bato
- Ezrha Leigh Dangilan
- Geoff Anthony Dulnuan
- Kaizer Cyn Gura
- Ava Narag
- Bernard Carlo Pacis
- Genrev Roque
- Jaymee Sofia Surro

**Adviser:** Rona Domantay  

---

## Abstract

This study addresses the rise of malicious social bots on Facebook and the threats they pose to online discourse. Botbook is a graph-based framework that detects and classifies bot accounts — distinguishing Humans from Trolls, Cyborgs, and Spam Bots — through the integration of behavioral, linguistic, and interaction-based features. A static graph model is built from user comment data, feature-rich profiles are constructed, and machine learning classifiers are applied to label users, with Random Forest achieving the highest classification performance (84%). Graph Neural Networks (GCN and GAT) are then employed to analyze user interactions, with GAT achieving 90.7% accuracy and superior F1 and AUC-ROC scores.

**Keywords:** Bots, Social Media, Facebook, Online Discourse, Graph Neural Networks

---

## Framework Overview

Botbook follows a five-stage modular pipeline:

**1. Data Collection**
Facebook comments were scraped from posts by major Philippine news outlets (ABS-CBN, GMA, Rappler, Inquirer, Philippine Star, Manila Bulletin) covering the 2022 Philippine Presidential Elections, using Apify's Facebook Comments Scraper. The final dataset contained 735,883 comments from 325,320 unique users across 350 posts. All personally identifiable information was anonymized.

**2. Data Annotation**
A stratified sample of 840 users was manually annotated by three independent annotators into four categories: Human, Troll, Cyborg, and Spam Bot. Inter-rater reliability was assessed using Krippendorff's Alpha and Fleiss' Kappa (both = 0.371), and final labels were assigned by majority vote.

| Class | Count | Proportion |
|---|---|---|
| Human | 453 | 53.86% |
| Troll | 206 | 24.49% |
| Cyborg | 156 | 18.55% |
| Spam Bot | 26 | 3.09% |

**3. Feature Extraction**
16 behavioral features were extracted per user across four categories:

| Category | Features |
|---|---|
| Linguistic | Average text length, innovation rate, average pairwise text dissimilarity, duplicate comment rate |
| Behavioral | Reply ratio, average comments per post, number of comments, number of unique posts/outlets |
| Temporal | Average response time, thread deviation, comment time variance |
| Engagement | Engagement (likes), average likes per comment, average media usage, average link usage |

**4. Traditional Machine Learning Classification**
Three classifiers were trained on the annotated, SMOTE-balanced dataset to label the remaining unlabeled users:

| Model | Accuracy | Macro F1-score |
|---|---|---|
| SVM | 79% | 0.79 |
| Random Forest | **84%** | **0.84** |
| XGBoost | 83% | 0.83 |

Random Forest was selected as the best-performing model.

**5. Graph Neural Network Classification**
A static interaction graph was constructed with 325,320 nodes (users) and ~6.1 million edges (reply and co-comment interactions). Each node carries a 16-dimensional feature vector. Two GNN architectures were compared using 10-fold cross-validation:

| Model | Accuracy | Precision | Recall | F1-score | AUC-ROC |
|---|---|---|---|---|---|
| GCN | 90.71% | 0.9768 | 0.2500 | 0.2378 | 0.4841 |
| GAT | **90.70%** | **0.9306** | **0.4554** | **0.5071** | **0.7645** |

GAT outperformed GCN in recall, F1-score, and AUC-ROC, demonstrating better generalization and minority class detection.

---

## Tech Stack

| Component | Technology |
|---|---|
| Language | Python |
| Data Collection | Apify Facebook Comments Scraper |
| Data Format | JSON |
| Machine Learning | Scikit-learn (SVM, Random Forest, XGBoost), SMOTE |
| Graph Construction | NetworkX / PyTorch Geometric |
| Graph Neural Networks | GCN, GAT (PyTorch Geometric) |
| Hyperparameter Tuning | GridSearchCV, RandomizedSearchCV |
| Evaluation | 10-fold cross-validation, Precision, Recall, F1, AUC-ROC |

---

## Scope and Limitations

- The dataset is limited to political discussions during the 2022 Philippine Presidential Elections
- A static graph model is used, which cannot capture temporal changes or evolving bot behavior
- Graph edges are based on comment relationships, not social network connections, due to Facebook's privacy policy
- The framework is platform-specific and may require adaptation for other social media platforms

---

## License

This project was created for academic research purposes at Saint Louis University. All rights reserved by the respective authors.
