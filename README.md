# GetDataCourseProject
Repository for Getting and Cleaning Data course project
# This R program assembles and merges data files
# for the Getting and Cleaing Data course project.
# 
# From Assignment:
#   You should create one R script called run_analysis.R that does the following. 
#   1. Merges the training and the test sets to create one data set.
#   2. Extracts only the measurements on the mean and standard deviation for each measurement. 
#   3. Uses descriptive activity names to name the activities in the data set
#   4. Appropriately labels the data set with descriptive variable names. 
#   5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
#


# File locations:
# UCI_HAR_Dataset/features.txt
# UCI_HAR_Dataset/activity_labels.txt
# UCI_HAR_Dataset/features_info.txt
# test_subject_df <- UCI_HAR_Dataset/test/subject_test.txt
# test_activity_df <- UCI_HAR_Dataset/test/y_test.txt
# test_observations_df <- UCI_HAR_Dataset/test/X_test.txt
# train_subject_df <- UCI_HAR_Dataset/train/subject_train.txt
# train_activity_df <- UCI_HAR_Dataset/train/y_train.txt
# train_observations_df <- UCI_HAR_Dataset/train/X_train.txt

# Load required libraries
library(dplyr)

# Read Test Files
test_subject_df <- read.table("UCI_HAR_Dataset/test/subject_test.txt")
names(test_subject_df)[names(test_subject_df)=="V1"] <- "subject_id"
test_activity_df <- read.table("UCI_HAR_Dataset/test/y_test.txt")
names(test_activity_df)[names(test_activity_df)=="V1"] <- "activity_id"
test_observations_df <- read.table("UCI_HAR_Dataset/test/X_test.txt")

# Merge Subject, Activity, and Observation Data
test_data <- cbind(test_subject_df, test_activity_df, test_observations_df)

# Read Training Files
train_subject_df <- read.table("UCI_HAR_Dataset/train/subject_train.txt")
names(train_subject_df)[names(train_subject_df)=="V1"] <- "subject_id"
train_activity_df <- read.table("UCI_HAR_Dataset/train/y_train.txt")
names(train_activity_df)[names(train_activity_df)=="V1"] <- "activity_id"
train_observations_df <- read.table("UCI_HAR_Dataset/train/X_train.txt")

# Merge Subject, Activity, and Observation Data
train_data <- cbind(train_subject_df, train_activity_df, train_observations_df)

# Merge Test and Training Data
raw_data <- rbind(test_data, train_data)

# Read Observation Labels
obs_label <- read.table("UCI_HAR_Dataset/features.txt")

# Create vector of observations columns with "-std()" or "-mean()" add offset for subject and activity
std_and_mean <- which(grepl("-std\\(\\)", obs_label$V2) | grepl("-mean\\(\\)", obs_label$V2)) + 2

# Select subject, activity, std and mean columns from raw_data
sm_data <- select(raw_data, 1, 2, std_and_mean)

# Read Activity Descriptions
act_desc <- read.table("UCI_HAR_Dataset/activity_labels.txt")
names(act_desc)[1:2] <- c("activity_id","activity_name")

# Merge Activity Name data 
sm_data <- merge(sm_data, act_desc, by = "activity_id")

# Clean up sm_data columns
sm_data <- select(sm_data, subject_id, activity_id, activity_name, V1:V543)

# Create descriptive name vector for sm_data from features.txt
new_labels <- select(obs_label[std_and_mean - 2,],V2)

# Apply descriptive names to sm_data data frame
names(sm_data) <- c(names(sm_data)[1:3], as.vector(new_labels$V2))

# Create tidy dataset of average variable values for each activity and each subject
tidy_out <- aggregate(sm_data[,4:ncol(sm_data)], list(sm_data$activity_name,sm_data$subject_id), mean)

# Create meaningfull names for tidy dataset columns
names(tidy_out) <- c(paste("group_by_",names(sm_data)[3], sep = ""),paste("group_by_",names(sm_data)[1], sep = ""), paste("avg_", new_labels$V2,sep = ""))

# Write tidy dataset to file
write.table(tidy_out, file = "gd_couresproj_tidyout.txt", row.names=FALSE)
