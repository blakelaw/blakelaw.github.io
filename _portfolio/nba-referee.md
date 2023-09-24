---
title: "Decoding the Decisions"
excerpt: "a deep dive into NBA referee impact on gameplay"
image: "/images/12.jpg"
collection: portfolio
---

*Find the source code for the article [here](https://github.com/blakelaw/Referee-Analysis).* 

Across every major sport, fans will regularly boo referees they feel have wrongly called a play. They'll emphatically explain how they're being paid off and rigging it in real time. Basketball is no exception. And indeed, there have been 
<a href="https://www.npr.org/2008/06/12/91415111/ex-referee-says-2002-nba-playoff-was-rigged">cases</a> of referees interfering and throwing a game, but how large of an effect are they really having on a daily basis?

To answer this, I pored through a <a href="https://www.kaggle.com/datasets/wyattowalsh/basketball">database</a> of over 64,000 NBA games that includes box scores, play-by-play data, and a most importantly, a list of referees for each game. After preprocessing the SQL database so that I had i) the two teams playing ii) the scores of each team, and iii) the three referees for the game, I was ready to start digging in. 


<h4 style="font-size: 24px;">Method 1: Points added from referee</h4>

The most basic way of seeing how much a particular referee adds to a team is by calculating the average score of the team over the dataset (in this particular case, starting in the 1996 NBA season), and then comparing that the to average score of the team when a particular referee officiates the game. This is easier to do in Python, after connecting to the SQL database with the sqlite3 library, then creating a dataframe in pandas from this.

After playing around with the dataframe, we can arrive at a new table, that provides the particular referee and NBA team combination, and the differential between that referee and how the team would normally do. To make sure we don't have referees that only officiated a couple games for the team, let's set the minimum amount of games officiated for that team at 30. Here are the top ten in terms of absolute difference:

<iframe title="Largest Referee-Team Discrepancies in Total Scoring" aria-label="Table" id="datawrapper-chart-zlDrb" src="https://datawrapper.dwcdn.net/zlDrb/7/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="542" data-external="1"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r=0;r<e.length;r++)if(e[r].contentWindow===a.source){var i=a.data["datawrapper-height"][t]+"px";e[r].style.height=i}}}))}();
</script>

A few things stand out in this top ten. Nine of ten of the entries are positive, indicating that the referee gave the particular team an advantage, while only one (when Kevin Fehr officiates the Clippers) creates a disadvantage. Does this mean that referees are more interested in helping certain teams than hurting others? We also see that there are multiple repeats: Gediminias Petraitas, Tyler Ford, and Mitchell Ervin, all twice. These deviations are quite large — all double digits. Is Gediminas Petraitis really having a <b>sixteen point difference</b> on games?


<div class="text-center">
    <div class="col-sm mt-3 mt-md-0">
        <img src="/images/Dist.png" alt="example image" style="max-width:90%; border: 1px solid #ccc; border-radius: 8px; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);" />
    </div>
</div>




To investigate, let's visualize. We'll overlay all the of Wizard's games <i>(when we do this, we start to see the dataset <a href="https://www.kaggle.com/datasets/wyattowalsh/basketball/discussion/402040">isn't complete</a> in certain years, mostly notably 2018, stressing the importance of having good data)</i> and Wizard's games officiated by Gediminias Petraitas in Tableau. Each solid black dot represents a game officiated by Petraitas.

<div class="text-center">
    <div class="col-sm mt-3 mt-md-0">
        <img src="/images/Ged.png" alt="example image" style="max-width:90%; border: 1px solid #ccc; border-radius: 8px; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);" />
    </div>
</div>

This visualization tells a much different story. Instead of Petraitas consistently adding double digits above the Wizards' expected score, he happened to officiate games when the Wizard's had their highest scoring seasons. Indeed, this is not just a Wizards phenomenon, but a league-wide one. The Wizards average points per game (PPG) in the 2014-2015 season was 98.5, 17th in the league, and increased to 114.4 PPG in the 2019-2020 season, a very significant increase, placing 7th in the league by PPG. Over the same period, the NBA league average increased from 100.0 to 111.8, likely due to more emphasis on three pointers and increasingly faster paced games.

<h4 style="font-size: 24px;">Method 2: Elo System</h4>

Instead of taking the average over the entire dataset, we can create an "elo" system where a referee will receive a harsher penalty if the difference deviates more egregiously to the team's average around the same time. For a given game, we'll subtract the score of the game officiated by a particular referee from the average in the same year instead. 

In the previous example with Petraitas, instead of the Wizard's 146-149 loss on 1/31/21 counting as a 47 point deviation, it is roughly 31 points. 

From this, we have a much less extreme picture. The top ten are again shown but with the new metric:

<iframe title="Largest Referee-Elo Discrepancies" aria-label="Table" id="datawrapper-chart-TPG4L" src="https://datawrapper.dwcdn.net/TPG4L/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="509" data-external="1"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r=0;r<e.length;r++)if(e[r].contentWindow===a.source){var i=a.data["datawrapper-height"][t]+"px";e[r].style.height=i}}}))}();
</script>

