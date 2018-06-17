This repository serves as a complementary part for the blog post:
https://medium.com/@martin.luksik/was-it-in-lebrons-hands-to-win-the-2018-nba-finals-d2763b6b466


Was it in LeBron’s hands to win the 2018 NBA Finals?
from a Data Science perspective

Objectives:
What was the probability of the Cleveland Cavaliers (CLE) beating the Golden State Warriors (GSW) in each of the four games based on LeBron James career statistics? What a heroic performance he’d need to put up in order to deliver another Championship for Cleveland? How much does this probability change when the classifier (doesn’t) know the quality of the opponent?

To answer this question, the article takes you through a Data Science solution, which implies a Machine Learning model. If you are not so much into Data Science and Statistics, you might want to directly scroll down to the results of the study. The study is possible to replicate. Data and Python code are accessible at GitHub.

Solution:
- Use LeBron James’s entire career statistics to train a classifier (Logistic Regression).
- Apply the classifier to predict the chance of CLE winning any of the four games in the Finals 2018 based on LeBron’s numbers (points, minutes, assists, blocks, fouls, etc.) in these games.
- Deriving an additional feature capturing the quality of the opponents’ team (a percentage of wins in a season) and training a new model
- Employing the improved model to predict the odds of CLE winning any of the Finals 2018 games -> comparing the results from two models and interpreting the results.

Data:
The 1. dataset consists of LeBron’s games’ statistics. There are 1380 games (observations) where LeBron played at least 1 minute. Note that the data for the model development does not include any data about the NBA finals 2018.

There are 17 variables:

W (Boolean): LeBron’s team has won the game or not
LeBron James statistics for every game in his career (int):
Points, Assists, Blocks, Defensive rebounds, Field Goals Attempted, Field Goals Made, Fouls, Free Throws Attempted, Free Throws Made, Minutes (float), Offensive Rebounds, Rebounds, Steals, Three-Pointers Attempted, Three-Pointers Made, Turnovers, Name of the Opponent’s team (str)
The 2. dataset (consists in total of 15 csv files (1 file = 1 season) includes all games played in the season (including playoffs). The time range is then 2003–2017 (LeBron entered the NBA in 2003).

There are 4 variables:

W (Boolean): Team has won the game or not
Team (str)
Opponent team (str)
Season (int)
Model development:
Checking on multicollinearity and dropping problematic features. This way we also solve a possible issue with Data Leakage.
Plotting a Validation Curve with Logistic regression model (a range of C parameters over 4 folds)
Displaying accuracy, AUC, precision, and recall for a range of C parameter values over 4 folds.
Choosing the best C parameter based on steps 2 and 3 and ensuring that the complexity of the model doesn’t lead to overfitting.
Splitting dataset on train and test set (including rows shuffle and random state to ensure the possibility of the study replication) and revealing the confusion matrix, accuracy, precision, and recall. Note that the model focuses on recall (87%) -> capturing positive cases (Wins), in order to develop a lower threshold for the positive class classification. The model is not forced towards higher recall, as this would result in a dummy classifier performance -> Wins are more frequent class than losses. Keeping recall on 86% while precision on 76% is still reasonable.
Plotting the precision and recall curve (just for the sake of completeness and further options of the model tuning).
Plotting the ROC curve with the variance of the C parameter.
Using the tuned model to classify a games’ outcome based on LeBron’s statistics from the NBA Finals 2018 Games 1 to 4.
Feature engineering and model improvement -> opponent’s team quality:

Deriving every team’s season winning percentage from the 2. data set. Merging the results with the 1. dataset -> this way the model can learn about the opponent’s team quality in the corresponding season that the game occurs.
Dropping features with low importance based on decision tree classifier.
Repeating the steps 1–8
Using the tuned classifier with the new feature “quality of the opponent”, to compute the probability of Cleveland winning the NBA Finals 2018 games, based on LeBron’s statistics from the games 1 to 4.
Interpretation of results:
The first model (without any knowledge about opponent’s team quality) predicts the following chances for CLE to win the NBA Finals 2018 games based on LeBron James statistics:

Games 1–4: 91%, 99%, 67%, and 98%

Obviously, the model was 4 times wrong. CLE lost all the 4 Games. What does this mean? Just two things which most of us, perhaps, have known all along:

1. LeBron James had done enough to increase the chance of the W in all the 4 games. In a regular game of his career, these numbers would probably lead into a W.

2. The model is not good enough to get close to the real probability. It simply needs more data to learn from. LeBron hadn’t faced his regular (average) opponent. He has faced one of the best team that we could witness in the history of NBA. Therefore, the model needs to learn about the quality of LeBron’s opponents.

After feeding the model with the new feature?—?winning season percentage of the opponent, the model delivered much more interesting insight:

Games 1–4: 64%, 36%, 22%, and 18%.

LeBron himself couldn’t do much more to increase the probability of CLE beating GSW. Even when delivering great performance in G1 the probability of W was only 63%.

The decrease of probabilities through games 1 to 4 also points to another interesting finding. The quality of LeBron’s statistics dropped with every lost game. Note that none of the models have data about any of these games and therefore the model can’t learn anything from the Game 1 in order to compute the probability of Game 2, etc.


This model shows evidence that the result of the Game was not depending on LeBron’s performance and motivates a hypothesis that the outcome of the game was more dependent on his teammates’ performance. The quality of the opponent is indeed a very significant feature?—?twice more important than any other feature in the model. The quality of GSW overshadows LeBron James’ statistics.


In other words, LeBron would need much more support from his teammates to beat GSW. For sure, it would be helpful if J.R. Smith would’ve handled the end of the Game 1 better, but that belongs to a different field of science…

So what number would he need to put up in order to increase the probability of winning? The model reveals that if he would put up 50 points, 15 assists, 10 rebounds, 42 minutes, 2 turnovers, 30 field goal attempts, and attempted 5 three pointers, Cleveland would have had 90% chance of winning in a game against GSW.

This study controls only LeBron’s performance and confirms what we might have assumed -> Golden State Warriors would have won the 2018 NBA Finals regardless LeBron James’ above average performance.
