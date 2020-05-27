# Activity Recognition system based on Multisensor data fusion (AReM)

## **Task:**
An interesting task in machine learning is classification of time series. In this problem,
I will classify the activities of humans based on time series obtained by a Wireless
Sensor Network.

## **Dataset details**
The dataset contains 7 folders that represent seven types of activities. In
each folder, there are multiple files each of which represents an instant of a human
performing an activity.1 Each file containis 6 time series collected from activities
of the same person, which are called avg rss12, var rss12, avg rss13, var rss13,
vg rss23, and ar rss23. There are 88 instances in the dataset, each of which contains 6 time series and each time series has 480 consecutive values.


## **Data Set Information:**

This dataset represents a real-life benchmark in the area of Activity Recognition applications, as described in [1].
The classification tasks consist in predicting the activity performed by the user from time-series generated by a Wireless Sensor Network (WSN), according to the EvAAL competition technical annex ([Web Link]).

In our activity recognition system we use information coming the implicit alteration of the wireless channel due to the movements of the user. The devices measure the RSS of the beacon packets they exchange among themselves in the WSN [2].

We collect RSS data using IRIS nodes embedding a Chipcon AT86RF230 radio subsystem that implements the IEEE 802.15.4 standard and programmed with a TinyOS firmware. They are placed on the userâ€™s chest and ankles. For the purpose of communications, the beacon packets are exchanged by using a simple virtual token protocol that completes its execution in a time slot of 50 milliseconds. A modified version of the Spin token-passing protocol is used to schedule node transmission, in order to prevent packet collisions and maintain high data collection rate. When an anchor is transmitting, all other anchors receive the packet and perform the RSS measurements. The payload of the transmitting packet is the set of RSS values between the transmitting node and the other sensors sampled during the previous cycle.

From the raw data we extract time-domain features to compress the time series and slightly remove noise and correlations.

We choose an epoch time of 250 milliseconds according to the EVAAL technical annex. In such a time slot we elaborate 5 samples of RSS (sampled at 20 Hz) for each of the three couples of WSN nodes (i.e. Chest-Right Ankle, Chest-Left Ankle, Right Ankle-Left Ankle). The features include the mean value and standard deviation for each reciprocal RSS reading from worn WSN sensors.

For each activity 15 temporal sequences of input RSS data are present. The dataset contains 480 sequences, for a total number of 42240 instances.

We also consider two kind of 

activity, illustrated in the figure provided (bendingTupe.pdf). The positions of sensor nodes with the related identifiers are shown in figure sensorsPlacement.pdf.

## **Attribute Information:**

For each sequence, data is provided in comma separated value (csv) format.

**- Input data:**
Input RSS streams are provided in files named datasetID.csv, where ID is the progressive numeric sequence ID for each repetition of the activity performed.

In each file, each row corresponds to a time step measurement (in temporal order) and contains the following information:
avg_rss12, var_rss12, avg_rss13, var_rss13, avg_rss23, var_rss23
where avg and var are the mean and variance values over 250 ms of data, respectively.

**- Target data:**
Target data is provided as the containing folder name.

For each activity, we have the following parameters:
* Frequency (Hz): 20
* Clock (millisecond): 250
* Total duration (seconds): 120

## **Training and Testing Dataset**
As we know that, the dataset is to be divided into training and test datasets for training and testing the Machine learning algorithms.
In our project, let us keep datasets 1 and 2 in folders bending1 and bending 2, as well as datasets 1,2, and 3 in other folders as test data and other datasets as train data.
Therefore there are a total of 69 instances of training and 19 instances in testing dataset.

## **Feature Extraction**

Classification of time series usually needs extracting features from them. In this problem, I focus on time-domain features.
i. Researched what types of time-domain features are usually used in time series classification and listed them.
* Features usually used in time-series classification problems are minimum, maximum, mean, median, standard deviation, first quartile, and third quartile of each time-series. 

ii. Therefore with respect to the project extracted the time-domain features minimum, maximum, mean, median, standard deviation, first quartile, and third quartile for all of the 6 time series in each instance. You are free to normalize/standardize features or use them
directly.2
Your new dataset will look like this:
|Instance| min1 |max1| mean1| median1|-|-|-|min6|max6|mean6|median6|1st quart6| 3rd quart6|label|
|--------|------|----|------|--------|-----|------|------|----|----|-----|-------|----------|-----------|----|
|1|
|2|
|3|
|'|
|'|
|88|

From the above table we could see that, for each instance six features are extracted  making the feature dataframe shape to 36 * 88. Here the label column is added to the dataframe which is target column that we are predicting. Here as already mentioned, the folders in which they are present, the folder name is given as label. As there are 7 folders, there are a total of seven activities. namely bending1, bending2, cycling, sitting, standing, walking, lying. Since the labels are text data, they are encoded to integers using scikit-learn encoder function.

From the displayed table, three most important features namely mean, median and mode are selected and used for the machine learning problem. *The extracted features for each of the time series are mean, median and standard deviation, this is because these three statastics for important parameters to describe most of the probability distributions*. Now the shape of our feature dataframe is 18 * 88.

