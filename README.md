# ISA444_FinalProject
Hotel Demand Track 

Through this project, I implemented time-series cross-validation across a variety of models to explore their predictive power for hotel room demand. During the initial data preparation and visual exploration stage, I identified extreme cases where certain hotels experienced a complete demand flatline to or near zero in early-to-mid 2022. Considering these as outliers likely reflecting unique, non-recurring scenarios - such as hotel  closures - I decided to drop them from the dataset to prevent them from distorting model training. I also removed the target_year variable, as its information was already fully captured by the primary date variable (ds). Finally, I converted categorical variables into dummy variables, transforming qualitative text data into a numerical format that machine learning algorithms can mathematically interpret to map complex patterns.

Looking at the plotted series, even though I dropped those specific extreme outlier properties, I consider MAPE to be an inappropriate metric for this dataset. Several remaining properties still experience deep drops in demand close to zero, which mathematically breaks the metric. Additionally, MAPE is biased because it calculates error using a fraction that penalizes under-predictions much more severely than over-predictions. To avoid these distortions, I decided to rely on Mean Absolute Error (MAE) as my primary evaluation metric, which measures the average magnitude of errors by taking the absolute value, treating overprediction and underprediction with equal penalization regardless of the hotel's overall size. Furthermore, MAE is highly interpretable, as the resulting error is expressed directly in the same units as the target variable (daily room demand).

Moving into the model-fitting phase, I executed a 5-fold cross-validation to evaluate predictive accuracy across non-overlapping testing windows. Following cross-validation, I extracted the performance metrics for each model on a per-property basis and aggregated the evaluation dataframes to calculate the number of metric "wins" (values closest to 0) achieved by each model across the series. Interestingly, AutoArimaWPred and LGBM tied for the top performance, each achieving the lowest MAE on 6 hotel properties. This finding aligned with what I’ve learned through class, both models successfully incorporate exogenous covariates. This highlights how external predictors - beyond just the baseline identifiers of unique_id, y, and ds - significantly enhance a model's predictive capabilities, capturing vital demand drivers like seasonality, day-of-week effects, etc. Ultimately, I selected the LGBM model for final testing due to its superior processing speed, scalability, and capacity to handle complex feature structures. While AutoARIMA accommodates covariates, LGBM seamlessly leverages both external covariates and high-dimensional lag variables, while also offering the advantage of automated feature selection to figure out which variables matter most.

## Note to Professor Fadel
Thank you so much for your guidance, encouragement, and understanding regarding my class absences throughout this semester. I deeply appreciate your willingness to support me and provide assistance given my circumstances. I hope to keep in touch!

## 📊 Project Notebooks & Deliverables

### 🗂️ Data Preparation & Cross-Validation Pipelines
* 📓 [Data Preparation, Baseline, StatsForecast, and LGBM Models Pipeline][(DataPrep_Baseline_StatsForecasts_LGBM_Project.ipynb)](https://colab.research.google.com/drive/1B3C3ozGHq9MKRmQrRxqDcFQe5b3sApWa?usp=sharing)
* 📓 [AutoNBEATS Model Pipeline](AutoNBEATS_Project.ipynb)
* 📓 [AutoNHITS Model Pipeline](AutoNHITS_Project.ipynb)
* 📓 [TimeCoPilot Model Pipeline](TCF_Project.ipynb)
* 📓 [Bonus - TabPFN Model Pipeline](Bonus_TabPFN_Project.ipynb)

### 📌 Model Selection
* 📓 [Selecting the Best Model](Selecting_BestModel_Project.ipynb)

### 📈 Final Testing & Visualizations
* 📓 [Forecasting with the Selected Best Model (LGBM)](FinalForecast_LGBM_Project.ipynb)
* 🖼️ [Final Forecast Plots vs. Actuals](FinalForecast_Plots_vs_Actuals.png)

### 📄 Required Evaluation Outputs (CSVs)
* 📄 [Baseline (No Predictors) Evaluation](baseline_no_pred_eval.csv)
* 📄 [Baseline (With Predictors) Evaluation](baseline_w_pred_eval.csv)
* 📄 [LightGBM Evaluation Results](eval_lgb.csv)
* 📄 [AutoNBEATS Evaluation Results](eval_autonbeats_1.csv)
* 📄 [AutoNHITS Evaluation Results](eval_autonhits_1.csv)
* 📄 [TimeCoPilot Evaluation Results](eval_tcf_1.csv)
* 📄 [TabPFN Evaluation Results](eval_tabpfn_1.csv)
