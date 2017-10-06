# Metacritic Webscrape & PC Title Recommender

This is a PC game recommender system using python, beautiful soup, scikit-learn, and pandas. My current model runs on scraped data from Metacritic's website using user and critic reviews to suggest game titles based on the user's input. There are a few bugs, but I am currently working to work these out. If you would like to test the model please run the Part IV of the recommender.

## How it Works...

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
Once the user has supplied a list of game titles they have played previously. Their results will be fed into the dataset. After that, their entry is saved and the dataset will be turned into a sparse matrix. I will then use the review scores as cordinates for a nearest neighbors regressor which will find reviewers who have played the same or similar game titles in the dataset. Recommendations will be pulled from the games that other reviewers have played but the user has not.

```python

# I put the pivotsparse in NearestNeighbors and checked the for the closest neighbors around user_id (watevs).

X = pivotsparse
nbrs = NearestNeighbors(n_neighbors=7).fit(X) #6
distances, indices = nbrs.kneighbors(pivotsparse[nameIndex]) #We put latest users 'nameIndex' in the sparse index


# The most similar users in the dataframe
print distances
print "-"*20
print indices
```
```
[[  0.          18.          18.08314132  18.27566688  18.52025918
   18.70828693  18.70828693]]
--------------------
[[6169 3485 2153 4188 2574 5268 4801]]
```

The numbers at the top represent the distance of similarity between the nearest reviewers with selections closets to the user input. The numbers below are index references for those reviewrs

### The Final Results
The results will be returned like so...

```
Hello Keith Strmiska.

Here are your Reviews:
------------------------------------------------------------
title
DOOM (PC)                              10.0
Heroes of the Storm (PC)                9.0
League of Legends (PC)                  8.0
Dota 2 (PC)                             8.0
Call of Duty: Modern Warfare 3 (PC)     7.0
Name: 6169, dtype: float64

************************************************************
Here are a few recommendations from similar gamers!
************************************************************

Binary Domain (PC)
Crysis 2 (PC)
The Elder Scrolls V: Skyrim (PC)
Call of Duty: Advanced Warfare (PC)
Diablo III: Reaper of Souls (PC)
Fallout 4 (PC)
BioShock Infinite (PC)
Grand Theft Auto IV (PC)
Battlefield 3 (PC)
Rage (PC)
Fallout 4 (PC)
Hearts of Iron IV (PC)
The Elder Scrolls V: Skyrim (PC)
Deadfall Adventures (PC)
Narcosis (PC)
Thief (PC)
```


For more information on this project please visit my blog:
https://keithstrmiska.com/
