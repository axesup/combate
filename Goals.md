# Goals
Goals are the way CodeCombat decides whether or not a level is completed. They are used by the achievement system to award completion as well because it is possible to beat a level without completing all the optional goals.

## Structure of a Goal
#### Name
This is what displays in the goal panel.
#### i18n
Be sure to include this field so translators can translate the goals.
#### ID
A specific identification string to reference the goal programatically.
#### World Ends After
How long after the goal is completed to end the level.
#### How Many
How many times this goal needs to be satisfied to complete.
#### Hidden
If this goal only appears after failure. Usually it is implied that the hero must survive, so it remains hidden until the hero dies. 
#### Optional
This is to signify a goal as optional. If it isn't required to get the gems before escaping, the goal is optional.
#### Save Thangs
What Thangs to save. This can be a specific Thang ID or a whole team.
#### Get To Locations
Which locations specific Thangs need to get.
#### Code Problems
Whether or not code problems are allowed.
#### Leave Off Sides
If specific units need to escape off the sides of the map.
#### Lines of Code
Check if there is a limit on how many lines of code required.
#### Keep From Leaving Off Sides
Prevent certain units from leaving off the side of the map.
#### Team
This is specifically for multi-player levels. Each side has their own victory goals, for example, a Human needs to slay all the Ogres and an Ogre needs to slay all the Humans. Each goal would be assigned to the individual team.
#### Get All To Locations
An expansion on how many need to get to a location.
#### Kill Thangs
A very basic goal. Usually killing all the Ogres on a map.