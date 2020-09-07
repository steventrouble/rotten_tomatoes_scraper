[![license](https://img.shields.io/badge/license-MIT-success)](https://github.com/pdrm83/Rotten_Tomatoes_Scraper/blob/master/LICENSE)

# Rotten Tomatoes Scraper 
You can extract information about movies and actors that are listed on the Rotten Tomatoes website using this module. 
Each movie has different metadata such as *Rating*, *Genre*, *Box Office*, *Studio*, and *Scores*. Note that the 
**Genre** has 20+ subcategories that also gives you more granular information on a movie. These metadata can be helpful 
for many data science projects. For actors you can extract movies listed in **highest-rated** or **filmography** 
sections depending on your need. I used the BeautifulSoup package to parse HTML documents obtained by the HTTP 
response in this library. 


## Library
The module requires the following libraries:

* bs4
* re
* requests
* urllib

## Install

It can be installed using pip:
```python
pip3 install rotten_tomatoes_scraper
```

## Usage
You can use this library to extract the complete list of movies that an actor played by calling `extract_metadata` 
method and using `section='filmography'`. Plus, you can also extract the list of top ranked movies by using the same
method and `section='highest'`. 

```python
from rotten_tomatoes_scraper.rt_scraper import CelebrityScraper

celebrity_scraper = CelebrityScraper('jack nicholson')
celebrity_scraper.extract_metadata(section='highest')
movie_titles = celebrity_scraper.metadata['movie_titles']

print(movie_titles)
['Kubrick by Kubrick (Kubrick par Kubrick)', 'On a Clear Day You Can See Forever', 'The Shooting']
```


If you want to find out what movie genres an actor has played in, you can, first, extract the list of movies that he or 
she participated in using `extract_movies` method. Then, you just need to feed in the list of movies to the `extract_genre` 
method to receive a dictionary that keys are movie genres and values are the number oof movies with that genre in which 
the actor played. You can easily use the code below.

```python
from rotten_tomatoes_scraper.rt_scraper import RTScraper

rts = RTScraper()
movie_titles = rts.extract_movies('meryl streep', section='highest')
movie_genres = rts.extract_genre(movie_titles)

print(movie_genres)
{'Documentary': 2, 'Comedy': 1, 'ScienceFiction&Fantasy': 1, 'Drama': 1, 'Romance': 1}
```

This library doesn't give you a full access to all the metadata that you may find in Rotten Tomatoes website. However,
you can easily use it to extract the most important ones.

And, that's pretty much it!

