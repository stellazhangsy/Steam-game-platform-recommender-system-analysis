# Steam-game-platform-recommender-system-analysis-Using-Pyspark
![1591946337278](https://user-images.githubusercontent.com/57570355/84475990-57424000-ac42-11ea-9a54-1b3053c7266d.jpg)

For over 15 years, Steam has dominated the gaming industry. However, with other similar platforms emerging, it has been a very competitive market. In order for Steam to remain as the industry leader, we created a recommender system to help drive the sales and revenue by putting forward appropriate strategies to retain and reacquire churned customers.

Using the Steam game review data we scraped from the website(SteamAPI), we were able to look at the review sentiment and cluster / segment customers into 4 groups based on how much they have played and how many games they have bought. In addition to the segmentations, We also divided users into active and inactive based on play time and recent activity.

Our pitch deck can be found here: https://drive.google.com/file/d/1LrNnzTNxDh701TRyj5zrF9wItkz9vCKz/view?usp=sharing

## Data 
<img width="954" alt="WechatIMG132" src="https://user-images.githubusercontent.com/57570355/84474680-18ab8600-ac40-11ea-851b-5bad984626d3.png">

## Data Processiong 
### filter out targeted games
There are totally 91,925 games on Steam across hundreds of genres and we scraped all of them. Based on the following conditions, we narrowed our analysis scope to 7,808 games:
1. Games that are not free
2. Games that were released between 2000 - 2020
3. Games that have enough reviews: without label like “without enough reviews to infer
sentiment” or “no user reviews”
4. Games that are under the TOP 3 popular genres: Action-Adventure, Simulation and RPG
(Role-Playing games)

### game genres 
After deciding on the top 3 genres as targeted games, we redefined game genres because of the 6 Steam Game Platform Recommendation System
two following reasons:
1. some genres are overlapping, for example, “RPGMaker” and “RPG”;
2. one game may have more than one genre, for example, one game’s main genre is
“Swordplay” but it also has another genre tag “Simulation”.

## User Clustering 
Before building a recommendation system, we explored the dataset further and clustered the users based on their activeness and the relationship between number of games purchased and how often they play the game. In doing so, we have a much clearer view of the exact clusters we should include in our recommendation system.
<img width="492" alt="Screen Shot 2020-06-12 at 12 06 15 AM" src="https://user-images.githubusercontent.com/57570355/84474989-a4251700-ac40-11ea-90fd-4d4d7e566833.png">

1. Game lover : users who bought lots of games of different genres and have played them for many times, game fanatic;
2. Game devotor : users who are only crazy about games of a few or a specific genre.They don’t necessarily purchase that many games;
3. Game explorer : users who have purchased lots of games but did not necessarily spend too much time on it, it is possible that they only love exploring different games but are less addictive compared to game lovers and game devoters.
4. Occasional User : the opposite of a game lover, just occasionally playing games and disinterested in purchasing more.

## Active/Inactive Users
<img width="965" alt="Screen Shot 2020-06-12 at 12 08 39 AM" src="https://user-images.githubusercontent.com/57570355/84475187-f108ed80-ac40-11ea-8d52-6213e08e1608.png">

## Topic Model 
![1591945802671](https://user-images.githubusercontent.com/57570355/84475261-17c72400-ac41-11ea-8b44-83454574c7ea.jpg)


### User Profile
To conduct a robust recommendation system based on user similarity, we first did some feature engineering to incorporate more features based on current dataset to analyze a user through different dimensions. A user’s profile includes the following features for individual user:
1. NumGamesOwned : the cumulative numbers of games that the user owns through his/her lifetime in Steam;
2. NumReviewsGiven :the cumulative numbers of reviews that the user has given through his/her lifetime in Steam;
3. Action-Adventure: percentages of playtime spent on action-adventure games
4. RPG : percentages of playtime spent on RPG games
5. Simulation : percentages of playtime spent on Simulation games
6. RecommendedPercent : Percentage of the user clicking thumb up for recommending the game out of all his/her clicks
7. SteamAgeProxy : (last LastPlayTime when giving reviews - first LastPlayTime whengiving reviews)
8. Topic_1 -Topic_6: topics generated from LDA topic model - the percentage for each user’s review within different topics.

### User Similarity
Finally, we calculated user similarity based on Eucleadia distance and Cosine Similarity for this recommender system using our user profile. 
