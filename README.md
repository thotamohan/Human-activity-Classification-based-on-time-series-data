# Activity Recognition system based on Multisensor data fusion (AReM)

## **Task:**
An interesting task in machine learning is classification of time series. In this problem,
we will classify the activities of humans based on time series obtained by a Wireless
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

We also consider two kind of bending activity, illustrated in the figure provided (bendingTupe.pdf). The positions of sensor nodes with the related identifiers are shown in figure sensorsPlacement.pdf.

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

Classification of time series usually needs extracting features from them. In this problem, we focus on time-domain features.
i. Researched what types of time-domain features are usually used in time series classification and listed them.
* Features usually used in time-series classification problems are minimum, maximum, mean, median, standard deviation, first quartile, and third quartile of each time-series. 

ii. Therefore with respect to the project extracted the time-domain features minimum, maximum, mean, median, standard deviation, first quartile, and third quartile for all of the 6 time series in each instance. You are free to normalize/standardize features or use them
directly.2
Your new dataset will look like this:
|Instance| min1 |max1| mean1| median1|-----|------|------|min6|max6|mean6|median6|1st quart6| 3rd quart6|
|--------|------|----|------|--------|-----|------|------|----|----|-----|-------|----------|-----------|
|1|
|2|
|3|
|'|
|'|
|88|

## **Source:**
Filippo Palumbo (a,b), Claudio Gallicchio (b), Rita Pucci (b) and Alessio Micheli (b)
(a) Institute of Information Science and Technologies â€œAlessandro Faedoâ€, National Research Council, Pisa, Italy
(b) Department of Computer Science, University of Pisa, Pisa, Italy

## **Relevant Papers:**

[1] F. Palumbo, C. Gallicchio, R. Pucci and A. Micheli, Human activity recognition using multisensor data fusion based on Reservoir Computing, Journal of Ambient Intelligence and Smart Environments, 2016, 8 (2), pp. 87-107.

[2] F. Palumbo, P. Barsocchi, C. Gallicchio, S. Chessa and A. Micheli, Multisensor data fusion for activity recognition based on reservoir computing, in: Evaluating AAL Systems Through Competitive Benchmarking, Communications in Computer and Information Science, Vol. 386, Springer, Berlin, Heidelberg, 2013, pp. 24â€“35.




