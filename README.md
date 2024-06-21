# nba-team-defense

This project was the capstone project for the 2024 cohort of the NBA Future Analytics Stars Program.

Leveraging the provided center-of-mass tracking data, we wanted to create a new metric to measure an aspect of basketball strategy not captured by widely known traditional or advanced stats. We also wanted to keep in mind how this metric might help a coach or GM make informed decisions about in-game strategy, free agency, trades, the draft, and more. We were more interested in what the metric could help quantify than how complex the metric was.

## Designing a new team-level defensive metric from NBA tracking data:

### Background

Analysts are generally better currently at evaluating offense on both a team and individual player level. We wanted to take a look at team-level defense particularly on off-ball defense as this is something we think is under-explored. We also wanted to focus on the team level vs. individual because team-wide defense is potentially more useful to evaluate since defense is very scheme-dependent and individual credit assignment is difficult. From the Midrange Theory by Seth Partnow: “According to tracking data from recent seasons, the average defensive “matchup usage” was between 18% and 22% for 90% of players, while only one in four had offensive usage rates in a similarly narrow range, demonstrating that defense is almost inherently more collaborative than offense in today’s NBA.”

We also wanted to build a measure or metric that’s easy to replicate given the volume of player tracking data and something that’s easy to extend given more time and future resources.

While individual 3PT defense is highly variable and not great to try and predict/forecast, rim protection/deterrence is more measurable due to shot dissuasion (“good” 3PT defense leads to a host of other offensive player outcomes such as passing and dribbling away, whereas shooters generally continue to shoot from spots at the rim/in the paint).

### Development Process

There were a number of steps we took to analyze the data: basic data wrangling (reading in data, joining data appropriately, cleaning null values), domain knowledge-based data wrangling (filtering out frames to only keep halfcourt situations to try and exclude noise related to fast break and miscellaneous game situations where defenses are not set), and developing functions to parse, plot, and analyze the x-y location data.

In terms of metric building: For each frame that belongs to a halfcourt moment of a possession (when the two team shapes intersect each other by at least 30% of either of the teams’ shapes), we calculate a convex hull for the defensive team and find the intersection of that with the paint area. In essence, we are calculating frame-by-frame the amount of paint area covered by the defensive team as a way to understand how much coverage of this space the defensive team has. We also calculate for each frame the distance between the offense's ball handler and the closest defender. 

### Metric Evaluation

We looked at correlation against full-season team defensive rating with some caveats and major assumptions by extrapolating the metrics we calculated for the sample of data that was provided. We also provide a brief qualitative evaluation with the idea of "meta-metrics" proposed in the "Meta-analytics: tools for understanding the statistical properties of sports metrics" paper by Franks, et. al. In essence, we look at stability (does the metric measure the same thing over time); discrimination (does the metric differentiate between players or teams); and independence (does the metric provide new information relative to other metrics).

### Future Considerations

In future work, we'd like to 1) filter out garbage time; 2) incorporate more data such as player wingspan and pose data to further enhance the data context especially for the perimeter defense measurement; and 3) use Voronoi tessellations intead of convex hulls as an alternative approach to the paint defense portion of the overall metric calculation.

### Resources

1. "The Midrange Theory" by Seth Partnow
2. Justin Jacobs' blog (https://squared2020.com)
3. “Meta-analytics: tools for understanding the statistical properties of sports metrics” by Franks, et. al.
