---
layout: post
title:  "Searching for the Flying V"
date:   2026-10-19 09:01:24 -0500
categories: jekyll update
---

# Introduction

The [Flying V](https://www.youtube.com/watch?v=-WZ0uRJOatQ) is from the Mighty Ducks films, where the skaters form a V and skate together in that V formation.

Since I've been analyzing tracking data, I wondered if I could use that data to find when NHL players happen to end up in a similar formation.

For those interested, the code for this analysis is [here](https://github.com/danielglin/nhl_goal_tracking_analyses/tree/main/flying_v).

# Data 

To look for the Flying V, I used the public player tracking data from NHL.com's goal visualizations.
That means I was only able to look at a very small portion of games, so there could be Flying V's out there that I missed.

At least on the flip side, I didn't have to handle massive amounts of data.
The data I did use was from the 2025-2026 regular season, with the empty-netters removed.
Using the Flying V against an empty net seemed against the spirit of the V.
Also, I only looked at the player tracking data for the scoring team since the Flying V is an offensive formation.

Other additional data pre-processing includes rotating the coordinates so that all goals are scored on the right side.

# Approach

To find the Flying V in the player tracking data, I used the Hausdorff distance.
The Hausdorff distance is used in computer vision to find a template image within an image.
Here I'm using the Hausdorff distance to compare how similar a player formation at a timestep is to a baseline Flying V.
The baseline Flying V looks like:

![](/images/flying_v/baseline_flying_v.png)

However, I couldn't use the Hausdorff distance directly since that would only find Flying V's near the same spot as the baseline.
To find Flying V's that could be anywhere, I calculated the baseline's center by averaging all the points.
Then I subtracted the center from all the points in the baseline.
This captures the relationships between the points.
Then at each timestep in the tracking data, I repeated the process on the five skaters' locations.
Finally, I calculated the Hausdorff distance between the timestep's adjusted locations and the adjusted baseline.

Repeating this process for all timesteps gave me the timesteps with the closest formation to the Flying V.

# Results

Out of all the 2025-2026 goals analyzed, the [goal by the New York Islanders against the Vegas Golden Knights on November 13, 2025](https://www.nhl.com/ppt-replay/goal/2025020277/295) got closest to the Flying V:

![](/images/flying_v/nyi_flying_v.png)

The V shape might be a little easier to see when looking at the skaters' locations in a top-down diagram:
![](/images/flying_v/nyi_flying_v_diagram.png)

Another goal that gets close to the Flying V is the [Leafs goal against the Rangers on March 5, 2026](https://www.nhl.com/ppt-replay/goal/2025020975/55):

![](/images/flying_v/leafs_flying_v.png)

![](/images/flying_v/leafs_flying_v_diagram.png)

Though I'm not sure if this one should count since it's right after a faceoff.

One more goal is [the Predators against the Blues on December 11, 2025](https://www.nhl.com/ppt-replay/goal/2025020487/704):

![](/images/flying_v/preds_flying_v.png)

![](/images/flying_v/preds_flying_v_diagram.png)

# Closing Thoughts

While I searched for the Flying V, it's possible to search for any formation with the approach I described here.

However, in the future I might try to come up with a method that scales better. 
Calculating Hausdorff distances over and over again seems to take a while.

Remember that [Ducks fly together](https://www.youtube.com/watch?v=TQL775VU3Us)!