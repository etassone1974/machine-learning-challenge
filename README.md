# machine-learning-challenge
## Machine Learning Homework - Exoplanet Exploration

### Create a README that reports a comparison of each model's performance as well as a summary about your findings and any assumptions you can make based on your model (is your model good enough to predict new exoplanets? Why or why not? What would make your model be better at predicting new exoplanets?).

## Assumptions and Limitations
Due to the complexity of the features and lack of domain knowledge, it was difficult to reduce the number of features with any degree of confidence.  They already appeared to have been reduced from the data available on the website.  The Support Vector Machine classifier was tried twice, once with the full set of features from the CSV data file, and once with selectively reduced features.  The features that were eliminated were the error columns and the koi_tce_plnt_num (planet number).  The other classifiers were all built with the set of features given in the dataset.

## Model Comparisons
There were six models created to train and test the exoplanet data.  They were a Support Vector Machine, a Support Vector Machine with reduced dimensionality, Decision Tree, k-Nearest Neighbour, Logistic Regression and Random Forest classifiers.  Both SVMs, k-NN and Logistic Regression models had their parameters tuned with GridSearchCV.  Following is a list of the accuracy of the models on both testing and training data, and also accuracy with regards to test data if GridSearchCV was used to tune parameters.  The confusion matrices and classification reports can be seen in each individual Jupyter notebook.  (Note that the Decision Tree and Random Forest classifiers will always produce 100% accuracy for the training data due to the nature of their algorithms.)

    * Format: Training / Testing / Testing after GridSearchCV (all percentages)
    1. SVM Model 1 -- 84.6 / 84.2 / 87.9
    2. SVM Model 2 (reduced features) -- 81.1 / 79.9 / 80.6
    3. Decision Tree -- 100 / 85
    4. k-NN -- Training - 83.6 / 82.4 / 84.1
    5. Logistic Regression -- 85.1 / 84.3 / 86.5
    6. Random Forest -- 100 / 89.2

Based on the accuracy scores above, the models in order of best performed to worst performed are:
1. Random Forest
2. SVM Model 1
3. Logistic Regression
4. Decision Tree
5. k-NN
6. SVM Model 2 (reduced features)

It should be noted that the accuracy scores are quite close, particularly in the case of the first five classifiers.  The only model with notably worse performance is the second SVM model.  Examining the confusion matrices, precision, recall and f-scores for the models largely confirms the ordering of the models in terms of performance.  However, it is obvious that the classifiers perform the best in distinguishing FALSE POSITIVE exoplanet samples, rather than CANIDATE or CONFIRMED exoplanet samples.  Precision, recall and accuracy for the FALSE POSITIVE set is very high across all models, but does drop significantly when used for CANDIDATE and CONFIRMED exoplanets.  The Decision Tree and Random Forest classifiers also provide a listing of the relative importance of each feature in classification.  Both models list the features 'koi_fpflag_nt', 'koi_fpflag_co', 'koi_fpflag_ss', 'koi_model_snr' as the top four in determining classification of data points.  With the large number of features, these models also demonstrate that some features only have a small impact on the classification of data.  This may suggest that more efficient models could be built by eliminating less important features, which should be possible with more domain knowledge.

## Summary
All six models built to train and test the dataset provided an accuracy of approximately 80% or greater, including the SVM that reduced the number of features from 40 to 19.  The models are all much more accurate in determining FALSE POSITIVE data points, rather than either CANDIDATE OR CONFIRMED exoplanets.  This is explained by the fact that there are almost double the amount of FALSE POSITIVE samples in the dataset, as opposed to the other two categories.  Hence the classifiers have become much better at recognising a FALSE POSITIVE rather than other potential or confirmed exoplanets.  This makes the classifiers much less useful in predicting new exoplanets given further data points, as they are essentially much more ruling out possible exoplanets rather than determining new ones.  Many more samples of CANDIDATE and CONFIRMED exoplanet data to build the models would result in more balanced classifiers, to more accurately find more possible and confirmed exoplanets.