In this ranking, no referee-team combination reaches double digits. In fact, we approach a difference of only 5 points very quickly. Notice that the Petraitis combination we analyzed earlier is ranked second. Mark Ayotte, who has officiated 49 Knicks games in our dataset, benefits the team by nearly 7.5 points on average. Like before, let's visualize this with Tableau to see if the deviation does indeed look extreme.

<div class="text-center">
    <div class="col-sm mt-3 mt-md-0">
        <img src="/images/Ayotte.png" alt="example image" style="max-width:90%; border: 1px solid #ccc; border-radius: 8px; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);" />
    </div>
</div>

Similarly, there seems to be no clear pattern of Mark Ayotte helping the Knicks score more points even though the data suggests it. In fact, there were a few games between 2014-2017 where NYK games officiated by Ayotte are near the bottom of their season scoring. However, the outlier games (143 points against the Hawks in 2019 and 137 points also against the Hawks in 2021) more than offset these. 

So far, we haven't found any convincing evidence that any referees in the league systematically favor or hurt particular teams. Of course, this neglects high-stakes playoffs games or one-off occurrences, but those must be looked at ad hoc and can't rely on statistics, as a major call with five seconds left that nets a team two points with only a few seconds left is statistically the same as a shooting foul two minutes into the first quarter. 

<h4 style="font-size: 24px;">Method 3: Impact Score</h4>

So far we've only focused on points and only worked with subtracting means from other means. However, we can go much further. Rather than just focus on the points for each game, we will focus on <i>all</i> metrics provided. In addition to points, the original database also contains the following for each team in a given game: field goals made, field goal percentage, three pointers made, three point percentage, free throws made, free throw percentage, offensive rebounds, defensive rebounds, total rebounds, assists, steals, blocks, turnovers, and personal fouls. That's a lot more to work with than we were before. However, there's an issue: how do we work with so many dimensions at once?

The objective is to reduce the dataset's number of dimensions to a more manageable size, ideally one or two, without losing significant information. One effective method for achieving this is <a href="https://en.wikipedia.org/wiki/Principal_component_analysis">principal component analysis (PCA)</a>. PCA employs linear algebra to identify the <b>principal components</b> of the dataset. The first principal component accounts for the most variance in the data. Subsequent components, each orthogonal to the preceding ones, account for decreasing amounts of variance. As a result of this orthogonality, each principal component is uncorrelated with the others.

To do this, we will need to do some pre-processing first. After returning to the original SQLite database, I modified it so that each row represents a single team's performance in a game with all of their relevant stats I just listed, as well as one of the referees involved in the game. Thus, there are six rows for a given game with three referees. 

After that, I found the mean of each statistic for every referee and aggregated this in a new table.

{% highlight python %}
# List of columns that contain statistics
stats_columns = ['fgm', 'fg_pct', 'fg3m', 'fg3_pct', 'ftm', 'ft_pct', 'oreb', 'dreb', 'reb', 'ast', 'stl', 'blk', 'tov', 'pf', 'pts']

# Group by referee and aggregate the original data
aggregated_raw_data = data.groupby(['first_name', 'last_name', 'official_id']).agg({**{col: 'mean' for col in stats_columns}, 'game_date': 'count'}).reset_index()
aggregated_raw_data = aggregated_raw_data.rename(columns={'game_date': 'num_games'})
{% endhighlight %}

Now, before we proceed to PCA in R, we need to normalize the data to ensure that statistics with higher means (such as points) don't necessarily receive more weight, although they might in the end. We will do this by calculate the mean and standard deviation for each statistic. Then, for each official, we will subtract the mean and divide by the standard deviation. This ensures the mean of every statistic is 0, and that the standard deviation is 1:

{% highlight python %}
# Normalize the aggregated data
aggregated_raw_data[stats_columns] = (aggregated_raw_data[stats_columns] - aggregated_raw_data[stats_columns].mean()) / aggregated_raw_data[stats_columns].std()
{% endhighlight %}

Now our data is ready for principal component analysis. We'll export this dataframe to R:

{% highlight python %}
# Perform PCA
pca_result <- prcomp(data_pca_only, scale. = TRUE, center = TRUE)

# Extract the scores for each principal component
scores <- pca_result$x

# Append the PC scores to the original dataframe
data_with_scores <- cbind(data_for_pca, scores)
{% endhighlight %}

Notice how two of the parameters for prcomp are `scale. = TRUE` and `center = TRUE`. This means we didn't necessarily have to standardize it beforehand, but it's nice to do it on the original dataframe in case we wanted to use it elsewhere where this might not be an option. Anyway, let's look at the results and interpret the principal components. First, we're going to look at the relative weights assigned to each variable, also known as loadings. This can be done by running `print(pca_result$rotation)`:

{% include my_table2.html %}


