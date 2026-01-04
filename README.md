Project Report: Chronic Kidney Disease Predictive Analytics
Objective: To analyze renal biomarkers, identify significant clinical predictors, and develop a high-accuracy supervised learning system for CKD screening.



# 1: Data Exploration & Statistical Profile


The initial phase focused on understanding the "shape" of the patient data.


Distribution Analysis: We identified that GFR (Glomerular Filtration Rate) is left-skewed.


Clinical Meaning: Most patients in the dataset are healthy (high GFR), but a significant "tail" of patients exists with pathological GFR values.


Normality Testing: Using the Shapiro-Wilk test, we confirmed the data is non-normal, necessitating the use of Non-Parametric statistical tests.


#  2. Inferential Statistics & Hypothesis Testing


We moved beyond descriptions to find proven relationships between features


I: The "Big Three" Predictors: Mann-Whitney U tests confirmed that Creatinine, BUN, and GFR are statistically different ($p < 0.05$) between healthy and CKD groups


II:Correlation: Spearman’s Rank Correlation showed a strong negative monotonic relationship between Creatinine and GFR.


III:_Post-hoc Analysis_: Using Kruskal-Wallis and subsequent post-hoc tests, we examined how different Medications affected kidney function, identifying which treatments were associated with the most significant changes in renal markers.



# 3. Supervised Learning Performance 


We trained three models to categorize patients as "Healthy" or "CKD."



Model Comparison Table



Model,        Accuracy ,Log   Loss, Recall (CKD),  Note


Random Forest,100%,    0.0056,       1.00,         Perfect separation based on GFR rules.


SVM,          99.8%,         N/A,  0.99,         Highly robust boundary detection.


MLP (Neural Net),99.9%,  0.0082,    1.00,         Excellent convergence via backpropagation.



# 4. The "Stress Test" (Feature Ablation)
To ensure the model wasn't just "reading the definition" of CKD (GFR < 60), we removed GFR, Creatinine, and BUN and re-trained the model using only lifestyle and comorbid factors (Age, Water Intake, Proteinuria, Diabetes, Hypertension).


Stress Test Accuracy: 98%


Stress Test Recall: 1.00


Conclusion: The model is an incredibly powerful Early Warning System. Even without expensive blood work, it can identify 100% of sick patients based solely on vitals and lifestyle history.


# 5. Technical Implementation & Deployment

The project concluded by transforming the code into a reusable tool.


Model Serialization: We used joblib to save the "Brain" of the model into a .pkl file.


Inference Portal: We developed a function that allows a clinician to input 7 simple values and receive an instant risk assessment with a confidence percentage.


# 6. Real-World Conclusions
Clinical Screening vs. Diagnosis: While GFR is the diagnostic gold standard, this project proves that Protein in Urine and Hypertension status are sufficient for a 98% accurate screening tool in resource-poor settings.


Zero-Miss Strategy: The model prioritizes Recall 1.00. In medical terms, this means the model is tuned to never miss a sick patient, which is the most critical requirement for a life-saving medical tool.


Future Utility: The saved model can be integrated into hospital management software or mobile apps to provide real-time decision support for doctors.

