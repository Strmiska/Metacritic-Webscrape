# Metacritic Webscrape & PC Title Recommender

This is a PC game recommender system using python, beautiful soup, scikit-learn, and pandas. My current model runs on scraped data from Metacritic's website using user and critic reviews to suggest game titles based on the user's input. There are a few bugs, but I am currently working to work these out.

## Example

A user will be prompted to feed in at least 4 PC game titles before the model will continue...

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

Once a title is chosen a user will be asked to give the title a score from 1-10. When the user is more critical with their review score (Not slapping 10's and 0's on everything) the model will return more accurate results. The user will be asked to do this for each title they chose.

```python
    # Get the user's score for the game
    loop = True
    while loop == True:
        score = int(raw_input("Please give the title a score from 0-10: "))
        if score >= 0 and score <=10:
            gamescore.append(score)
            loop = False
        else:
            loop = True
    
    # Ask if the users wants to stop adding games
    loop = True
    while loop == True:
        confirm = str(raw_input("Would you like to add another game? (y/n): "))
        if confirm == 'y' or confirm =='Y':
            exit = False
            loop = False
        elif confirm == 'n' or confirm =='N':
            exit = True
            loop = False
        else:
            loop = True
```
Once the user has supplied a list of game titles they have played previously. Their results will be fed into the dataset. Once their entry is saved the dataset will be turned into a sparse matrix.


For more information on this project please visit:
https://keithstrmiska.com/
