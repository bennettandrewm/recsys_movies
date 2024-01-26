# Movie Recommendation System

![family_movie](images/family_movie.jpeg)

You pick the movie, I'll choose the restaurant...

## 1. Project Overview

Choosing movies can be a stressful, high-stakes endeavor for anyone. And while users get stuck in indecision, the social media and streaming platfrom lose engagement and eventually profit. Fortunately, this program is here to help. It provides movie recommendations for any new user, based on their movie preferences. The program asks the user to rate five random movies from the [MovieLens](https://grouplens.org/datasets/movielens/) database of almost 10,000 movies. Based on the ratings, the program utilizes a user-based collaborative filtering model from [surprise](https://surpriselib.com/) to provide five recommendations.

## 2. Business Case

With the vast entertainment options available, low engagement and user churn in any social media or streaming service can hurt profit. Considering that 20% of adults are indecisive and 67% of relationship agreements never get resolved, picking a movie can be a daunting task, fueling decision paralysis and disengagement. Luckily, machine learning can relieve indecision by providing recommendations for any user, based on their preferences.


## 3. Github Repository

To execute this project, a github repository is utilized for public viewing and collaboration

You can see the following files stored in the github repository.

* *data* <a id='data'></a> - Folder containg the Movielens(100k ratings) files
    * [links.csv](data/links.csv)
    * [movies.csv](data/movies.csv)
    * [ratings.csv](data/ratings.csv)
    * [tags.csv](data/tags.csv)

* *Images* - Folder containing the image files used in the Notebook, Presentation, and README file

* *PDFs* - Folder containing pdf files below 
    * [Presentation](pdfs/Presentation.pdf) - Non-technical presentation of the Analysis
    * [Movie Recommendation Systems Notebook](pdfs/Notebook.pdf) - complete Jupyter Python Notebook in pdf form
            
* [README](README.md) the currently file you're reading with descriptions about the coding file

* [.gitignore](.gitignore) - git ignore file 

* [Movie Recommendation Systems Notebook](movie_recommendation_system.ipynb) - Notebook with Python analysis

## 4. Data Approach

### The Data
The program gets a user to rate five random movies from an existing database, and then returns five recommendations. It utilizes the [ratings.csv](data/ratings.csv) file from the [Movielens 100K ratings](#data) database, as described above, containing movie ratings (0.5-5) on thousands of movies from hundreds of users. The program uses a collaborative filtering model - no content-based or hybrid filtering was performed. Specifically, it relies on the model's ability to predict how any user would rate any movie. The `surprise` module is well suited for explicit ratings system with collaborative filter.

The approach can be summarized as follows:

* Step 1: Prior to input from the new user, we create a user-based collaborative filtering prediction model to predict how an existing user would rate a movie from the database. A few different models were attempted, but a model-based, single value decompisition method was selected.
* Step 2: Prompt user to rate five movies.
* Step 3: Add user's rating to the existing database
* Step 4: Use the model from step 1 to make predictions for how new users movie would rate (0-5) for all movies in the database and make a list
* Step 5: Output the top 5 recommendations 

### Source Data 
This project uses the Movielens dataset from the [GroupLens](https://grouplens.org/datasets/movielens/) lab at the University of Minnesota, which can be found in in the [`data`](#data) folder in this GitHub repository. 

The website notes that "This dataset (ml-latest-small) describes 5-star rating and free-text tagging activity from MovieLens, a movie recommendation service. It contains 100836 ratings and 3683 tag applications across 9,742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018. Users were selected at random for inclusion. All selected users had rated at least 20 movies. No demographic information is included. Each user is represented by an id, and no other information is provided."

The data are contained in the following files:

* [links.csv](data/links.csv)
* [movies.csv](data/movies.csv)
* [ratings.csv](data/ratings.csv)
* [tags.csv](data/tags.csv)


## 5. Modeling

To determine the best collaborative filtering model, multiple iterations were performed utilizing the `surprise` module's built-in capabilities. The metric for evaluation was Root Mean Square Error (RMSE). Considering that the scale is (0-5), we're probably hoping for something less than 1, and maybe even within 0.5.

But first, we created two baselines models of random selections and determined the RSME for those. One will be just picking a rating (0.0-5.0) at random. The other will assume the rating is just the median rating of the entire set.

After that, we utilized the `surpise` method to test SVD with GridSearch, KNNBasic, and KNNBaseline, with appropriate cross-validation. KNNBasic and KNNBaseline hyperparameters were tested manually, alternating between pearson/cosine similarities and user/item based similarities. 

The method with the lowest RMSE (0.859) was a user-based, SVD with tuned hyperparameters {n_factors=150, n_epochs=25, lr_all=0.010, reg_all=0.05}.


## 6. Sample Input/Output

So... the moment of truth. Did the model work? Or even worse, do I have bad tase in movies?

### Sample input
Some input below. You can see I've rated a John Mulaney comedy highly. The CHiPs movie? Not so much.

![input](images/input.png)

### Output

![output](images/output.png)

The output is spot on. I love four out of five of these movies. And I've never seen No. 4. Maybe I'll stream it tonight!


## 7. Summary

We were able to create a movie recommendation system that could help with user indecision to boost engagement on streaming platforms. Our system created a model using collaborative filtering on explicit ratings using the `suprise` module. We got an average accuracy of less than a point, and were able to successfully pick some movies for *this* developer to watch this weekend!







