This repository serves as a complementary part for the blog post:
https://medium.com/@martin.luksik/what-statistics-made-james-harden-the-mvp-of-2018-72100668ef3d

What statistics made James Harden the MVP of 2018?
from a Data Science perspective

Objectives:
This blog focuses on an investigation of all NBA players’ statistics in the regular season 2017/2018 in order to reveal the reasons which made James Harden a unique player this season. Using clustering methods would be one of many options how to tackle this topic. However, the dataset with players’ statistics includes many features and it’d be great to have them all in one plot. For these reasons, I decided to reduce the dimensionality via Principal Component Analysis (PCA).

Solution:
The final result is a description of 2-dimensional space where the main NBA statistical differences within the key players of the season 2017/2018 are captured and discussed. This is accomplished within a few steps of PCA, and feature selection. The result of this study is possible to replicate via shared data and code stored on my GitHub. Furthermore, I provide you with interactive plots stored on Plotly, so you can see where your favorite player stands. Have fun!

Data:
The only dataset used in this study includes 540 observations. Each tuple represents a statistics of an NBA player in the season 2017/2018.

The dataset captures the following variables:

GP - Games Played, W - Wins, L - Losses, DD2 -Double doubles, TD3 - Triple doubles. And further average statistics per game: MIN - Minutes Played, FGM - Field Goals Made, FGA - Field Goals Attempted, FG%- Field Goal Percentage, 3PM -3 Point Field Goals Made, 3PA - 3 Point Field Goals Attempted, 3P% - 3 Point Field Goals Percentage, FTM — Free Throws Made, FTA - Free Throws Attempted, FT% -Free Throw Percentage, OREB- Offensive Rebounds, DREB -Defensive Rebounds, REB- Rebounds, AST -Assists, TOV -Turnovers, STL -Steals, BLK -Blocks, PF- Personal Fouls, FP -Fantasy Points, PTS- Points, +/- Plus Minus

Dimension reduction:
As we know, it is not really in our hands to plot a space of 29 dimensions. The application of PCA transforms the set of possibly correlated features into a set of values of linearly uncorrelated variables. It is possible to create a 2D or 3D space and display all our features in one graph. Application of two principal components lead into the following plot:


Dimensionality reduction — 540 players and 29 features
At this moment, you can see the distances between the players, but no interpretation of the features determining the distances. The key at this moment is the fact that James Harden stands far from the other players, on the very right bottom corner of the graph (the fourth quadrant). This gives a great hint -> J. Harden’s statistics vary even from the other top NBA players like Kevin Durant, Stephen Curry, Russel Westbrook, Damian Lillard, or Lebron James. Nevertheless, this is not yet a time to make a conclusion that he deserves the MVP as it is not clear if he is so distant from other players for good reasons.

The next step is to work only with the 5 mentioned players (plus J.Harden) and apply PCA again. This helps to get a closer look at the differences between the players close to James Harden and investigate what makes him different.

Now, when the plot includes only a few players, let’s investigate the impact of features on the components.


James Harden stands on the coordinates [-0.7; 4.7]. This makes him unique on the scale of the second principal component while being the closest player to the 0 on the x-axis. The black & white scale displayed below this paragraph serves for the interpretation of the plot. Features represented by white color stand on the positive coordinates of axis and dark colors represent negative coordinates.


Analysis interpretation:
The PC2 explains that James Harden stands on the opposite of what’s interpreted as perfect FG%, high number of L, and high number of Blocks per game, while having high W, PTS, FTM, FTA, and STL. Especially the difference between W and L seems to increase the positive reasons for naming him the 2017/2018 MVP. On the other hand, his FG% 44.9 is way lower compared to Lebron James 54.2 and Kevin Durant 51.6. Anyway, what is it good for when you don’t bring home enough W.

The first principal component reveals that Steph Curry has high numbers in 3PM, 3PA, 3P%, FT% and +/-, while Russel Westbrook and Lebron James stands rather on the opposite side. James Harden stands between these extremes. Further investigation of his statistics shows the evidence that 3P% is compensated by his number of 3PM, 3PA and great +/- as well as FT% (compare to Westbrook and LeBron James).

This being said, James Harden has put up unique numbers this season. You might argue that he is not the real MVP based on the absolute numbers of the regular season. On the other hand, PCA of statistics per game reveals that he is the only player in the league who stands out not just compare to the average players of the league, but also compare to other superstars — potential MVPs.

As a player who is closest to the 0 on the x-axis (PC1), shows his balanced statistics and don’t put him in a position where he would master one skill but lack other skills. The y-axis shows his ability to bring many wins home while scoring a lot of points and knocking down many free throws.

I wasn’t sure why he was the 2017/2018 MVP. It’s much more clear to me after this analysis. His statistics simply stands out from the other superstars.