# Disease-Classification
The piece of code builds a classification model to detect the prescence of a rare disease given a set of patient parameters. The model is constructed using a declassified patient feature set is cleaned and processed. One unique issue addressed with this dataset is the problem of data imbalance. Since the records contain more data about patients without the disease there is a chance that the model may lack the sensitivity to detect the disease if the unprocessed data is used. A number of common techniques to solve this problem are explored in the model before constructing the classifier

## Data Uploading and Preprocessing
• The data after being read into the program is removed of NULL values  
• The heatmap was plotted to observe collinearity between the predictors
Heatmap
No serious cases of multi-collinearity was observed so we leave the data intact.  
• For fitting the models, dummies columns are created for the values in all categorical columns  
\# of new columns created per categorical column = No. of Values in categorical column – 1

## Train Test Split
• The entire dataset is divided into train and test sets
train-test snippet
• The train data is used to build different models and the test data is used to gauge the
performance of the models

## Upsampling to rectify imbalance in classes
• Upon analyzing the counts of the two classes (-1 and 1) an imbalance is observed
• The minority class of the training data is upsampled using the resample feature to get a
balanced dataset to train the models
• The values of x and y are extracted from this upsampled train data

## Model Comparison and Selection
• To select the best model different popular classifiers are used (without any parameter
tuning) to fit the balanced training data and predict the test data set aside in the Train
Test Split phase
• The different classifiers considered are:
Instance of steps used for each model to extract the metrics
• The models are gauged based on their overall prediction accuracy, prediction accuracy
of each class and their variance of prediction. The results are tabulated below:
• Based on these results the Radial SVM, Logistic Regression and Random Forest models
are chosen for tuning.

## Hyperparameter tuning:
## SVC
• Grid Search is used to pick the best parameters from a set of parameter options
provided:
• This model is used to predict the test set data. From the predicted values the prediction
accuracy and confidence intervals are calculated:
It can be seen that the model does not correctly predict any instance of the second
class, so it is ignored.

## Random Forest
• Grid Search is used to pick the best parameters from a set of parameter options
provided:
• The metrics for this model on predicting the test set are as follows:

## Logistic Regression
• Grid Search is used to pick the best parameters from a set of parameter options
provided:

Prediction Error for each class:
• Comparing the metrics for the Random Forest model and the Logistic Regression model
it can be seen that the overall accuracy for the latter is higher (although the
performance considering the prediction accuracy for each class is the same for both the
models).
• Hence, the Logistic Regression model is chosen as the best model to fit the test data

## Manual Tuning
• The C parameter of the Logistic Regression model is further tuned around the range
suggested by the grid search model to further improve its performance:
• The best C parameter is chosen from the results and other parameters suggested by the
grid search are used to build and gauge the performance of the model:

## Building the Final Model
• Now that the best model and its range of parameters are known, the model is again fit
using grid search with the entire dataset (upsampled to balance the minority class).
• The best parameters for the chosen Logistic Regression model are as follows:

## Fitting the test data
• Upon loading the test data and encoding the categorical columns it was observed that
some of the columns in the training data was missing in the test data because some of
the columns in the test data did not have as many values as the ones in the training
data. For instance the X5 column in the training data had 5 values (A,B, C, D and E)
whereas the same column in the testing data just had 3 (A, C and E).
• For each such missing value a new column was introduced in the testing data prefilled
with zero values

• The final model built on the entire dataset is used to predict the test data provided
