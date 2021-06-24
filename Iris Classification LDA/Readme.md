# Iris Classification with Linear Discriminant Analysis
> Classic, but this is where the starting step happens. Like the 'Hello World!' program.

Iris flower can be classified into 3 species (Setosa, Versicolor, and Virginica). It can be looked at its Sepal and Petal, which has significant differencies in size. With size, it's means number. It can be calculated with quantitative statistical methods, in this case is Linear Discriminant Analysis (LDA).

Linear Discriminant Analysis is used in ML's algorithm as supervised learning. Data that trained must be well labeled in order to predict the new test data into their sets of label, called classes. LDA can be used to predict data with binary classes or multiclass, it's versatile. LDA will find the linear combination of features observated that characterizes or separates two or more classes of objects or events (i.e. iris classification).

### Methods and Results

- Data Preparation

This including removing missing values. Because I want to make a scatter graph with predicted data, but raised an error with missing value.
The table read from Excel and converted into 'double' data type from 'string' so it can be calculated freely.
   - Before (String value automatically set by Matlab readtable function)
     - ![Before dataprep](https://user-images.githubusercontent.com/66581100/123330928-d44c0900-d568-11eb-8688-6eed33a1c58b.png)
   - After (Converted and removed missing values. No header)
     - ![After dataprep](https://user-images.githubusercontent.com/66581100/123331431-7cfa6880-d569-11eb-90da-321c3b3425d0.png)

- Data Training and Test
To train data, I use fitdiscr() function and train all data from training datasets. I didn't split data for validation, I choose to re-predict all data again to validate.
In result, this gave me 

Loss = 0.0163. 

where: Loss = fraction of missclassified data.

  - Confusion Matrix of Validation
    - ![CMVal](https://user-images.githubusercontent.com/66581100/123334164-e465e780-d56c-11eb-9c75-7bc3f8e5f7d9.png)
  - Bad predicted value in validation (Sepal Edition) 
    - ![BadSepal](https://user-images.githubusercontent.com/66581100/123334297-12e3c280-d56d-11eb-8f31-58a65a28d42d.png)
  - Bad predicted value in validation (Petal Edition)
    - ![BadPetal](https://user-images.githubusercontent.com/66581100/123334351-2b53dd00-d56d-11eb-9117-eb22417fa314.png)
  - (NB: Graph separated into 2, there's no 4-dimensional graph)


Next, test the trained data to predict new datasets without label.
- ![All in test](https://user-images.githubusercontent.com/66581100/123332172-5ee13800-d56a-11eb-95de-688352c35a6a.png)

From the test above, now I have score which determine class picked by samples.
- ![Score](https://user-images.githubusercontent.com/66581100/123338626-622cf180-d573-11eb-933e-66e2bdc8858e.png)

Where score is valued from 0 - 1. The more score it has, the more classifier tend to pick the class.
Here the result class chosen by all test data:
- ![Result test](https://user-images.githubusercontent.com/66581100/123339044-1169c880-d574-11eb-92ab-6ddd76fc20c6.png)

The number above means frequency chosen by the classifier for the corresponding classes. Total frequency is the total of test data.
I cannot make Bad Prediction graph and Confusion Matrix of the test data because there's no true class of test data provided. Hence I didn't know error rates of test prediction.
