# IMDB Exercise 2

Let's take our scraping code and put it in a file that we can call from the command line.

## Creating a file

Go to your command line terminal. (If you have a python shell open, type `quit()` to exit, or open a new terminal window)

In your command line terminal, type `touch imdb_scraper.py` to create a new python file named `imdb_scraper`.

We’ll be able to run this script by typing `python imdb_scraper.py` in command line.
But first we need to add our code to it.

Type `open imdb_scraper.py` (or use the text editor of your choice) to edit the file.

Here is some boilerplate python script code.

```
import requests
from bs4 import BeautifulSoup


def get_film_stats(url):
    # Put your HTTP request and Beautiful Soup logic here
    # Make it print the film’s title, summary and rating


def main():
    urls = ['https://www.imdb.com/title/tt0451279']

    for url in urls:
        get_film_stats('https://www.imdb.com/title/tt0451279')


if __name__ == "__main__":
    main()
```

Let's update that function to get our film information from IMDB and return a dictionary of film stats.
Then we'll print the dictionary in our main function.

```
import requests
from bs4 import BeautifulSoup

def get_film_stats(url):
    film_dictionary = {}

    r = requests.get('https://www.imdb.com/title/tt0451279/')
    soup = BeautifulSoup(r.text, 'html.parser')

    title = soup.h1.get_text()
    summary = soup.find('div', class_='summary_text').get_text()
    rating = soup.find('span', itemprop='ratingValue').get_text()

    film_dictionary['title'] = title
    film_dictionary['summary'] = summary
    film_dictionary['rating'] = rating

    return film_dictionary


def main():
    url = 'https://www.imdb.com/title/tt0451279'

    film_stats = get_film_stats(url)
    print(film_stats)


if __name__ == "__main__":
    main()
```

Save the file and try running it from the command line by typing `python imdb_scraper.py`

You should still see it print to the screen!

## Make it save to a csv instead of printing

In python, we can import the `csv` module to read or write to a CSV (comma separated value) file.

We can write to a new csv file (and create that file if it does not exist) with the following function that
takes some film stats.

```
def create_film_stats_csv(films):
    # write to a csv called film_stats.csv

    with open("film_stats.csv", "a") as f:
    writer = csv.writer(f)
    writer.writerow(['title', 'summary', 'rating']) # create the titles of the csv columns

    for film in films:
        # add the film's title, summary, rating to the csv
        writer.writerow([[film['title'], film['summary'], film['rating']])
```

### Can you update our `imdb_scraper.py` file above so that it does the following:

- Get the film stats from more than one URL (Don't forget: `import time` and use `time.delay(5)` to space out your requests)
- Add the film_stats dictionary to a list each time we get them from a new film
- Write all of the film stats to a csv once we are done with all of the URLs





