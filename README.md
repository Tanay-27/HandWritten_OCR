# HandWritten_OCR
Handwritten Character Recognition using NIST dataset

## About the dataset
https://www.kaggle.com/tanay27/handwrittennist

The dataset for this has been taken and preprocessed for utility purposes by manually naming each folder and preprocessing images to a standard size of 28x28 pixels as well as storing them in the form of csv files for direct implementation to CNNs.
The dataset contains 62 files - 26 each of upper and lower characters and 10 digits. For ease of use, ew have considered label of capital and small alphabets same.
Before combining one will have to add collumn names to the dataframe for concatenation.
Code snippet  - 
``` def initialise():
    data = pd.read_csv('dataset/a.csv')
    data.columns = col
    for file in os.listdir('dataset'):
        if(file=='a.csv'):
            continue
        df = pd.read_csv('dataset/'+file)
        df.columns = col
        data = pd.concat([data,df],ignore_index=True)
    return data 
 ```   
When the above code is run, the dataset can be easily read and dataframe is returned which is ready to use

## About Character Extraction
The input image is subjected to basic preprocessing using opencv and then segmentation for each line is done contour matching.
Each line segmented is further subjected to contour matching which results into segmentation of each word. 
Now comes the most difficult part ie. segmenting words into its constituent characters. 
This is difficult because no current available engines or library functions are able to segement at such resolutions and accuracy.
Thus special attention needs to be given to this step.
Here we have used Histogram Splitting to acheive character level segmentation.

![alt text](https://github.com/Tanay-27/HandWritten_OCR/blob/main/h.JPG)
![alt text](https://github.com/Tanay-27/HandWritten_OCR/blob/main/v.JPG)

These are the sum of values as mentioned along row or column. It is clearly observed that for each line and each word in a line there is a clear drop and absence. 
Using this the splits are made.
#### Histogram Splitting
In this technique, the sum of pixel values in each column is taken, whenever the character break exists, the sum of pixels of that area will be approximately 0.
This with careful tuning is being used for our purpose here.

## Character Recognition
A CNN has been made and trained on the NIST dataset which is a set of handwritten characters, only a part of it has been taken for use as as a whole it has huge amount of samples for each class. Due to computing limtations only a part of the daqtaset is considered, however this gives decent accuracy.



#Pls Note 
The repository is being updated and hence certain files have been taken down will be updated very soon
