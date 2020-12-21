# HandWritten_OCR
Handwritten Character Recognition using NIST dataset
Need - Currently available OCR Engines do not work correctly identify handwritten characters effectivetly. The necessity for a free and open source package that can be implemented easily within another application lead to the development of this project.
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
As seen from the above images, the ratio of width wrt height is made to split the segmented ROIs into words and subsequently characters. This needs to be done extremely carefully.

## Character Recognition
A CNN has been made and trained on the NIST dataset which is a set of handwritten characters, only a part of it has been taken for use as as a whole it has huge amount of samples for each class. Due to computing limtations only a part of the daqtaset is considered, however this gives decent accuracy.

Credits-
Vassilis Katsouros and Vassilis Papavassiliou, SEGMENTATION OF HANDWRITTEN DOCUMENT IMAGES INTO TEXT LINES, 
Institute for Language and Speech Processing/R.C. “Athena” Greece

Agrawal, N., & Kaur, A. (2018), AN ALGORITHMIC APPROACH FOR TEXT RECOGNITION FROM PRINTED/TYPED TEXT IMAGES,
2018 8th International Conference on Cloud Computing, Data Science & Engineering (Confluence)

Text Line Segmentation Based on Morphology and Histogram Projection 
Rodolfo P. dos Santos, Gabriela S. Clemente, Tsang Ing Ren and George D.C. Calvalcanti Center of Informatics, 
Federal University of Pernambuco Recife, PE, Brazil - www.cin.ufpe.br/~viisar

#Pls Note 
The repository is being updated and hence certain files have been taken down will be updated very soon
