# IMDB Exercise 2 - Potential Solution

```
import csv, requests, time
from bs4 import BeautifulSoup


def get_film_stats(url):
    r = requests.get(url)
    soup = BeautifulSoup(r.text, 'html.parser')
    film = {}

    title = soup.h1.get_text()
    summary_text = soup.find('div', class_='summary_text').get_text()
    rating = soup.find('span', itemprop='ratingValue').get_text()

    print(title) # you may want to print something as you process each film

    film['title'] = title
    film['summary'] = summary_text
    film['rating'] = rating

    return film


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


def main():
    urls = ['https://www.imdb.com/title/tt0451279/', 'https://www.imdb.com/title/tt5788792/']
    films = []

    for url in urls:
        time.sleep(5) # add a delay in our requests
        film = get_film_stats(url)
        films.append(film)

    create_films_csv(films)

    print('Done processing film URLs.')


if __name__ == "__main__":
    main()

```

## What might you want to work on next?

- Add error handling - if the request parsing BeautifulSoup, or creating file fails
- Make your script process the 'related films' on these web pages too
