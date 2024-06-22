# Module_14_Challenge

# Initial Analysis

![image info](cumulative_rtrn.png)

This strategy simply bought when the closing prices increased (ie: daily return was positive), sold when the closing price decreased (ie: daily return was negative), and held if there was no change to closing price.

Overall, the cumulative return has a negative trend.  This is not a good trend.

And I'd like to to point out that the strategy actually looks better if you do the exact opposite (sell when closing prices increase; buy when they decrease):

![image info](oppo_cumulative_rtrn.png)

However that was not part of the assignment, was just for my own idle curiosity

# Support Vector Machine - Baseline

Now we start looking at SVM, using the the Fast (4 day) and Slow (100 day) moving averages.  This is our baseline strategy.  We break off the moving averages so that we're working with just date and moving averages, break the moving averages into two groups (training and testing) based on date, scale the moving averages, then feed the training data into the SVM model.  (Training was based on April 2, 2015 - July 2, 2015; Testing was July 6 2015 - January 21 2021.)  Once we've trained the model, we apply test testing data, to generate predictions for buy and sell indicators.

Comparing the two, the SVM model closely followed the actual returns.  However, looking at the classification report:

              precision    recall  f1-score   support

        -1.0       0.43      0.04      0.07      1804
         1.0       0.56      0.96      0.71      2288

    accuracy                           0.55      4092
   macro avg       0.49      0.50      0.39      4092
weighted avg       0.50      0.55      0.43      4092

the model overall did fairly poorly and predicting the buy and sell signals, and the low F1 scores do not provide a high confidence in the model.

![image info](actual_vs_svm_cum_returns_3_mos.png)


# First Tuning - change months of training data

First tuning was to use the original data, but change the amount of training data from 3 months to 6 months.  This yields the following classification report:


              precision    recall  f1-score   support

        -1.0       0.44      0.02      0.04      1732
         1.0       0.56      0.98      0.71      2211

    accuracy                           0.56      3943
   macro avg       0.50      0.50      0.38      3943
weighted avg       0.51      0.56      0.42      3943

and graph:

![image info](actual_vs_svm_cum_returns_6_mos.png)


Overall I would say there isn't a huge improvement from using 3 months of data to 6 months.  Using the 6 months training data, the returns were actually lower in the 2019/2020 timeframe, although later in 2021 the returns were higher compared to both 3 month and actual.

# Second Tuning - change months of training data



