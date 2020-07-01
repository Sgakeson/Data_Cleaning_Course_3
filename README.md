# Data_Cleaning_Course_3

## The data for this project is downloaded at http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

## Read in all of the 6 tables (This doesn't account for needing to switch directories)
## It should be noted, these file paths assume that the current working directory is 
## UCI Har Data Set. All of the subsequent paths are for a windows operating system.

Y_test <- read.table("test\\y_test.txt")
X_test <- read.table("test\\X_test.txt")
Subject_test <- read.table("test\\subject_test.txt")
Features <- read.table("features.txt")
Y_train <- read.table("train\\y_train.txt")
X_train <- read.table("train\\X_train.txt")
Subject_train <- read.table("train\\subject_train.txt")

## Bind together the columns for all test or train appropriately
## Followed by binding the two sets of columns together to make the Data
## Table, Full_Data

Full_Data <- rbind(cbind(Subject_test, Y_test, X_test), cbind(Subject_train, Y_train, X_train))

## Bind the rows together for both data sets
Full_Data <- rbind(Test_Full_data, Train_Full_data)

##Rename the first and second column as Subjects and Activities
names(Full_Data)[1] <- "Subjects"
names(Full_Data)[2] <- "Activity"

##Rename all of the columns as features
for(i in 1:561){names(Full_Data)[i+2] <- Features[i,2]}

## Order the data in Columns 1 and 2 by Subject Number and then by Activity Number
Full_Data <- Full_Data[order(Full_Data[,1], Full_Data[,2]),]

## Extract only the mean and Std Deviation
Full_Data <- Full_Data[, grep("mean|std|Subjects|Activity", colnames(Full_Data))]

## Replace Activity Numbers with Activity Names
Full_Data$Activity[Full_Data$Activity == "1"] <- "Walking"
Full_Data$Activity[Full_Data$Activity == "2"] <- "Walking_Upstairs"
Full_Data$Activity[Full_Data$Activity == "3"] <- "Walking_Downstairs"
Full_Data$Activity[Full_Data$Activity == "4"] <- "Sitting"
Full_Data$Activity[Full_Data$Activity == "5"] <- "Standing"
Full_Data$Activity[Full_Data$Activity == "6"] <- "Laying"

## Utilizing dplyr functions group_by and summarize, create a new tidy data set
## only includes the average of each variable for each activity and
## each subject.

Mean_Full_Data <- Full_Data %>% group_by(Subjects, Activity) %>% summarize_all(mean)
