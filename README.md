# Genre Prediction Project
This is a project to predict the genre of songs using data analysis and machine learning.

## Collaborators  
- Daniel Tan Teck Wee (@DanielTanTWOfficial)
- Daryl Tang Jun Da (@Daryl-10)
- Choo Zhen Hui (@wewechoo)

## Contents  
1. [Motivation](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#motivation)
2. [Sample Collection](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#sample-collection)
3. [Problem Statement](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#problem-statement)
4. [Exploratory Data Analysis/Pattern Recognition](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#exploratory-data-analysispattern-recognition)
5. [Data Cleaning](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#data-cleaning)
6. [Initial Model Building & Testing](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#initial-model-building--testing)
7. [90 Percent Model Building & Testing](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#90-percent-model-building--testing)
8. [Final Model Building & Testing](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#final-model-building--testing)
9. [Lessons From Model Development](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#lessons-from-model-development)
10. [Business Use Case](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#business-use-case)
11. [Overall Learning Points](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#overall-learning-points)
12. [Instructions to Run Code](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#instructions-to-run-code)
13. [List of Files](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#list-of-files-with-descriptions)
    - [Data Files](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#data-files-located-in-the-data-folder)
    - [Model Files](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#model-files-located-in-the-models-folder)
    - [Notebook Files](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#notebook-files)
    - [Dataset Sources](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#dataset-sources)
14. [References :hearts:](https://github.com/DanielTanTWOfficial/song-popularity-analysis/edit/main/README.md#references-hearts)

## Motivation
Music :musical_note: is all around us! :musical_note:  
On Spotify alone, there are over 82 MILLION tracks on the platform :scream:, with over 5,818 unique song genres. :astonished:  
Being able to identify the genres of all these different songs therefore is a neat data analytics :computer: challenge, and opens up a world of potential use cases.

## Sample Collection
To start off, we need data :page_with_curl:, lots of it!  
In this project, we went with the [Spotify Music Dataset](data/genre_songs.csv), which is a compilation of 41,099 songs, along with their genres (EDM, Latin, Pop, R&B, Rap and Rock) and music characteristics such as Danceability, Liveness, Energy and Speechiness, among others.

## Problem Statement  
What are the defining characteristics of a particular genre that makes them unique? :triangular_flag_on_post:  
Can we accurately predict the genre of songs based on these characteristics? :dart:  

## Exploratory Data Analysis/Pattern Recognition
First, we performed [Exploratory Data Analysis](EDA%20-%20Characteristics%20of%20Genre.ipynb) on the data we had to gain a better understanding of the data, and to find patterns, if any, among the music characteristics.  
The goal was to discover:
    - What do the variables mean?
    - How do they help us in our analysis?

## Data Cleaning
In order to prepare the data to be used for training :muscle: of our model, we had to perform :star: [Data Cleaning](Data%20Cleaning.ipynb) :star:.  
This involved removing duplicate entries from the dataset.

## Initial Model Building & Testing
As this is a multi-class classification problem, we chose to go with the Multi-Layer Perceptron Neural Network to predict the genres.  
For our model, we used sklearn's MLPClassifier.  
In the design of the [initial model](Initial_Model.ipynb), as there was no clear correlation between any song characteristic and genre, we used most of the numeric variables as predictor variables. In order to let the classifier identify the genres we used LabelEncoder from sklearn to label the genres from 0 - 5. Furthermore, as the predictor values had varying ranges, we used sklearn's MinMaxScaler to scale the values to be between 0 - 1.  

Finally, as there were an imbalanced ratio of samples of Pop and R&B songs to Latin, Rap and Rock, we used StratifiedShuffleSplit instead of TrainTestSplit with an 80:20 train to test ratio to more evenly balance out the number of samples from each genre.  

The initial model's prediction accuracy was very bad, and as can be seen from the confusion matrices, it kept classifying all genres of songs into a single class. This was a result of using a batch size which was too large, which resulted in the model not being able to separate the individual genres.  

P.S. Run the file [Initial_Model_Test.ipynb](Initial_Model_Test.ipynb) to skip retraining the model from scratch!  

## 90 Percent Model Building & Testing
To improve on the initial model, we modified the parameters of the model. We increased the number of neurons in each hidden layer and the number of hidden layers, increased the maximum iterations value for linear regression, and reduced the batch size to 10, in the hopes of better separating the songs of different genres.  

These parameter modifications paid off, and the [new model](90pct_Model.ipynb) had a prediction accuracy of 90% on the train set and 91% on the test set, which was a great improvement from the previous model. However, we felt we could still do better, as the current model was still incorrectly classifying a lot of the genres.  

P.S. Run the file [90pct_Model_Test.ipynb](90pct_Model_Test.ipynb) to skip retraining the model from scratch!  

## Final Model Building & Testing
The problem with the 90 percent model was that it was incorrectly predicting many genres, which suggested that there were too many overlapping predictor variable values among the genres for the model to efficiently differentiate between different genres confidently.

Performing [pattern recognition](Genre%20Clustering%20Analysis.ipynb) on the most incorrectly predicted genres, we created a shortlist of the most unique characteristics of each genre. For example, Latin songs are most commonly predicted wrongly as Pop, and from analysis of the scatter plots, we find that we can identify Latin music from Pop by the energy levels of the songs. Based on this shortlist, we then extracted only these unique variables and dropped all other variables which did not seem as important in identifying the genres.

With the refined predictor variables, the [final model](Final_Model.ipynb) improved greatly, with 99% prediction accuracy on the train set and 98% prediction accuracy on the test set.  

To test the accuracy of the final model, we brought in a separate test dataset. This dataset only contained songs with the genres of Pop, R&B and Rap. The accuracy of the model on this test set was 41%, which is reasonable. However, there is still much room for improvement, and perhaps training the model on an even larger dataset with more song samples would yield a better prediction accuracy.

P.S. Run the file [Final_Model_Test.ipynb](Final_Model_Test.ipynb) to skip retraining the model from scratch! 

## Lessons From Model Development
We went above and beyond the lessons learnt in class and gained new knowledge :books: through the model development process.  
Here's what we learnt:  
* We learnt how Feed Forward Neural Networks like Multi-Layer Perceptron Classifiers work to predict classes. :white_check_mark:  
* We learnt how to label encode categorical response variables to work with the classifier. :white_check_mark:  
* We learnt the importance of scaling predictor variables with MinMaxScaler. :white_check_mark:  
* We learnt how to deal with oversampled data through the use of stratified sampling. :white_check_mark:  
* We learnt the importance of batch sizes when dealing with stochastic gradient descent algorithms. :white_check_mark:  
* We learnt that model parameters such as hidden layer sizes and max iterations have an impact on prediction accuracy. :white_check_mark:  
* We learnt that although the model does a lot of the work, exploratory data analysis and pattern recognition to select the right predictor variables to feed the model is very important too! :white_check_mark:  

## Business Use Case
After the Pattern Recognition and Machine Learning stages, we are now equipped with knowledge that can be applied to Business Use Cases involving retail store owners.  
1. Increase foot traffic to stores by playing attractive music.  
2. Create playlists congruent with the goods being sold in the store to create an immersive environment unique to your store.  
3. Tailor music to influence customer behaviour within stores.
    * One study found that when background music was being played in the Women's Department, shoppers were more likely to make purchases and make more purchases compared to when foreground music was being played.
    * The same study found that when foregorund music was being played in the Men's department, shoppers would spend more and make more purchases compared to when background music was being played.  
    * In another study, higher consumer expenditure was observed when both Japanese-themed and Mexican-themed restaurants played a mixture of pop and the respective traditional music.
    * The same study found that diners preferred music to be played in the background with lower volume as their priority was to hold conversations while dining.

This opens up new research directions such as:
* Using music tracks to affect employee outcomes at retail stores. :convenience_store:  
* Crafting playlists to achieve various business goals. :chart_with_upwards_trend:  

## Overall Learning Points
1. Nuances in music can be identified with software performing Analog-to-Digital (ADC) conversion. :white_check_mark:  
2. Picked up the use of Mult-Layer Perceptron Neural Network. :white_check_mark:  
3. Applied the insights obtained from the Machine Learning model to real-world business use cases. :white_check_mark:  

## Instructions to Run Code
Run the Jupyter Notebook files using the Anaconda version of Jupyter.
In Anaconda Prompt, create a new environment with all the required packages installed with:  
`conda create --name <env_name> --file requirements.txt`  
In the directory the files are located in, execute `jupyter notebook` to start the Jupyter Notebook instance.

## List of files (With descriptions)

### Data Files (Located in the "data" folder)
1. genre_music.csv
    - The dataset selected to analyse correlation between music characteristics and genres.
2. genre_music_cleaned.csv
    - Cleaned dataset used to train the model.
3. genres_v2.csv
    - Extra dataset used to test the prediction accuracy of model.

### Model Files (Located in the "models" folder)
1. initial_model.sav
    - The initial model.
2. 90pct_model.sav
    - The 90 percent accuracy model.
3. final_model.sav
    - The final model.

### Notebook Files
1. EDA -Characteristics of Genre.ipynb
    - Contains the codes for Exploratory Data Analysis.
2. Data Cleaning.ipynb
    - Contains the codes for data cleaning before data is used for model training.
3. Initial_Model_Test.ipynb
    - Contains the codes to load and test the prediction accuracy of the initial model on the train and test data.
4. Initial_Model.ipynb
    - Contains the codes used for the training of the initial model.
    - Saves the resulting model as initial_model.sav.
5. 90pct_Model_Test.ipynb
    - Contains the codes to load and test the prediction accuracy of the 90 percent model on the train and test data.
6. 90pct_Model.ipynb
    - Contains the codes used for the training of the 90 percent model.
    - Saves the resulting model as 90pct_model.sav.
7. Genre Clustering Analysis.ipynb
    - Contains the code used to plot the scatter plots of the music characteristics of the most incorrectly predicted genres.
    - This code is used to refine the predictor variables given to train the final model.
8. Final_Model_Test.ipynb
    - Contains the codes to load and test the prediction accuracy of the final model on the train and test data.
9. Final_Model.ipynb
    - Contains the codes used for the training of the final model.
    - Saves the resulting model as final_model.sav.
    
### Dataset Sources
1. genres.csv (https://www.kaggle.com/code/akiboy96/spotify-song-popularity-genre-exploration/data?select=knn_songs.csv)
2. genres_v2.csv (https://www.kaggle.com/mrmorj/dataset-of-songs-in-spotify?select=genres_v2.csv)

## References :hearts:
1. About Spotify. Spotify. (2022, February 2). Retrieved March 29, 2022, from https://newsroom.spotify.com/company-info/  
2. Mcdonald, G. (n.d.). Every noise at once. Every Noise at Once. Retrieved March 29, 2022, from https://everynoise.com/  
3. Aakash. (2020, October 2). Spotify genre joined. Kaggle. Retrieved March 29, 2022, from https://www.kaggle.com/datasets/akiboy96/spotify-genre-joined  
4. Yalch, R. F., & Spangenberg, E. (1993, January 1). >using store music for retail zoning: A field experiment: ACR. ACR North American Advances. Retrieved March 29, 2022, from https://www.acrwebsite.org/volumes/7531/volumes/v20/NA-20/full  
5. Choo, B. J.-K., Cheok, T.-S., Gunasegaran, D., Wan, K.-S., Quek, Y.-S., Tan, C. S.-L., Quek, B.-K., & Gan, S. K.-E. (2020, September 21). The sound of music on the pocket: A study of background music in retail. Sage Journals. Retrieved March 29, 2022, from https://journals.sagepub.com.remotexs.ntu.edu.sg/doi/10.1177/0305735620958472  
