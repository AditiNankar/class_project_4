# **Scope Report: Machine Learning Classification of Stars, Quasars, and Galaxies Using SDSS Data**

## **1. Project Overview**
This project aims to develop a machine learning model that accurately classifies **stars, quasars, and galaxies** using data from the **Sloan Digital Sky Survey (SDSS)**. By leveraging machine learning algorithms and data visualization techniques, we seek to identify key distinguishing features of these celestial objects. This contributes to astrophysical research and enhances automated classification methods.

Please follow steps to create sql database if you want to run the model.

## **2. Database Creation and Management**
### **Setting Up PostgreSQL Database**
1. Install **pgAdmin** or **PostgreSQL**.
2. Create a new database named **"StarsGalaxiesQuasars"**.
3. Open `schema.sql` in a query tab and execute it to create tables.
4. Import the dataset into `classification` and `observation` tables.
5. The database is now ready for machine learning model integration.

### **Database Connection**
- The code connects to a **PostgreSQL database** using **SQLAlchemy**.
- Data is retrieved by joining two tables:
  - **Observation**: Contains brightness measurements across five wavelengths (u, g, r, i, z).
  - **Classification**: Contains the object class (**STAR, GALAXY, or QSO**).

## **3. Data Acquisition and Features**
### **Data Source**
- **Sloan Digital Sky Survey (SDSS)**
- Dataset obtained from **Kaggle**, ensuring fair usage via an open API.

### **Key Features**
- **Photometric Magnitudes**: u, g, r, i, z bands
- **Redshift (z)**: Distance measurement indicator
- **Spatial Information**: Right Ascension (RA) and Declination (Dec)

## **4. Methodology**
### **Data Preprocessing**
- Removing unnecessary columns (e.g., observation ID, object ID, metadata)
- Encoding target variable (**STAR → 0, GALAXY → 1, QSO → 2**)
- Splitting dataset into **training (80%) and testing (20%)** sets
- Normalizing brightness values using **StandardScaler**

### **Machine Learning Models Used**
| Model | Accuracy |
|----------------------|---------|
| **Random Forest (RF)** | 94% |
| **Gradient Boosting (GB)** | 94% (after tuning) |
| **Logistic Regression (LR)** | 93.5% |
| **Support Vector Machine (SVM)** | **95.7% (Best Model)** |

### **Model Insights**
#### **Random Forest (RF)**
- A bagging ensemble model that trains multiple decision trees and averages their outputs.
- **Findings**:
  - Achieved **94% accuracy**.
  - Most important feature: **z-band (Infrared brightness)**.
  - Least important feature: **u-band (Ultraviolet brightness)**.

#### **Gradient Boosting (GB)**
- A boosting model that builds trees sequentially, improving the errors of the previous trees.
- **Findings**:
  - Initial accuracy: **88%**.
  - After **hyperparameter tuning**, accuracy improved to **94%**.

#### **Logistic Regression (LR)**
- A simple, fast linear model for classification.
- **Findings**:
  - Accuracy: **93.5%**.
  - Nearly as effective as complex models but computationally efficient.

#### **Support Vector Machine (SVM)**
- A classifier that finds the optimal boundary for separating classes.
- Used **SGDClassifier** for fast training and **SVC** for hyperparameter tuning.
- **Findings**:
  - Initial accuracy: **93.85%**.
  - After **hyperparameter tuning** (`C=10, kernel=rbf`), accuracy improved to **95.7%** (best-performing model).

### **Hyperparameter Tuning & Cross-Validation**
- **Why?** Improves model performance by optimizing parameter selection.
- **How?** Used **RandomizedSearchCV** to search for best hyperparameters.
- **Best Parameters Found:**
  - **Gradient Boosting**: `n_estimators=300, learning_rate=0.2, max_depth=7` → 94% accuracy
  - **SVM**: `C=10, kernel=rbf` → **95.7% accuracy**
- **5-Fold Cross-Validation** applied for model robustness.

### **Exploratory Data Analysis (EDA) & Visualization**
- **Matplotlib & Seaborn** for data trends and distribution insights.
- **PCA for Dimensionality Reduction** (used for visualization, not model training).
- **Tableau Dashboards** for interactive classification analysis.

## **5. Key Questions for Tableau Analysis**
1. What photometric features best distinguish between stars, quasars, and galaxies?
2. How does redshift distribution vary among these celestial objects?
3. Which spectral characteristics contribute most to accurate classification?
4. Are there spatial clustering patterns in their distribution?
5. How does classification accuracy change with different feature selection techniques?

## **6. Challenges and Solutions**
| Challenge | Solution |
|----------------------|---------|
| **Class Imbalance** | Applied **SMOTE** (Synthetic Minority Over-sampling) to balance dataset. |
| **Feature Selection** | Removed redundant features and applied PCA for efficiency. |
| **Hyperparameter Tuning** | Used **Grid Search & Randomized Search CV** for optimal results. |
| **Data Quality Issues** | Performed extensive **data cleaning and normalization**. |

## **7. Expected Outcomes**
- A machine learning model capable of effectively classifying celestial objects.
- Identification of key features that differentiate **stars, quasars, and galaxies**.
- Visual tools providing insightful representations of **SDSS data trends**.

## **8. Tools and Technologies**
- **Machine Learning**: Scikit-learn
- **Data Processing**: Pandas, NumPy, PostgreSQL
- **Visualization**: Matplotlib, Seaborn, Tableau
- **Database**: PostgreSQL with pgAdmin
- **Data Source**: Sloan Digital Sky Survey (SDSS)

## **9. Conclusion**
This project integrates machine learning with astrophysical research to improve the classification of celestial objects. By identifying key distinguishing features and leveraging data visualization tools, we enhance the accuracy of automated classification methods. The findings can contribute to **astronomical research, automated object detection, and space exploration advancements**.

### **Final Recommendation**
- Use **SVM with RBF Kernel** for the best classification performance.
- Consider additional **feature engineering** (e.g., incorporating object size, shape, or additional spectral properties).

