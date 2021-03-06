# Human Activity Recognition (HAR) Analysis
## Course 3 - Getting and Cleaning Data - Week 4 Project
## Paul Ringsted, 7th October 2018
---
### Overview and Study Design
Loads raw data from the messy UCI HAR dataset, merges into tidy dataset and generates summarized output.

The data used in this project represents data collected from the accelerometers from the Samsung Galaxy S smartphone.

A full description of the study is available at the site where the data was obtained:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Data set used for this project:
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

---
### Execution Description
|Item|Notes|
|:---|:---|
|Usage|**run_analysis()**|
|Inputs|HAR dataset in current working directory (*test* and *train* are immediate subdirectories)|
|Outputs|Mean of mean() and std() observations by subject ID and activity to file *harmean.txt*|
---
### Data Process Steps:
1. Load reference file *activity_labels.txt* from working directory (enumerates activity names)
2. Load reference file *features.txt* from working directory (enumerates observation column names)
3. Identify the mean() and std() cols only for final dataset (66 observations; Freq cols excluded)
4. Clean up the observation column names - strips punctuation and converts to lowercase
5. Process each TYPE = {test|train} dataset from TYPE subdirectory, using subfunction **harload(...)**:
	1. Load *subject_TYPE.txt*  -  Subject ID for the observation set (1-30)
	2. Load *y_TYPE.txt*  -  Activity labels for the observation set (1-6)
	3. Load *X_TYPE.txt*  -  Observation set (561 variables per obs)
	4. Convert activity ID in activity labels (y) data to activity name
	5. Selects only the mean() and std() observations from the observation (X) data
	6. Returns data frame with: subject id, activity name, selected observations
6. Merge the two datasets
7. Summarize data using aggregate() - calc mean() of each col, by subject id and activity name
8. Output summary resultset to file *harmean.txt* in working directory
---
### Codebook
|Column|Name|Type|Min|Max|Values|Description|
|:---|:---|:---|:---|:---|:---|:---|
1|subjectid|int|1|30||Id of subject for observation|
2|actname|char|||WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING|Activity for observation|
||
3-8|tbodyacc{mean,std}{x,y,z}|numeric|-1|1||Body Acceleration in 3D|
9-14|tgravityacc{mean,std}{x,y,x}|numeric|-1|1||Gravity Acceleration in 3D|
15-20|tbodyaccjerk{mean,std}{x,y,z}|numeric|-1|1||Body Linear Acceleration in 3D|
21-26|tbodygyro{mean,std}{x,y,z}|numeric|-1|1||Body Gyroscope in 3D|
27-32|tbodygyrojerk{mean,std}{x,y,z}|numeric|-1|1||Body Angular Velocity in 3D|
||
33-34|tbodyaccmag{mean,std}|numeric|-1|1||Body Acceleration Magnitude|
35-36|tgravityaccmag{mean,std}|numeric|-1|1||Gravity Acceleration Magnitude|
37-38|tbodyaccjerkmag{mean,std}|numeric|-1|1||Body Linear Acceleration Magnitude|
39-40|tbodygyromag{mean,std}|numeric|-1|1||Body Gyroscope Magnitude|
41-42|tbodygyrojerkmag{mean,std}|numeric|-1|1||Body Angular Velocity Magnitude|
||
43-48|fbodyacc{mean,std}{x,y,z}|numeric|-1|1||Body Acceleration in 3D FFT|
49-54|fbodyaccjerk{mean,std}{x,y,z}|numeric|-1|1||Body Linear Acceleration in 3D FFT|
55-60|fbodygyro{mean,std}mean{x,y,z}|numeric|-1|1||Body Gyroscope in 3D FFT|
||
61-62|fbodyaccmag{mean,std}|numeric|-1|1||Body Acceleration Magnitude FFT|
63-64|fbodybodyaccjerkmag{mean,std}|numeric|-1|1||Body Linear Acceleration Magnitude FFT|
65-66|fbodybodygyromag{mean,std}|numeric|-1|1||Body Gyroscope Magnitude FFT|
67-68|fbodybodygyrojerkmag{mean,std}|numeric|-1|1||Body Angular Velocity FFT|

**Notes**
1. Where OBS{mean,std}{x,y,z} infers iteration of variables named as follows
	1. OBSmeanx (mean in X direction)
	2. OBSmeany (mean in Y direction)
	3. OBSmeanz (mean in Z direction)
	4. OBSstdx (standard deviation in X direction)
	5. OBSstdy (standard deviation in Y direction)
	6. OBSstdz (standard deviation in Z direction)

2. FFT = Fast Fourier Transform (Frequency Domain)
3. For more information on the observation variables, see notes in the HAR dataset (*features_info.txt*)
