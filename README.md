# Genre Prediction Project
Project to predict the genre of songs using data analysis and machine learning.

### Requirements to run
Run the Jupyter Notebook files using the Anaconda version of Jupyter.
In Anaconda Prompt, create a new environment with all the required packages installed with:  
`conda create --name <env_name> --file requirements.txt`  
In the directory the files are located in, execute `jupyter notebook` to start the Jupyter Notebook instance.

### List of files (With descriptions)

#### Data Files (Located in the "data" folder)
1. genre_music.csv
    - The dataset selected to analyse correlation between music characteristics and genres.
2. genre_music_cleaned.csv
    - Cleaned dataset used to train the model.
3. genres_v2.csv
    - Extra dataset used to test the prediction accuracy of model.

#### Model Files (Located in the "models" folder)
1. initial_model.sav
    - The initial model.
2. 90pct_model.sav
    - The 90 percent accuracy model.
3. final_model.sav
    - The final model.

#### Notebook Files
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
    
#### Dataset Sources
1. genres.csv (https://www.kaggle.com/code/akiboy96/spotify-song-popularity-genre-exploration/data?select=knn_songs.csv)
2. genres_v2.csv (https://www.kaggle.com/mrmorj/dataset-of-songs-in-spotify?select=genres_v2.csv)
