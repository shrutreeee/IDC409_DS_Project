# IDC409_DS_Project
#### ~Kavish Parab (MS22231) and Shruti Swaminathan (MS22139)
#### Our IDC409 (Intro to DS and ML) course project on Event Type Classification of Belle II detector data (High Energy Physics)

The dataset provided to us consisted of different features and different event types (uubar, ddbar, ssbar, ccbar and bbbar). Our goal was to train a model using different features
available from the Belle II detector and try to reduce the features.

## I. Event Types and Binary Mapping

The original dataset contained **six event types**, each corresponding to a different kind of particle interaction observed in the Belle II detector.

| Reaction | Event type| Binary event type
|-------------|------------------|----------------
| $e^+ e^- \to \Upsilon(4S) \to B^+ B^-$ | 0 | **Signal (1)** 
| $e^+ e^- \to \Upsilon(4S) \to B^0 \bar{B}^0$ | 1 | **Signal (1)** 
| $e^+ e^- \to c \bar{c}$ | 2 | **Background (0)** 
| $e^+ e^- \to u \bar{u}$ | 3 | **Background (0)** 
| $e^+ e^- \to d \bar{d}$ | 4 | **Background (0)** 
| $e^+ e^- \to s \bar{s}$ | 5 | **Background (0)** 

---

### Binary Conversion Logic

To simplify the classification problem, we converted these six event types into **two broader categories**:

- **Signal events (1):** Event types `0` and `1` — corresponding to $B$ meson pair production  
- **Background events (0):** Event types `2`, `3`, `4`, and `5` — corresponding to other quark–antiquark interactions

This conversion helps simplify the model into a binary classification problem.

## II. Training and comparing different models
### Models used:

#### 1. Logistic Regression
- A simple linear model used as our baseline
#### 2. Support Vector Machine (SVM)
- Finds the best boundary (hyperplane) that separates the two classes
- Turned out to be computationally expensive
#### 3. Random Forest
- Uses multiple decision trees and combines their predictions
#### 4. XGBoost
- Builds trees one after another, learning from the mistakes of previous ones
- Improved accuracy compared to Random Forest
#### 5. LightGBM
- A faster and more memory-efficient version of gradient boosting.
- Grows trees leaf-by-leaf for better accuracy and speed on large data
- Best accuracy and AUC score

### Accuracy and ROC-AUC comparison of the various models
| Model                            |  Accuracy  |   ROC-AUC  |
| :------------------------------- | :--------: | :--------: |
| **1. Logistic Regression**          |   0.8430   |   0.9178   |
| **2. Support Vector Machine (SVM)** |   0.8626   |   0.9349   |
| **3. Random Forest**                |   0.8600   |   0.9322   |
| **4. XGBoost**                      |   0.8795   |   0.9467   |
| **5. LightGBM**                     | **0.8812** | **0.9491** |


## III. Feature reduction
To simplify the model and improve generalization, we applied two main feature reduction techniques:

### 1. Principal Component Analysis (PCA)
- PCA was performed on the standardized dataset to capture 95% of the total variance.
- This reduced the feature space from 48 original features to 23 principal components, significantly lowering dimensionality while retaining most of the information
- LightGBM model was  retrained on this reduced dataset to compare performance with the full feature set

### 2. Top Feature Selection (Feature Importance)
- Using the Decision Tree classifier, we identified the top 10 most important features for all decision tree models: Random forest, XGBoost and LightGBM
- LightGBM model trained only on these top features achieved comparable accuracy and AUC-ROC scores, indicating that much of the predictive power is concentrated in a small subset of features

## IV. Checking for overfitting in LightGBM Model:
- To ensure that the LightGBM model was not overfitting, we compared its performance on the training and testing datasets using metrics such as ROC-AUC and accuracy.
- The training AUC was slightly higher than the testing AUC, but the difference was within AUC gap < 0.05 telling us that the model generalizes pretty well to test data and is not overfitting to the training data

------------------------------------------------------------------------------------------------------------------------------------
A few useful resources we used along the way:
1. ROC and AUC: https://youtu.be/4jRBRDbJemM?si=UUH_TAnxRst2F5Gz
2. Logisitc regression: https://youtu.be/3bvM3NyMiE0?si=0s7nKj4lKTNxLGij
3. Decision tree classifier: https://youtu.be/ZVR2Way4nwQ?si=pSHpYpxlUSY9N9WL
4. Random forest: https://youtu.be/v6VJ2RO66Ag?si=PZx5oFGVM0kxr_ff
5. SVM: https://youtu.be/_YPScrckx28?si=dT2w_1x5WlxlBWS5
6. ML fundamentals—bias and variance: https://youtu.be/EuBBz3bI-aA?si=h7aiHohaC3RhJW44
7. https://medium.com/@jairiidriss/the-importance-of-feature-scaling-in-machine-learning-logistic-regression-for-example-b3068f8d3441
8. https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html
9. https://www.geeksforgeeks.org/machine-learning/radial-basis-function-kernel-machine-learning/
10. https://blog.dailydoseofds.com/p/how-to-inspect-decision-trees-after



thankyou:)



