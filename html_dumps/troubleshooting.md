## Requests aren't working?

You can import the HTML manually instead from a text file. We'll pretend like it was from our response HTML body. 

```
import csv

with open ("pyladies.txt", "r") as myfile:
    data = myfile.readlines()

    pyladies_html = data[0]
```