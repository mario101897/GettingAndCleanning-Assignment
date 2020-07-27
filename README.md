# GettingAndCleanning-Assignment
This repository is for the Course Proyect from courseras's course: Getting and Cleaning Data 


Hellow dear partnerr!! here i write the codes i wrote with them corresponding explanation. The objective was to collect and tidy data from the accelerometers from the Samsung Galaxy S smartphone, in other words: to polish it for further analysis. I wont elaborate here on the content of the varibles because as requested on the instructions i will explain it in the CodeBook.md.

Lets go for it!

First we download the file:

FileName <- GCData                                                                                      feel free to use any name that works for you.
fileURL <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"     download it the same way we have done it along the course, just remember
  download.file(fileURL, filename, method="curl")                                                        that you have to unzip it.
}  

unzip(fileName)

features <- read.table("UCI HAR Dataset/features.txt", col.names = c("n","functions"))
activities <- read.table("UCI HAR Dataset/activity_labels.txt", col.names = c("code", "activity"))
subject_test <- read.table("UCI HAR Dataset/test/subject_test.txt", col.names = "subject")
x_test <- read.table("UCI HAR Dataset/test/X_test.txt", col.names = features$functions)
y_test <- read.table("UCI HAR Dataset/test/y_test.txt", col.names = "code")
subject_train <- read.table("UCI HAR Dataset/train/subject_train.txt", col.names = "subject")
x_train <- read.table("UCI HAR Dataset/train/X_train.txt", col.names = features$functions)
y_train <- read.table("UCI HAR Dataset/train/y_train.txt", col.names = "code")
                                                                                                        Once the file is downloaded we need to assign the data frames, i was used 
                                                                                                        to work with read.csv, but since i was going to use .txt i choose read.tabl 
                                                                                                        I named the labels the same as the files 
Now we can continue. Remember that you have to call the library(dplyr) to work with this functions

X <- rbind(x_train, x_test)                                       we create one data ser by using rbind() and c(bind)
Y <- rbind(y_train, y_test)
Subject <- rbind(subject_train, subject_test)
Merged_Data <- cbind(Subject, Y, X)

TidyData <- Merged_Data %>% select(subject, code, contains("mean"), contains("std"))     and here we use select() to pick that part of the data that we are interested in
                                                                                         as we saw in the class the %>% is use to same some space, the code is esier to write
                                                                                         and to read

TidyData$code <- activities[TidyData$code, 2]


then we label the variable names

names(TidyData)[2] = "activity"                                              I used gsub() to replace the names but im pretty sure i'll be no problem if you use sub()
names(TidyData)<-gsub("Acc", "Accelerometer", names(TidyData))
names(TidyData)<-gsub("Gyro", "Gyroscope", names(TidyData))
names(TidyData)<-gsub("BodyBody", "Body", names(TidyData))
names(TidyData)<-gsub("Mag", "Magnitude", names(TidyData))
names(TidyData)<-gsub("^t", "Time", names(TidyData))
names(TidyData)<-gsub("^f", "Frequency", names(TidyData))
names(TidyData)<-gsub("tBody", "TimeBody", names(TidyData))
names(TidyData)<-gsub("-mean()", "Mean", names(TidyData), ignore.case = TRUE)
names(TidyData)<-gsub("-std()", "STD", names(TidyData), ignore.case = TRUE)
names(TidyData)<-gsub("-freq()", "Frequency", names(TidyData), ignore.case = TRUE)
names(TidyData)<-gsub("angle", "Angle", names(TidyData))
names(TidyData)<-gsub("gravity", "Gravity", names(TidyData))

FinalData <- TidyData %>%                                                 if you practice swirl this one is a no brainer, you use group_by to analyse by the variables that you 
    group_by(subject, activity) %>%                                       want, and the summarise to collect the mean.
    summarise_all(funs(mean))                                            
write.table(FinalData, "FinalData.txt", row.name=FALSE)
