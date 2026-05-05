---
layout: post
title:  "Defining Rush Goals with Puck Tracking Data"
date:   2026-05-04 07:07:18 -0500
categories: jekyll update
---

# Introduction

One of the analyses I wanted to do with the publicly available goal tracking data is to see how many goals each team scores off the rush.
In order to do that, I had to define criteria for rush goals.
That process involved iteratively setting some tentative criteria, reviewing the results, and updating the criteria.
At the end of it, I ended up with three criteria that I used to calculate how many rush goals each team scored in the 2025-2026 regular season.

You can find the code I created for this analysis [here](https://github.com/danielglin/nhl_goal_tracking_analyses/tree/main/rush_goals).

# Data

The data I used was the public goal tracking data for the 2025-2026 regular season.
This data is the same data that is used for NHL.com's goal visualizations.
Here is [one example](https://www.nhl.com/ppt-replay/goal/2025020151/457) goal visualization.

For this analysis, I did the same pre-processing steps I had used when looking at [goal similarity](https://github.com/danielglin/nhl_goal_similarity#data).
This includes trimming the starts and ends of the tracking data to account for things like faceoffs.

I filtered out empty net goals from the data using NHL.com's API to get empty net goal data.

One caveat: some goals are missing data, but this is a very small percentage of goals (< 0.1% of all goals).

To keep it simple, I only used puck tracking data and not the player tracking data.
In the future, I may revisit the criteria to include the player tracking data.

# Process

The process I used to come up with criteria to define rush goals was:

1. Set tentative criteria
2. Review a sample of goals that were close to being considered rush or non-rush
3. Update the criteria based on that review and repeat the process

Throughout this process, I reviewed around 60-80 goals in total.

# Criteria

The final criteria are:

1. The puck traveled at least 67 feet along the length of the ice
2. The puck spent less than 40 timesteps in the offensive zone
    - A timestep is the interval in between data points in the tracking data.
    - In a future analysis, I hope to calculate how much time this interval is.
3. The puck spent less than 9 timesteps beyond the goal line

# Results

Using the above criteria, about 29% of non-empty net goals were off the rush in the 2025-2026 regular season.

Some example goals defined as rush goals by the criteria:

- [https://www.nhl.com/ppt-replay/goal/2025021019/115](https://www.nhl.com/ppt-replay/goal/2025021019/115)
- [https://www.nhl.com/ppt-replay/goal/2025020129/353](https://www.nhl.com/ppt-replay/goal/2025020129/353)
- [https://www.nhl.com/ppt-replay/goal/2025021266/715](https://www.nhl.com/ppt-replay/goal/2025021266/715)
- [https://www.nhl.com/ppt-replay/goal/2025020257/828](https://www.nhl.com/ppt-replay/goal/2025020257/828)
- [https://www.nhl.com/ppt-replay/goal/2025020499/151](https://www.nhl.com/ppt-replay/goal/2025020499/151)

Here are the number of rush goals by team:

| Team | Number of Rush Goals |
| --- | --- |
| CAR | 89 | 
| PIT | 86 | 
| UTA | 85 | 
| BUF | 84 | 
| EDM | 80 | 
| LAK | 77 | 
| MTL | 75 | 
| ANA | 73 | 
| STL | 73 | 
| TBL | 73 | 
| CBJ | 71 | 
| NYR | 71 | 
| CGY | 70 | 
| MIN | 69 | 
| TOR | 69 | 
| NYI | 68 | 
| PHI | 68 | 
| VGK | 68 | 
| NJD | 66 | 
| WPG | 66 | 
| COL | 65 | 
| SJS | 65 | 
| DET | 64 | 
| FLA | 62 | 
| VAN | 61 | 
| SEA | 59 | 
| OTT | 58 | 
| BOS | 58 | 
| WSH | 58 | 
| CHI | 57 | 
| DAL | 56 | 
| NSH | 45 | 

Here are the percentages of goals that were rush goals by team (excluding empty net goals):

| Team | % of Goals that are Rush Goals |
| --- | --- |
| LAK | 37% | 
| CGY | 36% | 
| STL | 34% | 
| UTA | 34% | 
| BUF | 33% | 
| NYR | 32% | 
| NJD | 32% | 
| CAR | 32% | 
| PHI | 31% | 
| CBJ | 31% | 
| NYI | 31% | 
| WPG | 31% | 
| PIT | 31% | 
| EDM | 30% | 
| TOR | 30% | 
| VAN | 30% | 
| SEA | 29% | 
| ANA | 29% | 
| DET | 29% | 
| CHI | 28% | 
| MTL | 28% | 
| TBL | 28% | 
| MIN | 27% | 
| FLA | 27% | 
| SJS | 27% | 
| VGK | 27% | 
| WSH | 25% | 
| COL | 24% | 
| OTT | 23% | 
| BOS | 23% | 
| DAL | 21% | 
| NSH | 20% | 


# Conclusion

While the criteria I developed seem to work well, I may in a future analysis try to refine them by including player tracking data in addition to the puck tracking data.
I would also like to dive deeper into rush goals as well.