## **Binary Classification using Logistic Regression**

**Case 1:**
Let us assume that you want to use the training set to classify bending from other activities, i.e. you have a binary classification problem. 

Scatter plots are depicted of the features extracted of each instance and used color to distinguish bending vs other activities. the plot is as follows.

**Case 2**
Let us break each time series in your training set into two (approximately) equal length time series. Now instead of 6 time series for each of the training instances, you have 12 time series for each training instance. Let us extract the 3 most important time series features from this 12 time series columns. Now depict scatter plots of the features extracted from both parts of the time series 1,2, and 12. Do you see any considerable difference in the results with those of case 1? 

**When the features are extracted by dividing the time series dataset into "TWO", there are more no of features than the original one.
Scatter Plots are used to understand the effect of features on the classification problem.
When there are more features, there is definitely a chance to understand the patterns better. 
This can be observed in the above Scatterplots too. In some of the plots above, we can see a clear distinction 
between the classes in some scatter plots than the ones before.
So, it would be good idea to divide the scatter plots multiple times and extract the features from them.** 

Let us now break each time series in your training set into l ∈ {1, 2, . . . , 20} time series of approximately equal length and use logistic regression to solve the binary classification problem, using time-domain features. 

Remember that breaking each of the time series does not change the number of instances. It only changes the number of features for each instance. Here let us calculate the p-values for your logistic regression parameters in each model corresponding to each value
of l and refit a logistic regression model using your pruned set of features.Alternatively, you can use backward selection using sklearn.feature selection or glm in R. Here I used 5-fold cross-validation to determine the best value of the pair (l, p), where p is the number of features used in recursive feature elimination.

Here they are two ways of performing cross validation, for finding best value of pair(l,p). The right way to do Cross Validation would be to 
1) Feature Selection
2) Cross Validate

The wrong way of doing is:
1) Cross Validate
2) Feature Selection

Also, here we encountered the problem of class imbalance, which may make some of your folds not having any instances of the rare class.
**Stratified Cross Validation** can be used as this is an Imbalanced Dataset. This can be helpful to repersent every class is repersented in each fold.

Here I reported the confusion matrix and show the ROC and AUC for your classifier on train data. and reported the parameters of your logistic regression βi’s as well as the p-values associated with them.

# **Testing Dataset performance:**
Let us test the classifier on the test set. Remember to break the time series in your test set into the same number of time series into which you broke your training set. Remember that the classifier has to be tested using the features extracted from the test set. 

## **Analysis**
**Compare the accuracy on the test set with the cross-validation accuracy you obtained previously?**
* From the above results, we could see that the test accuracy and the train accuracy obtained is 100%. This is because the classes are well seperated. 
* This causes instability in the calculation of parameters of Logistic Regression.
* As a result the estimated p-values are higher. This causes Maximum Likelihood Estimate to fail Leading in a Perfect Seperation Error.

**From the confusion matrices you obtained, do you see imbalanced classes?**

* It is clearly evident that the classes obtained are imbalanced, let us use oversampling using SMOTE to handle this problem.
* therefore let us  build a logistic regression model based on case-control sampling and adjust its parameters. 
* Now report the confusion matrix, ROC, and AUC of the model.

# **Binary Classification Using L1-penalized logistic regression:**
Now let us repeat the above mentioned procedure using L1-penalized logistic regression i.e. instead of using pvalues for variable selection, use L1 regularization. 

Note that in this problem, you have to cross-validate for both l, the number of time series into which you break each of your instances, and λ, the weight of L1 penalty in your logistic regression objective function (or C, the budget). Packages usually perform
cross-validation for λ automatically.

## **Analysis:**
**Now let us compare the L1-penalised with variable selection using p-values?**
* L1 regularization can be used to feature selection. As the feature coefficients become zero here.
* It is easier to implement than Recursive Feature Selection or based on p values because.
* it just involves solving the optimization problem with a constraint.







## **Source:**
Filippo Palumbo (a,b), Claudio Gallicchio (b), Rita Pucci (b) and Alessio Micheli (b)
(a) Institute of Information Science and Technologies â€œAlessandro Faedoâ€, National Research Council, Pisa, Italy
(b) Department of Computer Science, University of Pisa, Pisa, Italy

## **Relevant Papers:**

[1] F. Palumbo, C. Gallicchio, R. Pucci and A. Micheli, Human activity recognition using multisensor data fusion based on Reservoir Computing, Journal of Ambient Intelligence and Smart Environments, 2016, 8 (2), pp. 87-107.

[2] F. Palumbo, P. Barsocchi, C. Gallicchio, S. Chessa and A. Micheli, Multisensor data fusion for activity recognition based on reservoir computing, in: Evaluating AAL Systems Through Competitive Benchmarking, Communications in Computer and Information Science, Vol. 386, Springer, Berlin, Heidelberg, 2013, pp. 24â€“35.




