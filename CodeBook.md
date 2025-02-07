## Getting and Cleaning Data Project

### Description
Additional information about the variables, data and transformations used in the course project for the Johns Hopkins Getting and Cleaning Data course.

### Source Data
Data + Description can be found here [UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)

### Data Set Information
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain.

### Attribute Information
For each record in the dataset it is provided: 
- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration. 
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

----------------------------------------------------------------------
The [run_analysis.R](https://github.com/MesyMacos/Getting-and-Cleaning-Data-Course-Project/blob/master/run_analysis.R) script performs the data preparation and then followed by the 5 steps required as described in the course project’s definition.

### 1. Download the dataset
Dataset downloaded and extracted under the folder called [UCI HAR Dataset](https://github.com/MesyMacos/Getting-and-Cleaning-Data-Course-Project/tree/master/UCI%20HAR%20Dataset)

### 2. Assign each data to variables
- `features` <- `features.txt` : 561 rows, 2 columns

_The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ._
- `activities` <- `activity_labels.txt` : 6 rows, 2 columns

_List of activities performed when the corresponding measurements were taken and its codes (labels)_
- `subject_test` <- `test/subject_test.txt` : 2947 rows, 1 column

_contains test data of 9/30 volunteer test subjects being observed_
- `x_test` <- `test/X_test.txt` : 2947 rows, 561 columns

_contains recorded features test data_
- `y_test` <- `test/y_test.txt` : 2947 rows, 1 columns

_contains test data of activities’code labels_
- `subject_train` <- `test/subject_train.txt` : 7352 rows, 1 column 

_contains train data of 21/30 volunteer subjects being observed_
- `x_train` <- `test/X_train.txt` : 7352 rows, 561 columns 

_contains recorded features train data_
- `y_train` <- `test/y_train.txt` : 7352 rows, 1 columns

_contains train data of activities’code labels_

### 3. Merges the training and the test sets to create one data set
* `X` (10299 rows, 561 columns) is created by merging `x_train` and `x_test` using **rbind()** function
* `Y` (10299 rows, 1 column) is created by merging `y_train` and `y_test` using **rbind()** function
* `Subject` (10299 rows, 1 column) is created by merging `subject_train` and `subject_test` using **rbind()** function
* `Merged_Data` (10299 rows, 563 column) is created by merging `Subject`, `Y` and `X` using **cbind()** function

### 4. Extracts only the measurements on the mean and standard deviation for each measurement
`TidyData` (10299 rows, 88 columns) is created by subsetting `Merged_Data`, selecting only columns: `subject`, `code` and the measurements on the `mean` and standard deviation (`std`) for each measurement

### 5. Uses descriptive activity names to name the activities in the data set
Entire numbers in `code` column of the `TidyData` replaced with corresponding activity taken from second column of the  `activities` variable

### 6. Appropriately labels the data set with descriptive variable names
* `code` column in `TidyData` renamed into a`ctivities`
* All `Acc` in column’s name replaced by `Accelerometer`
* All `Gyro` in column’s name replaced by `Gyroscope`
* All `BodyBody` in column’s name replaced by `Body`
* All `Mag` in column’s name replaced by `Magnitude`
* All start with character `f` in column’s name replaced by `Frequency`
* All start with character `t` in column’s name replaced by `Time`

### 7. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject
* `FinalData` (180 rows, 88 columns) is created by sumarizing `TidyData` taking the means of each variable for each activity and each subject, after groupped by subject and activity.
* Export `FinalData` into `FinalData.txt` file.
