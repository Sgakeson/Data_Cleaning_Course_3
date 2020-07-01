Codebook:

For explinations of the variables included with the data during download please
reference the codebooks written by the authors of the data. This codebook solely
contains explinations of the variables created in this code, the data created by
this code, and the work used to transform this data.

List of R objects created:
        Y_train
        Y_test
        X_train
        X_test
        Subject_train
        Subject_test
        Features
        Full_Data
        Mean_Full_Data

R Object descriptions:

        Y_train: A data table size [7352,1] containing the activity code (1-6) 
        for all of the data measurements for the training participants.
        
        Subject_train: A data table size [7352, 1] containing the Subject id
        numbered 1-30.
        
        X_train: A data table size [7352, 561] containing the measurements taken
        during the experiment. 
        
        Y_test: A data table size [2947,1] containing the activity code (1-6) 
        for all of the data measurements for the testing participants.
        
        Subject_test: A data table size [2947, 1] containing the Subject id
        numbered 1-30.
        
        X_test: A data table size [2947, 561] containing the measurements taken
        during the experiment. 
        
        Features: A data tables size [561, 2] containing the measurment
        descriptions(used as column names) for the data measurements.
        
        Full_Data: A data table that ranges in size during the program and is
        used as the data table to organize and clean the data.
        
        Mean_Full_Data: A new data table created through the dplyr summarize
        function. It is the average of each variable for each activity and each 
        subject.

Data Description:
        Briefly, the data is measurements of Triaxial acceleration from the 
        accelerometer and Triaxial Angular velocity from the gyroscope. For a 
        more detailed description the README file and the features_info file contained 
        with the downloaded data give more information about the units of the
        data as well as the detailed descriptions of the experimental process.
        
Data manipulation in the R script:
        The R script performs the following tasks:
                
                1. Reads in and merges all of the files that represent the data,
                column names, subject numbers, and activity numbers.
                
                2. Renames all of the temporary column names with the data names
                given in the features.txt file.
                
                3. Orders the data such that the subjects are listed in increasing
                numerical order (1-30) and then within each subject the activities
                are listed in increasing numberical order (1-6).
                
                4. Remove all columns that don't measure a mean or standard 
                deviation excluding  the metadata columns 1 and 2
                
                5. The activities are renamed based on the activity_labels.txt
                key provided in the initial download.
                
                6. Using the dplyr group_by() function the data is grouped into
                Subjects and each Subject is subgrouped into activity.
                
                7. Utilizing the %>% operator those subgroups are fed into the
                mean function which returns the average value for each variable 
                for each activity and each subject
        
        