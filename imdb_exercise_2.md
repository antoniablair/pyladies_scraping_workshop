# IMDB Exercise 2

## We're going to our scraping code and put it in a file that we can call from the command line.

### Creating a file

Go to your command line terminal. (If you have a python shell open, type `quit()` to exit, or open a new terminal window)

In your command line terminal, type `touch imdb_scraper.py` to create a new python file named `imdb_scraper`
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

Let's update it to get our film information from IMDB.

```
import requests
from bs4 import BeautifulSoup

def get_film_stats(url):
    title = soup.h1.get_text()
    summary = soup.find('div', class_='summary_text').get_text()
    rating = soup.find('span', itemprop='ratingValue').get_text()

    print('Title: {}'.format(title)) # if using python 2, just print 'Title {}'.format(title) will work
    print('Summary: {}'.format(summary))
    print('Rating: {}'.format(rating))


def main():
    url = 'https://www.imdb.com/title/tt0451279'

    get_film_stats(url)


if __name__ == "__main__":
    main()
```

Save the file and try running it from the command line by typing `python imdb_scraper.py`

You should still see the prints to the screen!

### Make it save to a csv instead of printing




