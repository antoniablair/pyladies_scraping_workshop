# IMDB Exercise 2 - Potential Solution

```
import csv, requests, time
from bs4 import BeautifulSoup


def get_film_stats(url):
    r = requests.get(url)
    soup = BeautifulSoup(r.text, "html.parser")
    film_dictionary = {}

    title = soup.h1.get_text()
    summary_text = soup.find('div', class_='summary_text').get_text()
    rating = soup.find('span', itemprop='ratingValue').get_text()

    print(title)

    film_dictionary['title'] = title
    film_dictionary['summary'] = summary_text
    film_dictionary['rating'] = rating

    return film_dictionary


def main():
    urls = ['https://www.imdb.com/title/tt0451279/', 'https://www.imdb.com/title/tt5788792/?ref_=nv_sr_1', 'https://www.imdb.com/title/tt2372162/']
    films = []

    for url in urls:
        time.sleep(5) # add a delay in our requests
        film_stats = get_film_stats(url)
        films.append(film_stats)

    with open("film_stats.csv", "a") as f:
        writer = csv.writer(f)
        writer.writerow(['title', 'summary', 'rating'])

        for film in films:
            writer.writerow([film['title'], film['summary'], film['rating']])

    print('Done processing film URLs.')


if __name__ == "__main__":
    # the script is being run directly, so run the main() function
    main()
```

## What might you want to work on next?

- Add error handling - if the request fails or parsing BeautifulSoup fails
- Make your script process the 'related films' on these web pages too
