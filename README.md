# Human Activity Recognition (HAR) Analysis
## Course 3 - Getting and Cleaning Data - Week 4 Project
## Paul Ringsted, 7th October 2018
---
### Overview
Loads raw data from the messy UCI HAR dataset, merges into tidy dataset and summarizes

The data used in this project represents data collected from the accelerometers from the Samsung Galaxy S smartphone.

A full description is available at the site where the data was obtained:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Data set used for this project:
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

---
### Execution Description
|Item|Notes|
|:---|:---|
|Usage|**run_analysis()**|
|Inputs|HAR dataset in current working directory (test and train are immediate subdirectories)|
|Outputs|Mean of mean() and std() observations by subject ID and activity to file *harmean.txt*|
---
### Data Process Steps:
1. Loads reference file *activity_labels.txt* from working directory (enumerates activity names)
2. Loads reference file *features.txt* from working directory (enumerates observation column names)
3. Identifies the mean() and std() cols only for final dataset (66 observations; "Freq" cols excluded)
4. Cleans up the observation column names - strips punctuation and converts to lowercase
5. Processes each <type> = {test|train} dataset from <type> subdirectory, using subfunction **harload(...)**:
- Load *subject_<type>.txt*	Subject ID for the observation set (1-30)
- Load *y_<type>.txt*		Activity labels for the observation set (1-6)
- Load *X_<type>.txt*		Observation set (561 variables per obs)
- Converts activity ID in activity labels (y) data to activity name
- Selects only the mean() and std() observations from the observation (X) data
- Returns data frame with: subject id, activity name, selected observations
6. Merges the two datasets
7. Summarizes data using aggregate() - calc mean() of each col, by subject id and activity name
8. Outputs summary resultset to file *harmean.txt* in working directory
---
