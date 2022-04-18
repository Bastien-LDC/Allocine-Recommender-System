# 🎦 **AlloCiné Movies and Series Recommender System** 🎬
## 📖 **Description**
AlloCiné is a company which provides information on French cinema and provide ratings from the press and from their users for a large number of movies and series. In this repository, we will scrape the website for movies and series data, as well as the ratings from the users that we will use to build a recommender system, based on the users' rating preferences.

## 🗃️ **The Data**

First, we had to webscrape the data from the AlloCiné website. As I was new in webscraping, I inspired myself by using [the deprecated script](https://github.com/ibmw/Allocine-project/blob/master/Webscraping%20From%20AlloCine.ipynb) of a project I found on GitHub made by [Olivier Maillot](https://github.com/ibmw/Allocine-project), as well as his module to retrieve the data from allociné [here](https://github.com/ibmw/allocine-dataset-scraper).

Therefore, I decided to fork the original project at first and build my own version of this webscraper. (I do not plan to do a pull request on the original project, as I don't want to change the original project, but only use it as reference.) But for ownership and privacy reasons due to my internship, I created my own repo and set its accessibility to private.

There are three notebooks used for webscraping the data from the AlloCiné website:
- [Webscraping_Movies_From_AlloCine.ipynb](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Movies_From_AlloCine.ipynb): for scraping the movies data.
- [Webscraping_Series_From_AlloCine.ipynb](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Series_From_AlloCine.ipynb): for scraping the series data.
- [Webscraping_Ratings_From_AlloCine.ipynb](https://github.com/Bastien-LDC/Allocine-Recommender-System/blob/master/Webscraping/Webscraping_Ratings_From_AlloCine.ipynb): for scraping the ratings of the press and the user for each movie and series.

### 📝 **Description of the data** **(TO EDIT)**

We provide the dataset in two version :
- A one csv files format (brut and clean versions) : [allocine_dataset.zip](http://olivier-maillot.fr/wp-content/uploads/2017/08/allocine_dataset.zip)
- A multiple csv files format (clean version only): [allocine_rel-dataset.zip](http://olivier-maillot.fr/wp-content/uploads/2017/08/allocine_rel-dataset.zip)

The brut file contains **59 966 movies**, but only **10 424 movies** have both press and users ratings.
If you decide to use the clean version, you directly start with the **10 424 movies** and if you decide to use the multiple csv files, you don't have to use ast library (see Getting Started).

#### ℹ️ **The Movie Columns** 🎬:
For the **movies** data, we have the following columns :
- `id` : AlloCiné movie id
- `title` : the movies title (in french)
- `release_date`: the release date
- `duration`: the movies length
- `genres` : the movies genres (as an array)
- `directors` : movies directors (as an array)
- `actors` : main movie actors (as an array)
- `nationality`: nationality of the movies (as an array)
- `press_rating`: average press rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `nb_press_rating`: number of ratings made by the press
- `spect_rating`: average AlloCiné users rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `nb_spect_rating`: number of ratings made by the users/spectators
- `summary`: the movies summary
- `poster_link`: url of the movies poster

#### ℹ️ **The Series Columns** 📺:
For the **series** data, we have the following columns :
- `id` : AlloCiné series id
- `title` : the series title (in french)
- `release_date`: the release date
- `duration`: the series average episode length
- `nb_seasons`: the number of seasons
- `nb_episodes`: the number of episodes
- `genres` : the series types (as an array)
- `directors` : series directors (as an array)
- `actors` : main actors of the series (as an array)
- `nationality`: nationality of the series (as an array)
- `press_rating`: average press rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `nb_press_rating`: number of ratings made by the press
- `spect_rating`: average AlloCiné users rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `nb_spect_rating`: number of ratings made by the users/spectators
- `summary`: short summary of the series in french
- `poster`: url of the series poster

#### ℹ️ **The Ratings Columns** 🏆:
To simplify the scraping of the ratings, I had to break it down into 4 different files/dataframes:
- `press_series_ratings`: contains the ratings made by the press for the series
- `press_movies_ratings`: contains the ratings made by the press for the movies
- `user_series_ratings`: contains the ratings made by the users/spectators for the series
- `user_movies_ratings`: contains the ratings made by the users/spectators for the movies

All of these dataframes have the following similar columns:
- `user_id`: AlloCiné user id (unavailable for the press)
- `(user/press)_name`: AlloCiné user/press name
- `(movie/series)_id`: AlloCiné movie/series id
- `(user/press)_rating`: AlloCiné user/press rating (from 0.5 to 5 stars ⭐⭐⭐⭐⭐)
- `date`: date of the rating (unavailable for the press)

### 🚀 **Getting Started**

First, we need to install the dependencies in the *requirements.txt* file.
```bash
pip install -r requirements.txt
```
Then, we can start the webscraping scripts for movies and series, in the *Webscraping* folder. You can choose for each script the number of pages to scrape, at the rate of 15 movies/series per page. All generated *.csv* files will be stored in the *Data* folder in the *Movies* and *Series* sections.

After that, we can get the urls of the press and users comments sections for each movie and series we retrieved, before starting the scraping process for the ratings. All generated *.csv* files will be stored in the *Ratings* folder in the *Movies* and *Series* sections.
  
*📝Note: for the user ratings, we choose the keep the 100 first users with the most number of reviews for each movie/series. This will increase our chances to find a user multiple times, as we need to get several ratings from the same user in order to create a user profile for our recommender system.*

(⚠️ **Warning** ⚠️: the process can take a while, depending on the number of pages you choose to scrape. It is recommended to use a dedicated computer for this process, as it can take a long time to complete.)


## 👥 **Authors**

* **Olivier Maillot** - *Reference Project* - [AlloCiné Project](https://github.com/ibmw/Allocine-project) - [Blog Post](http://wp.me/p8Ffnw-4U)
* **Bastien LEDUC** - *Webscraping and Recommender System* - [AlloCiné Recommender System](https://github.com/Bastien-LDC/Allocine-Recommender-System)

## 🧑‍🤝‍🧑 **Other Analysis**
* [Camille2T Analysis](https://github.com/Camille2T/Movies_ratings_allocine)

# 📄 **Licence**

This project is part of my internship mission at [AVISIA](https://www.avisia.fr/), a Consulting firm in Data, Digital & Technology.