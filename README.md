**Exoplanet Exploration**

1. Preprocessing

   - Clean data

     - Drop the null columns where all values are null.

     - Drop the null rows.

   - Create a train/test split

     - Label (Y): koi_disposition.
     - Features (X): all other variables in other remaining columns.

   - Scale the data using the MinMaxScaler to scale features to fit  X_train and tranfrom X-train and X_test.  Why?

2. Tune-Model-Parameters

   There are two classifiers in this exploration:

   - Support Vector Machine Linear Classifier
     - Training Data Score: 0.847919426654467
     - Testing Data Score: 0.862946020128088	
     - SVC(C=1.0, cache_size=200, class_weight=None, coef0=0.0,
           decision_function_shape='ovr', degree=3, gamma='auto_deprecated',
           kernel='linear', max_iter=-1, probability=False, random_state=None,
           shrinking=True, tol=0.001, verbose=False)

   - Hyperparameter Tuning (GridSearch CV model)
     - Best parameter: C=10, gamma=0.0001
     - Best score: 0.8690149435803599

3. Evaluate-Model-Performance

   SVM classification  report

   ```
                  precision    recall  f1-score   support
   
        CANDIDATE       0.37      0.24      0.29       528
        CONFIRMED       0.19      0.15      0.17       568
   FALSE POSITIVE       0.67      0.86      0.75      1090
   
         accuracy                           0.53      2186
        macro avg       0.41      0.42      0.40      2186
     weighted avg       0.47      0.53      0.49      2186
   ```

   Grid Search classification report

   ```
                   precision    recall  f1-score   support
   
        CANDIDATE       0.32      0.24      0.28       528
        CONFIRMED       0.23      0.23      0.23       568
   FALSE POSITIVE       0.70      0.77      0.73      1090
   
         accuracy                           0.50      2186
        macro avg       0.41      0.41      0.41      2186
     weighted avg       0.48      0.50      0.49      2186
   ```

   SVM model provided 3% slightly better accuracy over the Grid Search model.  The accuracy rate, however is quite low within the low range of the 50th percentile.  False positive are also very high, 67% for the SVM model and 70% for the Grid Search model.  Again the SVM does slightly better.  In addition, the best parameters for the Grid Search model are quite constrained with high C = 10 (versus 1 for the SVM model) and low gamma = .0001.  On the other hand, the SVM gamma is unspecified.  This may be an issue given that its function is polynomial, not linear (degree = 3).

   In summary, these models need revisions of features to improve the accuracy.  Meanwhile, other classifiers of machine learning may be explored as well.