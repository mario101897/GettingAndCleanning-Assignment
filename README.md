# GettingAndCleanning-Assignment
This repository is for the Course Proyect from courseras's course: Getting and Cleaning Data 


Hellow dear partnerr!! here i write the codes i wrote with them corresponding explanation. The objective was to collect and tidy data from the accelerometers from the Samsung Galaxy S smartphone, in other words: to polish it for further analysis. I wont elaborate here on the content of the varibles because as requested on the instructions i will explain it in the CodeBook.md.

We were ask to creat an R script that does this:

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.


First:
I download the file and unzip it

Second: 
I assign the data frames, i used the same names of the files

now we star to wirte the code:

Step 1:

I use the cbind and rbind functions to create one data set

Setep 2:

Use select to collect the specific part of data that i wanted, mean and std in this case

Step 3:

labe the names of the dataset

Step 4:

use group_by to analyses the table with the desireble variables, subject and activity in this case


