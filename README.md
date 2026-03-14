# Tanzania Tourism Prediction

[![Zindi Challenge](https://img.shields.io/badge/Zindi-Challenge-blue)](https://zindi.africa/competitions/tanzania-tourism-prediction)
[![Python 3](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=flat&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![CatBoost](https://img.shields.io/badge/CatBoost-FF9900.svg?style=flat)](https://catboost.ai/)
[![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)

## Overview
The Tanzanian tourism sector plays a significant role in the Tanzanian economy, contributing about 17% to the country’s GDP and 25% of all foreign exchange revenues. The sector, which provides direct employment for more than 600,000 people and up to 2 million people indirectly, generated approximately $2.4 billion in 2018 according to government statistics. Tanzania received a record 1.1 million international visitor arrivals in 2014, mostly from Europe, the US, and Africa.

Tanzania is the only country in the world that has allocated more than 25% of its total area for wildlife, national parks, and protected areas. Its famous attractions include the Serengeti plains, the Ngorongoro Crater, Mount Kilimanjaro, and the Mafia Island marine park.

**This project was developed as a solution to the [Tanzania Tourism Prediction](https://zindi.africa/competitions/tanzania-tourism-prediction) challenge on Zindi.**

## Objective
The primary objective of this project is to develop a machine learning model to **predict how much money a tourist will spend when visiting Tanzania**. This predictive model aims to assist tour operators and the Tanzania Tourism Board in automatically helping tourists across the world estimate their expenditure before visiting Tanzania.

## Evaluation
The evaluation metric for this competition is the **Mean Absolute Error (MAE)**. 
For every row in the dataset, the model correctly outputs the target variable `total_cost`.

Example submission format:
```csv
test_id,total_cost
tour_6322,65000
tour_1153,11000
```

## Project Structure

```text
Tanzania-Tourism-Prediction/
├── 01_baseline_modeling.ipynb          # Initial Data Exploration, Baseline Models, and Feature Engineering
├── 02_advanced_modeling_catboost.ipynb # Refined modeling (CatBoost) and final inference generation
└── README.md                           # Project documentation
```

## Methodology & Algorithms Used

Throughout the project, several machine learning methodologies were applied and evaluated to find the best-performing model for predicting tourist expenditure.

**1. Data Preprocessing & Feature Engineering:**
- Handling missing values and encoding categorical variables using [`LabelEncoder`](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html).
- Extracting meaningful features from dates, durations, and geographical data.
- Splitting data using [`train_test_split`](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html) for robust local validation.

**2. Baseline Modeling (`01_baseline_modeling.ipynb`):**
To establish a performance benchmark, several standard regression algorithms from `scikit-learn` were evaluated:
- **Linear Models:** [Linear Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html) ([Wiki](https://en.wikipedia.org/wiki/Linear_regression)), [Ridge Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html) ([Wiki](https://en.wikipedia.org/wiki/Ridge_regression)), [Lasso](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Lasso.html) ([Wiki](https://en.wikipedia.org/wiki/Lasso_(statistics)))
- **Tree-Based Models:** [Decision Tree Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html) ([Wiki](https://en.wikipedia.org/wiki/Decision_tree_learning)), [Random Forest Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html) ([Wiki](https://en.wikipedia.org/wiki/Random_forest))
- **Boosting Algorithms:** [Gradient Boosting Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html) ([Wiki](https://en.wikipedia.org/wiki/Gradient_boosting))
- **Other Approaches:** [Support Vector Regression (SVR)](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVR.html) ([Wiki](https://en.wikipedia.org/wiki/Support-vector_machine#Regression)), [K-Nearest Neighbors (KNN)](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsRegressor.html) ([Wiki](https://en.wikipedia.org/wiki/K-nearest_neighbor_algorithm)), [Multi-Layer Perceptron (MLP Regressor)](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPRegressor.html) ([Wiki](https://en.wikipedia.org/wiki/Multilayer_perceptron))

**3. Advanced Modeling (`02_advanced_modeling_catboost.ipynb`):**
After evaluating the baselines (which were primarily assessed on MSE and R2 metrics), the focus shifted to more advanced gradient boosting techniques that handle categorical features natively to directly optimize the competition's MAE metric.
- **[CatBoostRegressor](https://catboost.ai/en/docs/concepts/python-reference_catboostregressor) ([Wiki](https://en.wikipedia.org/wiki/CatBoost)):** Chosen for its superior handling of the categorical nature of tourism survey responses without extensive one-hot encoding.
  - **Ensemble Strategy & Hyperparameters:** Rather than relying on a single model, an ensemble approach was taken. Ten separate `CatBoostRegressor` models were trained with varying tree depths (`depth` = 0 to 9) and the final predictions were averaged. 
  - **Shared Parameters:** `iterations=1000`, `loss_function='MAE'`, and `logging_level='Silent'`.
  - **🏆 Final Performance:** The optimized CatBoost ensemble achieved a **Validation Mean Absolute Error (MAE) of ~3,835,241 TZS** (Tanzanian Shillings), delivering the best performance on the leaderboard and significantly improving upon the traditional baselines.

## Technologies & Libraries Used
- **Language**: [Python 3](https://www.python.org/)
- **Data Manipulation**: [`pandas`](https://pandas.pydata.org/), [`numpy`](https://numpy.org/)
- **Data Visualization**: [`matplotlib`](https://matplotlib.org/), [`seaborn`](https://seaborn.pydata.org/), [`plotly`](https://plotly.com/python/)
- **Machine Learning**: [`scikit-learn`](https://scikit-learn.org/), [`catboost`](https://catboost.ai/)

## How to Run the Project
1. **Clone this repository** to your local machine:
   ```bash
   git clone https://github.com/your-username/Tanzania-Tourism-Prediction.git
   cd Tanzania-Tourism-Prediction
   ```
2. **Install the required dependencies**:
   ```bash
   pip install pandas numpy scikit-learn catboost matplotlib seaborn plotly
   ```
3. **Launch the Jupyter Notebooks**:
   - Begin with `01_baseline_modeling.ipynb` to understand the data processing and baseline benchmarks.
   - Or proceed to `02_advanced_modeling_catboost.ipynb` for the advanced feature pipeline.

## Acknowledgments
- Thank you to **Zindi Ambassador Davis David** for creating this competition.
- Data and challenge hosting provided by the **[Zindi Africa](https://zindi.africa/)** platform.

## What I Learned & What Improved the Process
Throughout the development of this predictive model, several key iterations drastically improved the final results:
- **Categorical Data Handling (The Biggest Improvement):** Survey data is notoriously high in cardinality (e.g., thousands of different user responses for locations, agencies, etc.). I discovered that relying on traditional algorithms with one-hot encoding resulted in highly sparse data, hurting performance. Switching to **CatBoost**, which intrinsically handles categoricals, was the single biggest improvement in the process.
- **Targeting the Right Metric:** Early baseline models relied on R2 and Mean Squared Error (MSE), which overly penalized outliers. Shifting the optimization landscape strictly to **Mean Absolute Error (MAE)** aligned the model perfectly with the Zindi evaluation criteria, dropping the error down to **~3.83M TZS**.
- **Model Evaluation:** Deepened my understanding of how MAE interprets real-world financial cost differences compared to other metrics like RMSE.
- **Real-World Application:** Gained practical experience applying machine learning to real-world socio-economic data to solve a concrete business problem for the tourism industry.
