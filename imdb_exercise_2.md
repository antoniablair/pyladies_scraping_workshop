# IMDB Exercise 2

Let's take our scraping code and put it in a file that we can call from the command line.
Then, we'll make it output to a CSV!

## Creating a file

Make a new file called `imdb_scraper.py`. You can do this in command line by typing `touch imdb_scraper.py`

When we are in the same directory as the file, we’ll be able to run this script by typing `python imdb_scraper.py` in command line.
But first we need to add our code.

Type `open imdb_scraper.py` (or use the text editor of your choice) to edit the file.

## Make a basic python script

Here is some boilerplate python code.

```
import requests
from bs4 import BeautifulSoup


def get_film_stats(url):
    # Put your HTTP request and Beautiful Soup logic here
    # Make it print the film’s title, summary and rating


def main():
    url = 'https://www.imdb.com/title/tt0451279'

    get_film_stats(url)


if __name__ == "__main__":
    main()
```

## Get our film information

Go ahead and update the `get_film_stats` function above to get our film information from IMDB and return a dictionary with the film's details.

```
def get_film_stats(url):
    r = requests.get(url)
    soup = BeautifulSoup(r.text, "html.parser")
    film = {}

    title = soup.h1.get_text()
    summary_text = soup.find('div', class_='summary_text').get_text()
    rating = soup.find('span', itemprop='ratingValue').get_text()

    film['title'] = title
    film['summary'] = summary_text
    film['rating'] = rating

    return film
```

Then we'll update our `main()` method to get and print the dictionary.

```
def main():
    url = 'https://www.imdb.com/title/tt0451279'

    film = get_film_stats(url)
    print(film)
```

The file should now look like this:

```
import requests
from bs4 import BeautifulSoup

def get_film_stats(url):
    r = requests.get(url)
    soup = BeautifulSoup(r.text, 'html.parser')
    film = {}

    title = soup.h1.get_text()
    summary_text = soup.find('div', class_='summary_text').get_text()
    rating = soup.find('span', itemprop='ratingValue').get_text()

    film['title'] = title
    film['summary'] = summary_text
    film['rating'] = rating

    return film


def main():
    url = 'https://www.imdb.com/title/tt0451279'

    film = get_film_stats(url)
    print(film)


if __name__ == "__main__":
    main()
```

## Try running the file

Save the file and try running it from the command line by typing `python imdb_scraper.py`

You should still see it print to the screen, but in dictionary format!

```
{'title': 'Wonder Woman\xa0(2017) ', 'summary': '\n                    When a pilot crashes and tells of conflict in the outside world, Diana, an Amazonian warrior in training, leaves home to fight a war, discovering her full powers and true destiny.\n            ', 'rating': '7.5'}
```

## Make it save to a csv instead of printing

In python, we can import the csv module with `import csv` to read or write to a CSV (comma separated value) file.

We can write to a new csv file (and create that file if it does not exist) with the following function that
takes a list of film dictionary objects.

```
def create_films_csv(films):
    # write to a csv called film_stats.csv

    with open("film_stats.csv", "a") as f:
        writer = csv.writer(f)
        writer.writerow(['title', 'summary', 'rating']) # create the csv column titles

        for film in films:
            # add the film's title, summary, rating to the csv

            title = film['title'].encode('utf-8')
            summary = film['summary'].encode('utf-8')
            rating = film['rating'].encode('utf-8')

            writer.writerow([title, summary, rating])
```

### Can you update our `imdb_scraper.py` file above so that it does the following:

- Get the film stats from more than one URL (Don't forget: `import time` and use `time.delay(5)` to space out your requests)
- Add the film_stats dictionary to a list each time we get them from a new film
- `import csv`  and write all of the film stats to a csv once we are done with all of the URLs





