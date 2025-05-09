# Wearable Computing

This repo takes the data found on [this website](https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones) from an experiment where measurements from accelerator and gyroscope embedded in a smartphone were taken, and presents them in a more readable manner.
This repository consists of three files (aside from this one, that is):

- The file run_analysis.r contains a script that:
  - Merges all the files in the data as one single dataframe
  - Calculate means of mean and standard deviation from the measurements found in the dataframe
  - Creates a new dataframe with this new information.
    
- CodeBook.md contains the information on variables in the original data, how the files were manipulated, etc.

- The dataset tidydata.txt contains the means and standard deviation values, averaged by participant and type of activity.
