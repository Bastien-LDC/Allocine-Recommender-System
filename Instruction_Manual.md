# 🎦 **AlloCiné Movies and Series Recommender System: Instruction Manual** 📖🎬

After having installed the environment and the dependencies, you can start the recommender system by running the following notebooks:


## 🌍**Web Scraping**📄
For both [movies](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Movies_From_AlloCine.ipynb) and [series](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Series_From_AlloCine.ipynb), as well as the [ratings](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Ratings_From_AlloCine.ipynb) scraping notebooks:
- Run the `"Import Libs"` cell. Make sure every library is installed correctly and available in your environment.
- Run all `"Functions"` cells.
- In the `"Launching the script"` part:
    - for **movies** and **series**: select the parameters values you want to use for the scraping (`start_page`, `end_page`, `nb_pages`) before running the next cells.
    - for **ratings**: reload the movies and series dataframes. Set the parameters of the `getCommentsUrl(...)` function and run it. Run the `"Loading the comments section urls"` cells. You can choose what you want to load (`movies`, `series`, `movies+series`, `user`, `press`, `user+press`) before running the next cells. This allows you to load only the urls you want before scraping the ratings. Finally, enter the number of maximum users you want to load (`nb_users`) for each item, the number of folds to split the movies and series urls and the fold number you want to start with (`fold_start`) (in case the script shuts down to a certain fold, you can pick it up to the last fold and not run everything again).

For more details, see the [Technical Report](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Docs/Recommender_System_-_Technical_report.pdf).

## 📊**Data Analysis**📉
In this [notebook](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Data%20Analysis/Allocine_Data_Analysis.ipynb):
- Run the `"Import Libs"` cell. Make sure every library is installed correctly and available in your environment.
- Change the file path of the dataframes in the `load_csv(...)` function. Personally, I manually renamed and placed all the final CSV dataframes in the `Saved Data` folder so that they are not altered by another run of the scraping scripts. 
- Finally, you can run all the cells chronologically.

## 🎯**Recommendation System**📚
In this [notebook](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Recommendation/Allocine_Recommender_System.ipynb):
- Run the `"Import Libs"` cell. Make sure every library is installed correctly and available in your environment.
- Run all the `"Functions"` cells starting from the `"Loading the csv files"` cell to the `"Model CB N°1"` cell excluded.
- For **Content-Based**:
    - Unwrap the cells of the model you'd like to use and run them one by one.
    - You can try change the parameters of the functions to see how the model performs.
    - For some models, some cells were duplicated with slight parameters changes to compare the results of different models.
    - Some plots were made for **`Model CB N°3`** and **`Model CB N°4`** to compare the results of the models.
    - For **`Model CB N°4`**, it is possible to save the models predictions into dataframes that can be used for the model comparison at the end of the notebook.
- For **Collaborative Filtering**:
    - You can run the `"Plots"` cells to see the sparsity and long tail of our database (optional).
    - Run the `"Functions"` cells.
    - For the **`Model CF N°1`**, you can execute the model in the `Model` section as well as the RMSE and MAE of the model in the `Metrics` section. It is possible to save the models predictions into dataframes that can be used for the model comparison at the end of the notebook.
    - For the **`Model CF N°2`**, first define the sparse data variable for the model. Secondly, estimate the best parameters of the SVD algorithm with Cross-Validation and Grid Search. Then, run the model with the best parameters. Finally, print the top *n* predictions of the model for each user. 
    - In the end, you can compare the results of most of the computed models so far with the `"Models' Analysis"` part.

****Note***📝: There was some issues regarding the installation of the `surprise` and `recmetrics` packages. Both couldn't coexist in the same environment as `surprise` was only successfully installed in a `conda` environment, and that `recmetrics` was only available on Python. Therefore, the last part of the Collaborative-Filtering chapter was semi-compromised as not every cell of the notebook can be executed, so error about **missing packages** and **undefined functions** will occur. Until both dependencies can be installed in the same environment, a temporary CSV file has been saved, resulting from the computation of the SVD model using `surprise`. I contains the user ids, movie ids, the actual rating and the predicted ratings of the model. This dataset can be used as it is in the `models_analysis(...)` function.*