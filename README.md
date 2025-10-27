# IDC409_DS_Project

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

## Checking for overfitting in LightGBM Model 
## III. Feature reduction

