# Predicting Next Attacking Action in Football Matches

## Introduction & Objective
The objective of this project is to produce a model capable of correctly predicting the next attacking action during a football match. The model will work with time sequential in-game data, using information from previous matches as well as the "current" match to predict the next move of the attacking team.
The data used for this project was gotten from StatsBomb's open data GitHub [repository](https://github.com/statsbomb/open-data). The model relied specifically on StatsBomb 360 event data, which contains location of attacking and defending players accross the pitch to further improve the decision making of the model. This left us with data from three National team competitions; FIFA World Cup - 2022, UEFA Euro – 2020, UEFA Women's Euro – 2022, i.e 146 matches from these three competitions. These three competitions served as the basis for the building the model used to tackle the problem of predicting the next action.

## Pre-Processing
To focus on attacking actions (actions on the ball), the data provided was cleaned by deleting attributes deemed not important to the task, merging features and actions that were similar as well as generating new attributes deemed more valuable for the task. This left us with 4 attacking actions to serve as the actions to be predicted; Passing, Shooting, Crossing and Dribbling. 

The data was split using 8:1:1 for Train, Validation and Test respectively. Data was standardised and windowing was applied to the datasets.

**Due to computing limitations, average distance from the ball for attacking player and defending players were used**

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
Different types of LSTM models were developed to also serve as a means of hyper-parameter tuning to obtain the best posisble model. Validation Loss was used during training to ensure model learning and F1 score and Recall were preferred to evaluate the model during testing. The best performing model is highlighted in blue.
![Screenshot 2023-09-07 191714](https://github.com/LaseTawak/Predicting-Next-Action-in-Football-Matches/assets/69163893/9f4239a7-7428-4e7d-a531-bb4c1403ccf4)

The chart below shows how well the model predicts the 4 actions;
![Screenshot 2023-08-28 091741](https://github.com/LaseTawak/Predicting-Next-Action-in-Football-Matches/assets/69163893/868f05e0-e1fb-4fe1-a588-a3f967da3541)

The final and selected model showed that it could do a great job at predicting the next action of a team in a football match. The confusion matrix produced by this model on the test is shown below. The model showed its best performance in predicting a player attempting to run or dribble with the ball as the next action, recalling 81% of such actions. The model was also  at predicting when a shot would be taken, this is particularly interesting given the class was the least represented in the dataset.

Furthermore, the ability of the model to accurately recall the next action as a Pass or Cross was at an above average rate. Even with the overall strong performance of the model and high representation of Passes, the confusion matrix showed the model struggled in predicting Passes, misrepresenting 20% of them for dribbles. 

From the context of football matches, this confusion might be attributed to the possibility that passes in attacking situations are used to move the ball closer to the oppositions goal, which is also usually the main reason for running with the ball or trying to dribble. It can also be because of the data structure, the sequence of most events in the dataset, where dribbles are usually followed by passes. This common sequence could have resulted in the model picking up a sequence bias. Also, because of the creativity that comes from players in playing football, the mislabeling of passes might be because of each player's unique decision making in breaking out patterns and drawing on their own inspirations.
