# Backblaze
This repo contains notebooks to download, preprocess and get started working with the [Backblaze](https://www.backblaze.com/b2/hard-drive-test-data.html) data.

### Overview:

In an effort to make a number of operational datasets more widely available and useful for data scientists, the AIOps group within the office of the CTO at Red Hat has decided to select a few key datasets that can be made open source within the IT domain for training Machine Learning models. The first will be a portion of the Backblaze data for hard drive failure prediction.  

### Project Description:

Although the Backblaze data has already been made available in its entirety [here](https://www.backblaze.com/b2/hard-drive-test-data.html), our goal is to provide a dataset with some basic preprocessing done to make it more manageable and easier to work with out of the gate. We hope to mirror the sentiment noted on Yann Lecun’s MNIST website and prepare the Backblaze data in such a way that it is, “a good database for people who want to try learning techniques and pattern recognition methods on real-world data while spending minimal efforts on preprocessing and formatting”. 

In addition, we also define a specific problem that we would like the community to solve with this data set. Namely, **given the previous 6 days of data, accurately predict the value of SMART metric 1 ‘Read Error Rate’ for the following day**. 

Our hope is that these notebooks will help to generate a dataset that is manageable, but still large enough, to serve as a benchmark or ‘golden dataset’ that can be relied on and referenced by the community at large when comparing different drive failure prediction techniques.   

We have selected the 6 day time window, as we believe it reflects a realistic retention policy for a user in a real-world scenario, and we would like our community built models to follow this same restriction to ensures that any experiments done could be easily and actually implemented in practice.  

The data is provided as 3 csv files, divided into train/ test/ validation splits with an equal distribution of failed and working drives (about 100:1) in each.   


#### Problem Statement:

Given, at most, the previous 6 days of SMART metric data, can we accurately predict the value of SMART metric 1 “Read Error Rate” for the following day?  

This can be thought of as a multi-dimensional time series regression problem, where we have 130 dimensional data points captured over multiple days, and our goal is to predict (forecast) the value of one feature on the following day.  

#### Evaluation: 

The evaluation metric for this project is the Mean Squared Logarithmic Error. This metric has been chosen over the standard MSE due to the large values of our target variable.  


We will also provide a number of baseline MSLE’s based on extremely naive models that simply predict the value to be equal to the previous day’s value, or the average of the past 6 days, etc. Any model, to be considered performant, must outperform the best of these naive approaches and score a lower MSLE.     


#### Data:

As noted above, our goal is to curate a benchmark dataset for those who want to spend minimal effort on preprocessing and formatting. To this end, we will look only at the most recent data available as of October 2019, that is data from Q2_2019, and we will only look at drives associated with the manufacturer Seagate. We do this because there are possible inconsistencies among the meaning of SMART metrics across manufacturers, so keeping with a single manufacturer should yield the most consistent results.   

We have taken the following steps in an effort to make the data more manageable:

* Restrict ourselves to the most recent quarter of data, Q2_2019, which contains ~9 million data points.
* Only looking at 1 manufacturer: Seagate. Which leaves ~7 million data points.

* Randomly sampled from working drives so that we have a 100:1 ratio of working:failed drives

These actions effectively halved the size of the data from ~3Gb to ~1.5Gb (for a single quarter). 

We have kept all 130 SMART metrics in the data set. There is a fair amount of literature about which metrics are most and least informative and there are a few metrics that contain a large number of NaN’s. But, we felt that any additional feature selection or NaN interpolation might introduce too much bias and have therefore avoided it here. However, our 'Getting_Started' notebook will provide suggestions for how to deal with both of these issues.   

#### The Data Set: 
Using the 'convert_backblaze' notebook generates the following dataset.

4,443,314 data points across 49,490 individual drives over a 90 day time window.

In addition, we have divided the data into 3 separate csv files:

* test_backblaze_seagate_q2_2019.csv : ~369Mb 
* train_backblaze_seagate_q2_2019.csv: ~1.1Gb
* validation_backblaze_seagate_q2_2019.csv: ~375Mb

##### Training Set: 
2,665,601 data points, across  29,694 individual drives. With an average of 89.7 entries per drive. 

##### Testing Set:
887,632 examples across 9,898 individual drives. With an average of 89.7 entries per drive

##### Validation Set:
889,081 examples across 9,898 individual drives. With an average of 89.9 entries per drive. 

#

To learn more about the specific features, please look [here](https://www.backblaze.com/b2/hard-drive-test-data.html) 

# 
Finally, as this work is based on data collected by Backblaze I would like to cite them as the source of this data, as well as repost their requests around data usage below. And ask that anyone who uses or contributes to any of the work in this repo follow these same guidelines. 

**How You Can Use the Data**

You can download and use this data for free for your own purpose, all we ask is three things 
1) you cite Backblaze as the source if you use the data, 
2) you accept that you are solely responsible for how you use the data
3) you do not sell this data to anyone, it is free.