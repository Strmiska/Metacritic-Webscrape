# Metacritic Webscrape & PC Title Recommender

This is a PC game recommender system using python, beautiful soup, scikit-learn, and pandas. My current model runs on scraped data from Metacritic's website using user and critic reviews to suggest game titles based on the user's input. There are a few bugs, but I am currently working to work these out.

## Example

A user will be prompted to feed in at least 4 PC game titles before the model will continue.

```python
while exit == False:
    
    results = []

    gamesearch = str(raw_input("Please enter a title to review: "))
    
    while len(results) > 1 or len(results) == 0:
        results = []

        for title in df['title'].unique():
            if re.search(gamesearch, title, re.IGNORECASE):
                results.append(title) #gather up the possible results...
```

For more information on this project please visit:
https://keithstrmiska.com/
