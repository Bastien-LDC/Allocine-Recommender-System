# 🎦 **AlloCiné Movies and Series Recommender System** 🎬
## 📖 **Description**
AlloCiné is a company which provides information on French cinema and provide ratings from the press and from their users for a large number of movies and series. In this repository, we will scrape the website for movies and series data, as well as the ratings from the users that we will use to build a recommender system, based on the users' rating preferences.

---
## 🗃️ **The Data**

First, we had to webscrape the data from the AlloCiné website. As I was new in webscraping, I inspired myself by using [the deprecated script](https://github.com/ibmw/Allocine-project/blob/master/Webscraping%20From%20AlloCine.ipynb) of a project I found on GitHub made by [Olivier Maillot](https://github.com/ibmw/Allocine-project), as well as his module to retrieve the data from allociné [here](https://github.com/ibmw/allocine-dataset-scraper).

Therefore, I decided to fork the original project at first and build my own version of this webscraper. (I do not plan to do a pull request on the original project, as I don't want to change the original project, but only use it as reference.) But for ownership and privacy reasons due to my internship, I created my own repo and set its accessibility to private.

There are three notebooks used for webscraping the data from the AlloCiné website:
- [Webscraping_Movies_From_AlloCine.ipynb](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Movies_From_AlloCine.ipynb): for scraping the movies data.
- [Webscraping_Series_From_AlloCine.ipynb](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Series_From_AlloCine.ipynb): for scraping the series data.
- [Webscraping_Ratings_From_AlloCine.ipynb](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Ratings_From_AlloCine.ipynb): for scraping the ratings of the press and the user for each movie and series.

### 🧹**Data Cleaning**
After scraping all the data, we proceed to a first data analysis and cleaning process in this [notebook](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Data%20Analysis/Allocine_Data_Analysis.ipynb).

### 📝 **Description of the data**

The latest data is dated from **May 6th, 2022** to **May 14th, 2022** and it was scraped from the first **600 pages** of the movies and series sections.

If you are interested in it, the data from all the movies, series and ratings scraping is available here:
- Raw data:
    - [movies](https://storage.cloud.google.com/bucket-bastien/Saved%20Data/allocine_movies_600p.csv) (8026 movies including 7907 unique).
    - [series](https://storage.cloud.google.com/bucket-bastien/Saved%20Data/allocine_series_600p.csv) (8126 series including 8001 unique).
    - [press_ratings_movies](https://storage.cloud.google.com/bucket-bastien/Saved%20Data/press_ratings_movies_600p.csv).
    - [press_ratings_series](https://storage.cloud.google.com/bucket-bastien/Saved%20Data/press_ratings_series_600p.csv).
    - [user_ratings_movies](https://storage.cloud.google.com/bucket-bastien/Saved%20Data/user_ratings_movies_600p.csv).
    - [user_ratings_series](https://storage.cloud.google.com/bucket-bastien/Saved%20Data/user_ratings_series_600p.csv).

- Cleaned data:
    - [movies](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/movies.csv).
    - [series](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/series.csv).
    - [press_movies](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/press_movies.csv).
    - [press_series](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/press_series.csv).
    - [user_movies](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/user_movies.csv).
    - [user_series](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/user_series.csv).

- Additional data:
    - [movies_genres](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/m_genres.csv).
    - [series_genres](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/s_genres.csv).
    - [movies_nationality](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/m_nationality.csv).
    - [series_nationality](https://storage.cloud.google.com/bucket-bastien/Cleaned%20Data/s_nationality.csv).

#### ℹ️ **The Movie Columns** 🎬:
For the **movies** data, we have the following columns :
- `id`: AlloCiné movie id
- `title`: the movie title (in French)
- `release_date`: the movie release date
- `duration`: the movie length (in minutes)
- `genres`: the movie genres (as a CSV string)
- `directors`: movie directors (as a CSV string)
- `actors`: main movie actors (as a CSV string)
- `nationality`: nationality of the movie (as a CSV string)
- `press_rating`: average press rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `nb_press_rating`: number of ratings made by the press
- `spect_rating`: average AlloCiné users rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `nb_spect_rating`: number of ratings made by the users/spectators
- `summary`: the movie summary (in French)
- `poster_link`: url of the movie poster

#### ℹ️ **The Series Columns** 📺:
For the **series** data, we have the following columns :
- `id`: AlloCiné series id
- `title`: the series title (in French)
- `status`: the series status (in French) (En cours|Terminée|Annulée|À venir)
- `release_date`: the series release date
- `duration`: the series average episode length (in minutes)
- `nb_seasons`: the number of seasons
- `nb_episodes`: the number of episodes
- `genres`: the series genres (as a CSV string)
- `directors`: series directors (as a CSV string)
- `actors`: main actors of the series (as a CSV string)
- `nationality`: nationality of the series (as a CSV string)
- `press_rating`: average press rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `nb_press_rating`: number of ratings made by the press
- `spect_rating`: average AlloCiné users rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `nb_spect_rating`: number of ratings made by the users/spectators
- `summary`: the series summary in French
- `poster_link`: url of the series poster

#### ℹ️ **The Ratings Columns** 🏆:
To simplify the scraping of the ratings, I had to break it down into 4 different files/dataframes:
- `press_series_ratings`: contains the ratings made by the press for the series
- `press_movies_ratings`: contains the ratings made by the press for the movies
- `user_series_ratings`: contains the ratings made by the users/spectators for the series
- `user_movies_ratings`: contains the ratings made by the users/spectators for the movies

All of these dataframes have the similar following columns:
- `user_id`: AlloCiné user id (unavailable for the press)
- `(user/press)_name`: AlloCiné user/press name
- `(movie/series)_id`: AlloCiné movie/series id
- `(user/press)_rating`: AlloCiné user/press rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `date`: date of the rating (unavailable for the press)

#### ℹ️ **The Genres Columns** 🎭:
The **genres** dataframe is the same for the movies and the series. It contains the following columns :
- `genres` : the genre name
- `nb_(movies/series)` : number of movies/series in this genre
- `avg_duration` : average duration of the movies/series in this genre
- `median_duration` : median duration of the movies/series in this genre
- `nb_press_rating` : number of ratings made by the press in this genre
- `nb_user_rating` : number of ratings made by the users/spectators in this genre
- `total_rating` : total rating made by the press and users in this genre
- `press_rating_percentage` : percentage of the total rating made by the press in this genre
- `user_rating_percentage` : percentage of the total rating made by the users/spectators in this genre
- `(movies/series)_percentage` : percentage of the total number of movies/series in this genre

#### ℹ️ **The Nationality Columns** 🌍:
The **nationality** dataframe is built the same way as the **genres** one mentioned above, except that it lacks the `avg_duration` and `median_duration` per nationality.



---
## 🚀 **Getting Started**

First, we need to install the dependencies in the *requirements.txt* file.
```bash
pip install -r requirements.txt
```
Then, we can start the webscraping scripts for movies and series, in the *Webscraping* folder. You can choose for each script the number of pages to scrape, at the rate of 15 movies/series per page. All generated *.csv* files will be stored in the *Data* folder in the *Movies* and *Series* sections.

After that, we can get the urls of the press and users comments sections for each movie and series we retrieved, before starting the scraping process for the ratings. All generated *.csv* files will be stored in the *Ratings* folder in the *Movies* and *Series* sections.
  
*📝Note: for the user ratings, we choose the keep the 50 first users with the most number of reviews for each movie/series. This will increase our chances to find a user multiple times, as we need to get several ratings from the same user in order to create a user profile for our recommender system.*

(⚠️ **Warning** ⚠️: the process can take a while, depending on the number of pages you choose to scrape. It is recommended to use a dedicated computer for this process, as it can take a long time to complete.)


## 👥 **Authors**

* **Olivier Maillot** - *Reference Project* - [AlloCiné Project](https://github.com/ibmw/Allocine-project) - [Blog Post](http://wp.me/p8Ffnw-4U)
* **Bastien LEDUC** - *Webscraping and Recommender System* - [AlloCiné Recommender System](https://github.com/Bastien-LDC/Allocine-Recommender-System)

## 🧑‍🤝‍🧑 **Other Analysis**
* [Camille2T Analysis](https://github.com/Camille2T/Movies_ratings_allocine)

# 📄 **Licence**

This project is part of my internship mission at [AVISIA](https://www.avisia.fr/), a Consulting firm in Data, Digital & Technology.