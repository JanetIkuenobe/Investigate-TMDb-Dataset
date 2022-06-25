# Project Title
### Investigate-TMDb-Dataset

# Project Description
### This data set contains information about 10,000 movies collected from The Movie Database (TMDb), including user ratings and revenue.The information includes some basic information about the movie like the title, cast, and director, and other relevant statistics such as popularity, budget, and revenue, vote count and vote average.

#### This project help to answer some questions like:
##### Which movie genres are most popular from year to year?
##### What kinds of properties are associated with movies that have high revenues?

# How To Use This Project
#### First import some libaries of Python including Numpy, Pandas, and Matplotlib to be used for this project.
##### import pandas as pd
##### import numpy as np
##### import matplotlib.pyplot as plt
##### import seaborn as snb
##### %matplotlib inline 

#### Load the data, check for cleanliness, and then trim and clean dataset for analysis
###### loading data and print a few lines. Perform operations to inspect
###### data types and look for instances of missing or possibly errant data
##### df = pd.read_csv('tmdb-movie.csv')
##### df.head()

#### check for missing data and remove missing data
##### df.isnull().any().sum()

#### check for duplication data and remove duplicate
##### df.duplicated().sum()

### Which movie genres are most popular from year to year?
###### First remove Null values from genres column
##### df = df.dropna(subset=['genres'], axis=0)
##### df.info()

#### Copy movie genres to a new dataframe, split the genres columns, create each row for each movie genre and perform the calculation
##### copy a new dataframe 
###### df1 = df.copy()
###### convert genres datatype to string
###### df1.genres = df1.genres.astype('str')

#####  split the genres string
###### df1.genres = df1.genres.str.split('|')
###### df1.head()

##### create genre list( create each row for each gen) using explode 
###### df1 = df1.explode('genres')
###### df1.describe()

##### calculating popularity of each genres for each years
###### genres_count = df1.groupby(['release_year','genres'], as_index=False)['popularity'].mean()
###### genres_count.head()

##### Select the most popular genre for each year
###### df_most_pop_genre = df1.groupby('release_year', as_index=False).apply(func).reset_index(drop=True)
###### df_most_pop_genre.head(5)

##### Draw the scatterplot to show the change of the most popular genre
###### plt.scatter(df_most_pop.release_year, df_most_pop.genres)
###### plt.title('The change of the most popular genre over the year')
###### plt.xlabel('Year')
###### plt.ylabel('Genre')

###### plt.show()



##### Draw the pie chart of genres
###### sizes = df_most_pop_genre.genres.value_counts().values
###### labels = df_most_pop_genre.genres.value_counts().index

###### fig1, ax1 = plt.subplots()
###### ax1.pie(sizes, labels=labels, autopct='%1.1f%%')
###### ax1.axis('equal')
###### plt.title('The percentage of each genre')

###### plt.show()

