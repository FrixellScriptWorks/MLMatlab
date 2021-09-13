# Gamma Spectrum Classification with Decision Tree Classifier

Gamma spectrum, by its shape, has a unique feature with each isotope. It can be a noted one from 'peak spectrum' or even the whole spectrum should be different. Hence, we can use statistical method to process and classified one another with machine learning. This time is with Decision Tree Classifier.

Decision Tree Classifier asking the datasets feature if it can passed to the branching parameter (a constant or binary yesno). The branch will make another branch until the feature splitted with purest [gini impurity](https://en.wikipedia.org/wiki/Gini_coefficient). Eventually, making it looks like a tree. When a tree has been made, the classifier will sends new data and insert it which branch the data approximated to be true.

### Methods and Results
- Data Preparation
All spectrum is recorded and obtained manually, so this is special. (Datasets available)
Data recorded with scintillator Leybold Didactic and calibrated under Cassy Lab application. Scintillator formatted as:
  - Multichannel: On
  - Gain Box: -2
  - Negative Pulses: On
  - Voltage: 676 V (with external power supply)
  - Channel: 512 Channel (5.9 keV/Channel)
  - Time: 50 seconds (training) / 80 seconds (test)
  - Total Data: 200 data training of Co60, Na22, Am241, Cs137, Sr90 (total: 1000) / 15 data test for each (total: 75)

Before continuing, I'll tell my PC specification to compare if others might be faster or slower. This can affect the processing time too.
Specifications:
  - CPU: Intel Core i3-5005U
  - GPU: (Integrated: Intel HD Graphic 550) (Dedicated: NVIDIA GeForce 930M)
  - HDD: Toshiba MQ01ABF050 5400 RPM
  - RAM: DDR3 4x2 GB SODIMM 1600 MHz

- Transposing
As sklearn classifiers cannot process classes within X-plane, so the table is transposed first.
  - Before Transpose
    - ![Before Transpose](https://user-images.githubusercontent.com/66581100/133018157-f1d7499e-7d17-4706-b55c-ce235f6ca4ee.png)
  - After Transpose
    - ![After Transpose](https://user-images.githubusercontent.com/66581100/133018212-1e5f3074-93f6-4e57-bab0-712b4b14e200.png)

- Parameters
To increase the view of the progress of training data, I manipulated the parameter max_depth within the classifier function to 1 until 9. You can see the documentation[here](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn.tree.DecisionTreeClassifier)

- Training and Test
A splitting data is done before the training process to validate the data after training (like a pre-test). The ratio I use is 90%/10% with random values = 4. I don't use any complicated methods.
  - ![Splitting](https://user-images.githubusercontent.com/66581100/133018909-a6647191-f46b-46e8-8b05-6709edb995c9.png)

After that, the training begin with DecisionTreeClassifier(*parameters*) function as dtc. Next, fit the data with dtc.fit(X_train, Y_train).
See the X and Y? The X is datum features, and Y is Datum.

Next, validate the trained DTC using 10% of splitted data before. When the process is iterated many times, I will use only the test data last iteration to make the confusion matrix and reports. Else, I will only use the accuracy percentage and deviation errors. this can save more time needed to prepare.

Validation accuracy dtc: (37%, 56%, 78%, 100%, 100%, 100%, 100%, 100%, 100%)
Deviation errors: (0%, 0%, 0.3%, 0.4%, 0.3%, 0%, 0.6%, 0%) deviation calculated using normalization on errors occurs.

  - Validation Graph
    - ![Graph 1](https://user-images.githubusercontent.com/66581100/133020424-9fa109f6-f6d0-44ca-9a74-95f6ab9e69d9.png)

Test accuracy dtc: (40%, 60%, 77%, 94%, 80%, 80%, 80%, 92%, 96%)
Deviation errors: (0%, 5.86%, 5.96%, 9.50%, 7.48%, 9.01%, 7.53%, 10.46%, 11.81%)

  - Test Graph
    - ![Graph 2](https://user-images.githubusercontent.com/66581100/133020813-464b0dfc-50d0-49cc-a4f0-744372bd244a.png)

Finally, the confusion matrix reports:
  - ![Confusion Matrix](https://user-images.githubusercontent.com/66581100/133020882-9165de7b-d4de-41d8-91d6-45942571eb7e.png)
  - ![Cm Reports](https://user-images.githubusercontent.com/66581100/133020937-967979db-6721-422c-ac83-71b5b14fc5fd.png)

Processing time: 6.75 seconds

If we can look at the reports, it's looks pretty good accuracy with overall f1-score is at 99%. Combined with processing time, we can say that the decision tree classifier can be used as gamma spectrum classification with **decent accuracy (99%)** at **max_depth = 9** with processing time about **6.75 seconds**.

