# Predicting Next Attacking Action in Football Matches

## Introduction & Objective
The objective of this project is to produce a model capable of correctly predicting the next attacking action during a football match. The model will work with time sequential in-game data, using information from previous matches as well as the "current" match to predict the next move of the attacking team.
The data used for this project was gotten from StatsBomb's open data GitHub [repository](https://github.com/statsbomb/open-data). The model relied specifically on StatsBomb 360 event data, which contains location of attacking and defending players accross the pitch to further improve the decision making of the model. This left us with data from three National team competitions; FIFA World Cup - 2022, UEFA Euro – 2020, UEFA Women's Euro – 2022, i.e 146 matches from these three competitions. These three competitions served as the basis for the building the model used to tackle the problem of predicting the next action.

## Pre-Processing
To focus on attacking actions (actions on the ball), the data provided was cleaned by deleting attributes deemed not important to the task, merging features and actions that were similar as well as generating new attributes deemed more valuable for the task. This left us with 4 attacking actions to serve as the actions to be predicted; Passing, Shooting, Crossing and Dribbling. 
** Due to computing limitations, average distance from the ball for attacking player and defending players were used**

| Field Name          | Description |
|---------------------|-------------|
| match_id            | This is a unique number given to differentiate between matches |
| under_pressure      | Describes if an action was done under pressure from an opposition player or players |
| zone                | Describes the square out of 30 squares where an event occurred |
| type                | Describes the action that has been done during an event |
| possession_team_id  | Unique number to differentiate between teams in possession of the ball |
| position            | Describes the position or role of the player in possession of the ball |
| formation           | Describes the tactical formation employed by a team during the event |
| duration            | The time taken to complete an action |
| avg_teammate_dist   | Average distance of teammates of the player in possession |
| avg_opponent_dist   | Average distance of opposition players from the player in possession |
| num_teammates       | Number of teammates in the frame during an event |
| num_opponents       | Number of the opposition players in the frame during an event |
| x0, y0              | Coordinates of the player in possession on the x and y axis |
| Zone_deltay         | Change in coordinate on y-axis using the zone |
| Zone_deltax         | Change in coordinate on x-axis using the zone |
| Zone_dist           | Distance between zones |
| Zone_dist2g         | Distance from zone to goal |
| zone_angle2g        | Angle from zone to goal |


