---
title: "Getting and Cleaning Data Course Project"
author: "Todd W. Beadle"
date: "10/23/2015"
output:
  html_document:
    keep_md: yes
---

## Project Description
The project was designed to demonstrate the student's ability to obtain, process, and present data.

##Study design and data processing
A body of real life data obtained as part of a study on using smartphone internal sensors to measure user activity was provided to the student.  The student was required to merge training and test data sets into a single pool of raw data and extract only the variables representing standard deviation and mean values.  The dataset was then augmented with descriptive labels for the activity type mapped from the original integer data.  The resulting dataset was then relabled with descriptive variable names.  Finally a tidy dataset was created to represent the average of each of the variables for each activity and each subject.

###Collection of the raw data
The data was provided for the student in the form of a zip archive file UCI_HAR_Dataset.zip
UCI_HAR_Dataset/
UCI_HAR_Dataset/test
UCI_HAR_Dataset/test/X_test.txt
UCI_HAR_Dataset/test/Inertial Signals
UCI_HAR_Dataset/test/Inertial Signals/body_gyro_z_test.txt
UCI_HAR_Dataset/test/Inertial Signals/total_acc_y_test.txt
UCI_HAR_Dataset/test/Inertial Signals/body_acc_z_test.txt
UCI_HAR_Dataset/test/Inertial Signals/body_acc_x_test.txt
UCI_HAR_Dataset/test/Inertial Signals/body_gyro_y_test.txt
UCI_HAR_Dataset/test/Inertial Signals/body_gyro_x_test.txt
UCI_HAR_Dataset/test/Inertial Signals/body_acc_y_test.txt
UCI_HAR_Dataset/test/Inertial Signals/total_acc_x_test.txt
UCI_HAR_Dataset/test/Inertial Signals/total_acc_z_test.txt
UCI_HAR_Dataset/test/y_test.txt
UCI_HAR_Dataset/test/subject_test.txt
UCI_HAR_Dataset/activity_labels.txt
UCI_HAR_Dataset/README.txt
UCI_HAR_Dataset/features_info.txt
UCI_HAR_Dataset/train
UCI_HAR_Dataset/train/y_train.txt
UCI_HAR_Dataset/train/subject_train.txt
UCI_HAR_Dataset/train/Inertial Signals
UCI_HAR_Dataset/train/Inertial Signals/total_acc_z_train.txt
UCI_HAR_Dataset/train/Inertial Signals/total_acc_y_train.txt
UCI_HAR_Dataset/train/Inertial Signals/body_gyro_y_train.txt
UCI_HAR_Dataset/train/Inertial Signals/total_acc_x_train.txt
UCI_HAR_Dataset/train/Inertial Signals/body_acc_y_train.txt
UCI_HAR_Dataset/train/Inertial Signals/body_gyro_x_train.txt
UCI_HAR_Dataset/train/Inertial Signals/body_acc_z_train.txt
UCI_HAR_Dataset/train/Inertial Signals/body_gyro_z_train.txt
UCI_HAR_Dataset/train/Inertial Signals/body_acc_x_train.txt
UCI_HAR_Dataset/train/X_train.txt
UCI_HAR_Dataset/features.txt

##Creating the tidy datafile

###Guide to create the tidy data file
Download and unzip data file from link provided
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

You should create one R script called run_analysis.R that does the following. 
   1. Merges the training and the test sets to create one data set.
   2. Extracts only the measurements on the mean and standard deviation for each measurement. 
   3. Uses descriptive activity names to name the activities in the data set
   4. Appropriately labels the data set with descriptive variable names. 
   5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

