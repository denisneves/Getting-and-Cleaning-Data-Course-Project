# Getting-and-Cleaning-Data-Course-Project
Week 4 exercise
==================================================================
Data Science Coursera/Johns Hopkins Course
Getting and Cleaning Data Course Project
==================================================================
Denis R. Neves
==================================================================

A dataset has been created using data from an experiment which was carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. The script working conditions to arrange data and get the mean for each variable to the subject and activities groups are described below.

# 1. Appropriately labeling the data set with descriptive variable names

X_test <- `colnames<-`(X_test, features$V2)

X_train <- `colnames<-`(X_train, features$V2)

subject_test <- data.frame(subject = subject_test$V1)

subject_train <- data.frame(subject = subject_train$V1)

activity_labels <- data.frame(V1 = activity_labels$V1, activity = activity_labels$V2)

# 2. Extracting only the measurements on the mean and standard deviation for each measurement

features <- data.frame(features = gsub("meanFreq", "freq", features$V2))

mean_sd <- grep('mean()|std()', features$features, value = TRUE)

x_test_set <- subset(X_test, select = mean_sd)

x_train_set <- subset(X_train, select = mean_sd)

# 3. Merging the training and the test sets to create one data set

x_test_set <- cbind(subject_test, y_test, x_test_set)

x_train_set <- cbind(subject_train, y_train, x_train_set)

data <- rbind(x_test_set, x_train_set)

# 4. Merging the activity variable and the data set

library(plyr)

data_set <- join(data, activity_labels, by = "V1")

# 5. Creating a second independent tidy data set with the average of each variable for each activity and each subject

library(dplyr)

mean_subject <- data.frame(subject = data_set$subject, select(data_set, 3:68))

mean_subject <- aggregate(. ~ subject, data = mean_subject, FUN = mean)

mean_activity <- data.frame(activity = data_set$activity, select(data_set, 3:68))

mean_activity <- aggregate(. ~ activity, data = mean_activity, FUN = mean)

final_data <- cbind(mean_subject, mean_activity)


========

Denis R. Neves. December 2016.
