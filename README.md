# Movies_ETL

## Overview and Objectives

A lot of information about movies including the date of release and or production is stored in Wikipedia. This information can be extracted and stored as a JSON file. Presented with a JSON file containing information scraped from Wikipedia about different (genres of) movies from 1990 to 2018, the main objective of this project was to create a data pipeline to extract, transfrom and load (ETL) the data. In other words, the main aim of this project was to create one function that takes in three files — Wikipedia data, Kaggle metadata, and MovieLens rating data — and perform the ETL process by adding the data to a PostgreSQL database. 

## Resources
* Python 3.7.6, JupyterLab 2.26
* PostgreSQL 14, Pgadmin 5.1
* Movie Data (sourced from IMDB, Kaggle), wikipedia.movies.json

## Analysis and Results

###  Write an ETL Function to Read Three Data Files
1. A function to read in the three files was first created.
2. The Kaggle metadata and MovieLens ratings CSV files were read in as Pandas DataFrames.
3. The Wikipedia JSON file was loaded and the JSON data was converted to raw data.
4. A Pandas DataFrame was then created from the raw Wikipedia movie data
5. After reading the three DataFrames, a path to the Wikipedia data, the Kaggle metadata, and the MovieLens rating data files was created. 
6. The function, created in step 1, was then linked to these variables and the variables were reassigned.

    ** Results: The resulting dataframes can be viewed in the ETL_function_test.ipynb file.

### Extract and Transform the Wikipedia Data

1. A function called for the clean movie function that takes in the argument "movie" was created.
2. Tv shows were filtered out of the wiki_movies_raw file.
3. A list comprehension was written to iterate through the cleaned wiki movies list created in the previous step and a cleaned movies DataFrame was the created. 
4. A try-except block was written to catch errors while extracting the IMDb IDs and dropping duplicate IDs.
5. A list comprehension was written to keep the columns that have non-null values from the DataFrame created in the previous step and the a wiki_movies_df DataFrame was then created from the list.
6. All non-null values from the "Box office" column was assigned to a variable. This box office data was then converted to string values using the lambda and join functions.
7. Since the box office data was in different $ format two regex expression, "form one" and "form two", was created to convert the data in this column to a standard form. To do this, a regular expression to match the different elements of form_one and form_two of the box office data was written.
8. A parse_dollars() function was created to clean the box office column in the wiki_movies_df DataFrame using the form_one and form_two lists created.
9. Similarly, the budget column, the release date column and the running time column in the wiki_movies_df DataFrame was cleaned using regex expressions.
10. A path to the Wikipedia data, the Kaggle metadata, and the MovieLens rating data files was created using three variables.
11. The ETL function created was then linked to these variables and the variables were reassigned to the respective dataframes.

    ** Results - The full code and resulting DataFrames are displayed in the ETL_clean_wiki_movies.ipynb file.

### Extract and Transform the Kaggle Data

In general, the code created in the two previuos subsections was refractured. 

1. First, the ETL function created and the code from the subsection Extract and Transform the Wikipedia Data was again utilized at the beginning of this code.
2 A code was written to clean up the Kaggle metadata.
3.The wiki_movies_df DataFrame and the kaggle_metadata DataFrames was then merged to a new DataFrame, movies_df.
4. Unnecessary columns from the movies_df DataFrame was then dropped.
5. The fill_missing_kaggle_data() function that fills in the missing Kaggle data on the movies_df DataFrame was created.
6. This function was then called with the movies_df DataFrame and the Kaggle and Wikipedia columns to be cleaned as the arguments.
7. The movies_df DataFrame was then filtered to keep the necessary columns, and the columns in the movies_df DataFramewas then renamed.
8. The ratings DataFrame was then transformed and merged with the movies_df DataFrame, to create a new new DataFrame movies_with_ratings_df, which was then cleaned.
9. A path to the Wikipedia data, the Kaggle metadata, and the MovieLens rating data files was created using three variables.
11. The ETL function created was then linked to these variables and the variables were reassigned to the respective dataframes.

** Results - The full code and resulting DataFrames are displayed in the ETL_clean_kaggle_data.ipynb file.

### Create the Movie Database

The code in the previous subsection was modified with the following steps to complete this requirement.

1. A code was written to create a connection to the PostgreSQL database, then the movies_df DataFrame and ratings DataFrame was added to the SQL database.
2. A code that prints out the elapsed time to import each row was written.
3. After the program was completed, a query was written on the PostgreSQL database to retrieve the number of rows for the movies and ratings tables


## Results

The full code is displayed in the ETL_create_database.ipynb file, and the query results displaying the number of rows in the two tables are displayed as movies_query.png and ratings_query.png files in the Resources folder.