####File locations:
 - UCI_HAR_Dataset/features.txt
 - UCI_HAR_Dataset/activity_labels.txt
 - UCI_HAR_Dataset/features_info.txt
 - test_subject_df <- UCI_HAR_Dataset/test/subject_test.txt
 - test_activity_df <- UCI_HAR_Dataset/test/y_test.txt
 - test_observations_df <- UCI_HAR_Dataset/test/X_test.txt
 - train_subject_df <- UCI_HAR_Dataset/train/subject_train.txt
 - train_activity_df <- UCI_HAR_Dataset/train/y_train.txt
 - train_observations_df <- UCI_HAR_Dataset/train/X_train.txt

###Cleaning of the data
 - Load required libraries
 - Read Test Files
 - Merge Subject, Activity, and Observation Data
 - Read Training Files
 - Merge Subject, Activity, and Observation Data
 - Merge Test and Training Data
 - Read Observation Labels
 - Create vector of observations columns with "-std()" or "-mean()" add offset for subject and activity
 - Select subject, activity, std and mean columns from raw_data
 - Read Activity Descriptions
 - Merge Activity Name data 
 - Clean up sm_data columns
 - Create descriptive name vector for sm_data from features.txt
 - Apply descriptive names to sm_data data frame
 - Create tidy dataset of average variable values for each activity and each subject
 - Create meaningfull names for tidy dataset columns
 - Write tidy dataset to file

##Description of the variables in the gd_couresproj_tidyout.txt file

###group_by_activity_name
This variable represents the activity being performed when the measurements were recorded
 - Class: Factor w/ 6 Levels
 - Unique values/levels of the variable:
      WALKING
      WALKING_UPSTAIRS
      WALKING_DOWNSTAIRS
      SITTING
      STANDING
      LAYING
 - Unit of measurement: NONE

###group_by_subject_id
This variable represents the identfication number assigned to research study participants
 - Class: Integer
 - Unique values/levels of the variable
      Integer value from 1 to 30 corresponding with each study participant
 - Unit of measurement: NONE

###avg(general information)
These variables represent the average mean and standard deviations computed from the measurement in the studay data collected described below.  The naming convention used adhers to the one set put for the study data with the prefix avg to indicate average values.

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

###avg_tBodyAcc-mean()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAcc-mean()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAcc-mean()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAcc-std()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAcc-std()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAcc-std()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tGravityAcc-mean()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tGravityAcc-mean()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tGravityAcc-mean()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tGravityAcc-std()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tGravityAcc-std()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tGravityAcc-std()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccJerk-mean()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccJerk-mean()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccJerk-mean()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccJerk-std()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccJerk-std()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccJerk-std()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyro-mean()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyro-mean()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyro-mean()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyro-std()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyro-std()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyro-std()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroJerk-mean()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroJerk-mean()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroJerk-mean()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroJerk-std()-X
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroJerk-std()-Y
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroJerk-std()-Z
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccMag-mean()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccMag-std()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tGravityAccMag-mean()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tGravityAccMag-std()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccJerkMag-mean()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyAccJerkMag-std()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroMag-mean()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroMag-std()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroJerkMag-mean()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_tBodyGyroJerkMag-std()
 - Class: Number
 - Unit of measurement: Time Domain Signal

###avg_fBodyAcc-mean()-X
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAcc-mean()-Y
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAcc-mean()-Z
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAcc-std()-X
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAcc-std()-Y
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAcc-std()-Z
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAccJerk-mean()-X
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAccJerk-mean()-Y
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAccJerk-mean()-Z
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAccJerk-std()-X
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAccJerk-std()-Y
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAccJerk-std()-Z
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyGyro-mean()-X
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyGyro-mean()-Y
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyGyro-mean()-Z
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyGyro-std()-X
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyGyro-std()-Y
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyGyro-std()-Z
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAccMag-mean()
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyAccMag-std()
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyBodyAccJerkMag-mean()
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyBodyAccJerkMag-std()
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyBodyGyroMag-mean()
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyBodyGyroMag-std()
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyBodyGyroJerkMag-mean()
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

###avg_fBodyBodyGyroJerkMag-std()
 - Class: Number
 - Unit of measurement: Frequency Domain Signal

