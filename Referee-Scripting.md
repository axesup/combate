**Note:** All scripting is done in [CoffeeScript](http://coffeescript.org/)!

Levels in CodeCombat quickly exceed the simple pre-existing structure that the Dungeon displays. When you are ready to make a more advanced level, you'll want to make a Referee to control the rules of the level. The Referee has complete control over the map at all times. They can even kill the Hero instantly, if the programmer of a level's so wills it. Below are some tips to get started.

## Making a Referee
Add any static Thang to the level and give it a Referee component. We recommend using a Well and placing it out of the field of view.
## Explanation of Extra Code
Add the Extra Code field to the Referee to begin your custom scripting.
### setUpLevel
This function happens exactly once at the start of the level. This is when you'll want to build the level, as this happens even before the hero is added.
### onFirstFrame
This function happens exactly once, as well, but this time this happens after the hero is all set up and about to begin.
### chooseAction
This function happens once every frame. This is a good place to custom write some logic.
### checkVictory
This is similar to the chooseAction, however this is a good place to delegate all victory checks as convention.
## Useful code:
`@world.getThangByID "Thang ID"` returns a Thang by it's ID.  
`@hero` is a predefined variable for selecting the hero.
## Advanced Goals
`@world.setGoalState "goal-id", "success" # or "failure"` Set a goal state at any time.