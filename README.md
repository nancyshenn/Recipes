# 🍽️ Recipe Interaction Predictor

![Python](https://img.shields.io/badge/Python-Used-blue)
![Machine Learning](https://img.shields.io/badge/Type-Recommendation%20System-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📌 Project Overview
This project builds a **binary classification model** to predict whether a user will interact with (rate) a given recipe using data from Food.com.

By analyzing user behavior and recipe characteristics, we aim to model **user engagement patterns** and develop an accurate predictor of user-recipe interactions. This project combines **exploratory data analysis, feature engineering, and similarity-based modeling techniques** to improve prediction performance.

---

## 📂 Dataset Description
We use the **Food.com dataset** (Kaggle), which contains recipe metadata and user interactions:

- ~83,782 recipes with attributes such as ingredients, preparation time, and steps  
- ~731,927 user interactions including ratings and reviews  
- Key files used:
  - `RAW_recipes.csv`
  - `RAW_interactions.csv`
  - `interactions_train.csv`

Each interaction includes:
- `user_id`, `recipe_id`
- `rating` (1–5 scale)
- interaction timestamps  

These datasets were merged to enable comprehensive analysis of **user preferences and behavior**. 

---

## 📊 Exploratory Data Analysis (EDA)

### Key Findings:
- **Preparation time** showed extreme outliers, which were removed using the IQR method  
- **Number of steps (~8)** and **ingredients (~9)** followed stable distributions  
- After cleaning, distributions became closer to **right-skewed normal distributions**  
- Ratings were heavily skewed toward **high ratings (4–5 stars)**  
- Most users had **low activity**, with a few highly active outliers  

📈 Visualizations (see notebook):
- Histograms before/after outlier removal  
- Rating distributions  
- User activity distributions  
- Top tags and ingredients  

These insights informed feature selection and model design.

---

## 🎯 Predictive Task
The goal is to predict:

👉 **Will a user interact with (rate) a given recipe?**

This is formulated as a **binary classification problem**:
- **1 (Positive):** User interacted with recipe  
- **0 (Negative):** No interaction  

Model performance is evaluated using **accuracy**, with a balanced validation set of positive and negative samples. 

---

## 🤖 Model Development & Optimization

### Baseline Model
- Based on **recipe popularity** (number of reviews)
- Predict interaction if recipe is in the **top 50% most popular**
- Achieved ~**70% accuracy**

### Feature Engineering
- **User features:** historical interactions  
- **Recipe features:** popularity metrics  
- Removed:
  - NaN values  
  - Invalid ratings (rating = 0)

### Improved Model
- Added **similarity-based features**:
  - **Jaccard similarity**
  - **Cosine similarity**
- Weighted similarity by **user ratings**
- Reduced reliance on popularity

📈 Final performance:
- Improved accuracy from **~70% → ~79%**

This demonstrates the value of combining **popularity heuristics with collaborative filtering signals**. 

---

## ⚠️ Challenges & Unsuccessful Attempts

- **Similarity thresholds tuning** did not consistently improve results  
- Jaccard and Cosine similarity led to:
  - High **false positives**
  - Limited predictive power  

### Key Issue:
- **Data sparsity**
  - Many users had <10 interactions  
  - Many recipes had <20 reviews  

👉 Result:
- Popularity remained a **stronger predictor** than similarity metrics alone  

This highlights a common challenge in recommender systems:  
> Sparse interaction data limits the effectiveness of similarity-based methods.

---

## 📚 Literature Review & Similar Datasets

### Related Work
- *Generating Personalized Recipes from Historical User Preferences* (Majumder et al., 2019)
  - Used neural models with attention mechanisms  
  - Showed personalization improves engagement  

- Kaggle Recipe Recommender Systems
  - Use collaborative filtering and TF-IDF  
  - Emphasize ingredient-based similarity  

### Similar Dataset: Recipe1M+
- Over **1 million recipes + images**
- Used for:
  - Image-to-recipe generation  
  - Cross-modal learning  
  - Ingredient prediction  

👉 Compared to Recipe1M+, the Food.com dataset is stronger for:
- **User interaction modeling**
- **Behavioral analysis**

---

## 🔍 Key Insights
- **Popularity is a strong baseline** for predicting interactions  
- Similarity metrics alone are **not sufficient in sparse datasets**  
- User behavior is highly **skewed and unevenly distributed**  
- Data cleaning (outlier removal) significantly improves model performance  
- Simple models can perform well, but may lack **generalizability**

---

## 🔮 Conclusion
We developed a model that achieves **~79% accuracy** in predicting user-recipe interactions.

While effective, the model relies heavily on **popularity-based heuristics**, suggesting potential overfitting to dataset-specific patterns. More advanced features—such as user preferences, ingredient similarity, and latent representations—could further improve performance and generalizability.

👉 Future improvements:
- Incorporate **latent factor models** (e.g., matrix factorization)  
- Model **user preferences explicitly** (ingredients, cuisines)  
- Explore **deep learning-based recommender systems**  
---

📅 **Submission Date:** December 3, 2024  
📄 **Full Report:** [Assignment_2_Write_Up.pdf](https://docs.google.com/document/d/11d70F0-U2R2Duj4i3AYVjNjIrCMGBjr4YEiYqhzSFl4/edit?usp=sharing)
