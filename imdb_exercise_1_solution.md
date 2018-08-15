# IMDB Exercise 1 - Solution

```
import requests
from bs4 import BeautifulSoup

r = requests.get('https://www.imdb.com/title/tt0451279/')
soup = BeautifulSoup(r.text, 'html.parser')

title = soup.h1.get_text()
summary = soup.find('div', class_='summary_text').get_text()
rating = soup.find('span', itemprop='ratingValue').get_text()

print('Title: {}'.format(title)) # if using python 2, just print 'Title {}'.format(title) will work
print('Summary: {}'.format(summary))
print('Rating: {}'.format(rating))
```

Note: You may have different syntax, that's ok too! There are many ways to query a BeautifulSoup object.