That's a lot to look at, even after rounding each loading to three decimal places. Thankfully, PCA makes things easier, not harder. We first column, labeled PC1, has the largest variance compared to each subsequent principal component. We're going to just focus in on the first two columns. Reading off the first and second column:

$$\textbf{PC1} = -0.315 \cdot \textbf{fgm} - 0.272 \cdot \textbf{fg_pct} - 0.314 \cdot \textbf{fg3m} - 0.128 \cdot \textbf{fg3_pct} + \ldots$$
$$\textbf{PC2} = -0.040 \cdot \textbf{fgm} - 0.259 \cdot \textbf{fg_pct} - 0.023 \cdot \textbf{fg3m} - 0.064 \cdot \textbf{fg3_pct} + \ldots$$

In the first component, many of the loadings were in the 0.25-0.30 range (in absolute terms), with the largest weights belong to field goals made (-0.315), three pointers made (-0.314), and total points (-0.310). This makes sense that these have similar weights, as they are also highly correlated which each other: if you make more three pointers in a game, of course you're going to typically score more points. Measures like steals and blocks (-0.034 and 0.008, respectively) received almost no weight. 

In the second component, which is mathematically uncorrelated with the first, the weights are completely different. Assists go from having a weight of -0.309 to -0.001. In this second component, defensive measures take importance. Now, steals and blocks have the highest magnitude weights: -0.550 and -0.619, respectively. Free throws made (0.259) is  also relatively high. The offensive stats such as pts and fgm now score relatively low, under 0.1.

We can conceptualize the first component as a measure of offensive variance and the second as primarily defensive. Referees that tend to affect offensive statistics more will stray further from PC1 = 0 in either direction, while referees that tend to affect defensive statistics more will deviate further on PC2. Now, let's project each of these weights onto the statistics we calculated for each referee and visualize the results. Hover over each point to see the referees name, the exact values of PC1 and PC2, and the number of games they've officiated.

<iframe title="NBA Referees by Principal Components" aria-label="Scatter Plot" id="datawrapper-chart-suU3Z" src="https://datawrapper.dwcdn.net/suU3Z/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="400" data-external="1"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r=0;r<e.length;r++)if(e[r].contentWindow===a.source){var i=a.data["datawrapper-height"][t]+"px";e[r].style.height=i}}}))}();
</script>

The first thing I noticed is that the most extreme values (e.g. Robbie Robinson, Danielle Scott, Matt Kallio) are on the lower end of games officiated, while veteran referees such as Ed Malloy, Leon Wood, and Marc Davis are much closer to the origin (0,0). This might reflect the fact that veteran referees are retained because of their impartiality and lack of overall effect on the game. Or it could simply be a statistical artifact, as referees with more games officiated contribute more to the overall average. Let's do some ad hoc analysis on some of the outliers:

<b>Robbie Robinson</b>: Robinson stands out, with an usually high PC1 and PC2 (5.6, 3.8). Was he actually a "bad" officiator though? The answer appears to be yes. <a href="https://archive.is/XjAXM">According to Sports Illustrated</a>, citing league sources, Robinson was fired "for his poor performance" in his three-year stint as referee. 

<b>Ted Bernhardt</b>: Bernhardt was one of the three officials who oversaw Game 6 of the 2002 Lakers-Kings series, which is arguably the most controversially officiated game of all time. As referenced earlier, Tim Donaghy claimed this game was rigged by two of the referees in a filing to the U.S. District Court in New York:

<blockquote>
    Referees A, F and G were officiating a playoff series between Teams 5 and 6 in May of 2002. It was the sixth game of a seven-game series, and a Team 5 victory that night would have ended the series. However, Tim learned from Referee A that Referees A and F wanted to extend the series to seven games. Tim knew referees A and F to be 'company men,' always acting in the interest of the NBA, and that night, it was in the NBA's interest to add another game to the series. Referees A and F heavily favored Team 6. Personal fouls [resulting in obviously injured players] were ignored even when they occurred in full view of the referees. Conversely, the referees called made-up fouls on Team 5 in order to give additional free throw opportunities for Team 6. Their foul-calling also led to the ejection of two Team 5 players. The referees' favoring of Team 6 led to that team's victory that night, and Team 6 came back from behind to win that series.
</blockquote>

However, a few caveats. It's more than likely Referees A and F are Dick Bavetta and Bob Delaney. Second, there's never been any conclusive proof that the games were rigged, and Tim Donaughy himself is <a href="https://www.nytimes.com/2007/08/16/sports/basketball/16nba.html">disgraced</a> for betting on games. However, even Bernhardt <a href="https://www.espn.com/nba/news/story?id=3444557">admitted</a> that the game wasn't well-officiated, including on his part. Of course, only one game (and it's a playoff game, so it's not contributing to the dataset anyway), so it would have little to no effect on these results anyway. 

<b>Matt Kalio & Danielle Scott</b>: Kalio and Scott are  relative newcomers, only beginning to officiate games since the pandemic. It's very possible that his current aberration is just statistical noise. 

<h4 style="font-size: 24px;">Conclusion</h4>
