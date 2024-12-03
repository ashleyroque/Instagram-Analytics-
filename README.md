
# Instagram Engagement Classification

## 📜 Project Overview  
This project aims to predict whether an Instagram post will have **high** or **low engagement** based on specific post characteristics. Engagement is measured by likes and comments, and the model enables predictions prior to posting. This project is essential for **brands**, **content creators**, and **marketers** looking to optimize their strategies and foster better audience interactions.

## 🎯 Goals  
1. **Predict engagement levels** (high/low) before a post is published.  
2. **Identify key features** influencing Instagram engagement.

---

## 📊 Dataset  
The dataset used is sourced from [Kaggle: Instagram Data](https://www.kaggle.com/datasets/propriyam/instagram-data).  
**Key Features**:  
- `is_video`: Indicates if the post is a video.  
- `caption`: The text included in the post.  
- `comments`: Number of comments on the post.  
- `likes`: Number of likes the post received.  
- `followers`: Number of followers the user has.  
- `multiple_images`: Indicates if the post contains multiple images.  

**Target Variable**:  
- `engagement_level`: High or low engagement based on engagement rate.

---

## 🧹 Data Preprocessing  
- **Handling Missing Values**: Filled missing captions and locations with placeholders like `no caption` and `no location`.  
- **Feature Engineering**:  
  - Created `engagement_rate` using the formula:  
    \[
    \text{engagement\_rate} = \frac{\text{likes} + \text{comments}}{\text{followers}}
    \]
  - Classified posts as `high` or `low` engagement based on the median engagement rate.  
- **Boolean Conversion**: Converted `is_video` and `multiple_images` into numerical values (`1` for True, `0` for False).  

---

## 📈 Visualizations  
### Correlation Heatmap  
Examined relationships between features such as followers, likes, and comments.  

```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 8))
correlation_matrix = df.corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt='.2f')
plt.title('Feature Correlation Heatmap')
plt.show()
```

### Bar Chart  
Compared average engagement rates for posts with single vs. multiple images.  

```python
post_type_engagement = df.groupby('multiple_images')['engagement_rate'].mean()
fig, ax = plt.subplots(figsize=(8, 6))
post_type_engagement.plot(kind='bar', color='skyblue', ax=ax)
ax.set_title("Engagement Rate by Post Type")
ax.set_xlabel("Post Type (0: Single Image, 1: Multiple Images)")
ax.set_ylabel("Average Engagement Rate")
plt.show()
```

---

## 🤖 Modeling  
- Used **Logistic Regression** for binary classification of engagement levels.  
- Achieved an **accuracy score of 98.93%** on the test set.  
- Evaluation included a confusion matrix and classification report.

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report, confusion_matrix

model = LogisticRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

print("Classification Report:\n", classification_report(y_test, y_pred))
```

### Confusion Matrix  
```python
sns.heatmap(confusion_matrix(y_test, y_pred), annot=True, cmap='Blues', fmt='d')
plt.title("Confusion Matrix")
plt.xlabel("Predicted")
plt.ylabel("True")
plt.show()
```

---

## 📖 Insights  
1. Posts with **multiple images** showed slightly higher engagement on average.  
2. Engagement doesn't solely depend on follower count—**timing, content type**, and **post format** are significant.  

---

## 🌟 Impact  
- **For Content Creators**: Offers insights to tailor posts for better engagement.  
- **For Brands**: Enhances posting strategies to reach a larger audience effectively.  
- **Ethical Considerations**: While useful, such models could incentivize creators to prioritize engagement metrics over authentic content.


---

## 💡 Future Work  
- Experiment with advanced models like **Random Forest** or **Gradient Boosting** to address overfitting issues.  
- Explore additional features, such as **post timing** or **hashtag usage**.

---

## 📜 References  
1. [Kaggle Dataset: Instagram Data](https://www.kaggle.com/datasets/propriyam/instagram-data)  
2. [Scikit-learn: Logistic Regression Documentation](https://scikitlearn.org/dev/modules/generated/sklearn.linear_model.LogisticRegression.html)  
3. [IBM: Logistic Regression Overview](https://www.ibm.com/topics/logistic-regression)  
4. [Scikit-learn: Confusion Matrix Documentation](https://scikitlearn.org/dev/modules/generated/sklearn.metrics.confusion_matrix.html)  
5. [Medium: How to Create a Seaborn Correlation Heatmap](https://medium.com/@szabo.bibor/how-to-create-a-seaborn-correlation-heatmap-in-python-834c0686b88e)  
6. [Seaborn: Heatmap Documentation](https://seaborn.pydata.org/generated/seaborn.heatmap.html)  
7. [W3Schools: Confusion Matrix Explanation](https://www.w3schools.com/python/python_ml_confusion_matrix.asp)  


