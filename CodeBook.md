# Data Cleaning: wearable computing

## Intro: the dataset

The script run_analysis.R is made to be run on the data about wearable computing found [on this website](https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones).
The data have a series of measurements on different activities perormed by 30 volunteers who wore a smartphone (Samsung Galaxy S II) with an in-built accelerometer and gyroscope on the waist.
The data are given separately in different files, and the goal of the script is to (a) put everything together in a dataset, and (b) create a smaller dataset with the averaged values of each mean and standard deviation by activity and participant. 
There are two subsets of data: the TRAINING phase, and the TEST phase. Each of these are given in three files: one with the participant number arranged by observation, then only the observations in wide format, and the code for each of the activities, also arranged by observation. An extra file with the names of the columns is also provided.

Below is a description of the variables.

### Participants

Participants are identified with a number from 1 to 30. These numbers were not changed.

### Activities

The activities performed by the participants were:
- Walking (coded 1, we changed it here to "walking")
- Walking upstairs (coded 2, here "walking_upstairs")
- Walking downstairs (coded 3, here "walking_downstairs")
- Sitting (coded 4, here "sitting")
- Standing (coded 5, here "standing")
- Laying (coded 6, here "laying")



### The measurements 

These signals were used to estimate variables of the feature vector for each pattern:  '-XYZ' is used to denote 3-axial signals in the X, Y and Z directions. They contain time (prefix t) and frequency (prefix f) measurements.

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag

The means, standard deviations, and other measurements for each of these variables are given in the dataset. Each column consists of the variables above with the appended statistic in it, e.g., "tBodyAccMag-mean()". There are 561 columns in total. More information on the meaning of each specific measurement obtained from the participants' smartphones can be found in the features_info.txt file of the dataset; this script has left them as-is.

## The script run_analysis.r

The scripts takes the relevant files in the dataset and merges them in order to create one single dataset with all the measurements arranged in different columns by activity performed and subject number. Then, only the means and standard deviations are kept; these are later also averaged by subject and activity type, with these averages forming a new dataset (tidydata.txt)
Here is how the data were treated in the script:

- The three independent data sets corresponding to the TEST phase (subject_test.txt, basically a vector with participant number; x_test.txt, containing only the results; and y_test.txt, containing the labels for each activity) are opened first, and then put together with cbind(); then the **labels for each measurement** (file features.txt) are attached as column names. A further column labels each row of this subset as "test" (lines 10-25). The columns with the subject and activity type are labeled as "subject" and "activity", respectively.
- Lines 28-37 repeat the steps above with the data from the TRAINING phase.
- Line 40 **merges** both datasets using rbind().
- Line 46 keeps only the means and standard deviations recorded in the data by selecting only the columns with the strings **"mean()" and "std()"** in their name.
- Lines 50-56 use mutate() to **create a new column with activity names** ("activity_type") in a more readable way, replacing the numbers with which they were coded in the original data, and then deletes the column with the numbers and rearranges everything.
- Line 63 creates a new dataset which contains only the **mean** for each of the means and stds by subject and type of activity performed.
- Finally, line 69 saves this new dataset as "tidydata.txt".

## The dataset tidydata.txt

This dataset contains only the means by group and participant of all the means and standard variations found originally in the data.
