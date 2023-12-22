# Predicting Next Attacking Action in Football Matches

## Introduction & Objective
The objective of this project is to produce a model capable of correctly predicting the next attacking action during a football match. The model will work with time sequential in-game data, using information from previous matches as well as the "current" match to predict the next move of the attacking team.
The data used for this project was gotten from StatsBomb's open data GitHub [repository](https://github.com/statsbomb/open-data). The model relied specifically on StatsBomb 360 event data, which contains location of attacking and defending players accross the pitch to further improve the decision making of the model. This left us with data from three National team competitions; FIFA World Cup - 2022, UEFA Euro – 2020, UEFA Women's Euro – 2022, i.e 146 matches from these three competitions. These three competitions served as the basis for the building the model used to tackle the problem of predicting the next action.

## Pre-Processing
To focus on attacking actions (actions on the ball), the data provided was cleaned by deleting attributes deemed not important to the task, merging features and actions that were similar as well as generating new attributes deemed more valuable for the task. This left us with 4 attacking actions to serve as the actions to be predicted; Passing, Shooting, Crossing and Dribbling. 

The data was split using 8:1:1 for Train, Validation and Test respectively. Data was standardised and windowing was applied to the datasets.

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

## Modelling
The LSTM framework (Long Short-Term Memory) was selected based on these considerations, its ability to handle time series data. The model was designed to have 7 inputs and 4 outputs. 6 of inputs were the categorical features and the last all the numerical features combined as one. The final model was trained over 16 epochs and had a total of 22,848 trainable parameters and 0 non-trainable parameters.
![Screenshot 2023-08-27 172618](https://github.com/LaseTawak/Predicting-Next-Action-in-Football-Matches/assets/69163893/3d856aa6-0c98-4420-a094-d90be192c858)

Embedding was used to handle categorical features over One-Hot encoding. Embeddings provide a reduction in dimensionality that One-Hot encoding does not which allows for 30 lower training time. Embeddings also have the potential to provide context and meaning representation of categories to the model which can help improve the accuracy of the model.

## Results
