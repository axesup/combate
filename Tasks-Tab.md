# Tasks
Below you will find some information on default tasks for creating a level for CodeCombat. These have been resorted in order that they should occur during the natural progression of a level.
## Prototyping
#### Build the level.
Building the level is often the first step in creating a new CodeCombat level. Survey the landscape. Place the floor. Add some trees. Add some ogres and a few humans and boom! You have the start of your own level.
* **Important**: Include a Hero Placeholder or there will not be a programmable Hero included in the level!

#### Create a Referee stub, if needed.
If your level will require any custom logic (spawning ogres, calculating the final score, listening for specific commands,) you will want to create a referee which monitors the level and performs actions. Not all levels need a referee, but as level complexity goes up, it is often easier to script things inside a referee instead of trying to set up the logic by hand.
* **Further Reading:** [Referee Scripting](https://github.com/codecombat/codecombat/wiki/Referee-Scripting)

## First Draft
Once the prototype has been made, it's time to finalize a few aspects of the level before sharing it with the public. It's mostly about putting a good foot forward when demoing your level to the masses.
#### Name the level
The best level names aren't too long... **Destruction of the Evil OGre FORTRESS DOOM DAY!!!!** is no where as elegant as **Fortress Assault**. One of the best rules for a good name is not to over think it. Don't worry about giving it a placeholder name until that perfect name strikes you.
#### Write the sample code.
Since CodeCombat is a game about programming, the sample code plays an important part in how the level plays. Giving no sample code makes for a difficult level. Giving too much sample code means after a few lines the game plays itself. It is important to find the balance as to create an interesting challenge for players to solve.
* **Further Reading:** [Sample Code](https://github.com/codecombat/codecombat/wiki/Sample-Code)

#### Do basic set decoration.
A different task from actually building the level. Once the prototype is established, you'll want to begin filling out some of the details that will make your level unique. Alcoves, tents, rocks, and general doodads will help differentiate your level from the rest.
#### Set up goals.
The goals are how you decide when a player has succeeded or failed. Is killing all the ogres required? Or is losing 0 humans? How about reaching a specific point in the map? There are many more ways to complete a level, but some might require custom scripting to get working correctly.
* **Further Reading:** [Goals](https://github.com/codecombat/codecombat/wiki/Goals)

#### Adjust script camera bounds.
If you made any changes to the overall size of the level after creating the basic shape you'll want to go in and make sure the camera bounds are set up correct.
* **Further Reading:** [Scripts](https://github.com/codecombat/codecombat/wiki/Scripts)

#### Publish.
Once the previous tasks are complete, you're ready to publish the level. Your level isn't visible to the public until the level has been published.

[<img align="center" width="50%"src="http://files.codecombat.com/wiki-images/publish.png"/>](http://files.codecombat.com/wiki-images/publish.png)

## Improve
With the level put to the public, feel free to share your level's URL with your friend, on the forums, and in the Slack channel. People will gladly give you feedback and you will ned to take that feedback and make meaningful changes to improve your level! Don't worry, no level is perfect on the first draft.
#### Do thorough set decoration.
When you settle on the concepts and gameplay of your level, it's time to finish the visuals for the level. All tasks are suggestions so don't worry about tweaking things later. But, when you finally hone in on the motif of the level, you'll realize you're placing the last few sprites and everything looks perfect.
#### Write the description.
Describe your level. Once again, shortness is sweetness. Don't be afraid of being silly. CodeCombat is light hearted so humor is always welcome.
#### Write the guide.
This is where you will provide in detail help for players who may need it. It is your choice how detailed you will go into further hints, but we recommend not providing the full solution inside the guide. Instead reiterate the concepts the players will need to demonstrate to finish the level. Give a few level-specific code snippets that may lead the player to figuring out the solution.

[<img align="center" width="50%"src="http://files.codecombat.com/wiki-images/guides.png"/>](http://files.codecombat.com/wiki-images/guides.png)
* **Reference:** [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

#### Choose the Existence System lifespan and frame rate.
The Existence System is the system that updates each Thang individually. If a Thang isn't recognized by the Existence System, well, it doesn't exist. This system controls how long the level goes for (**Lifespan**) and how often it updates (**Frame Rate**). This is a process-heavy system, so it is important to optimize it. If fine details are important for your level, you will want a high frame rate, but, as a tradeoff we recommend shortening the lifespan. If the level is a long level, (60 seconds+,) we recommend dropping the frame rate to 15 or even 8.

**Location:**

1. Click the Settings tab at the top of the editor.
2. Expand Existence.

#### Choose the UI System paths and coordinate hover if needed.
The UI System creates a layer of content over the battlefield. The path that the hero has walked and mousing over specific coordinates are provided by the UI System. If the user has no need for coordinates (dungeon with simple boots,) then they can be turned off. If a level doesn't need to display all the paths traversed by the play (e.g. lots of back-tracking, jumbled looking path lines, or the level isn't explicitly movement centric,) then that can be turned off.

**Location:**

1. Click the Settings tab at the top of the editor.
2. Expand UI.

#### Choose the AI System pathfinding and Vision System line of sight.
The AI System handles interactions between all Thangs inside the level. "Can I see an enemy?" "How am I going to get there?" are some questions the AI System answers for the Thangs. It is a processing-heavy system, so it is important to get these values correct for your level. If the level is wide open, there is no need for pathfinding or line-of-sight. If the level is in the Dungeon with lots of turns? The AI system needs to create paths for the Thangs to navigate.

**Location:**

1. Click the Settings tab at the top of the editor.
2. Expand UI.

## Final Steps
Nearing release? Have you gotten it reviewed by friends and peers alike? Ready to see your name in lights? There are a few more important tasks you'll need to knock out. Mostly 
#### Click the Populate i18n button.
i18n is shorthand for 'internationalization' ... Now you can see why we use the short version! Pressing this button includes the necessary fields for the Diplomat team to translate the various strings inside your level.

[<img align="center" width="50%"src="http://files.codecombat.com/wiki-images/populate_i18n.png"/>](http://files.codecombat.com/wiki-images/populate_i18n.png)

#### Add i18n field for the sample code comments.
The sample code i18n is a special i18n field that needs to be added after the sample comment field has been added. Just create the i18n object field under the comments and you are good to go.
#### Add programming concepts covered.
CodeCombat uses a category system for describing which topics are covered, per-level. Early on in the campaign the only skill being taught is *Basic Syntax*, but soon we introduce *While Loops* and *Conditionals*. We use these to keep track of which concepts are being taught.
* **Further Reading:** [Programming Concepts](https://github.com/codecombat/codecombat/wiki/Programming-Concepts)

#### Remove/simplify unnecessary doodad collision.
The Collision System is process heavy. Having 100+ doodads each with a collision group can significantly impact level render times as the number of Thangs increase. The more collision objects that can be simplified into squares, the better.
* **Further Reading:** [Simplify Collision](https://github.com/codecombat/codecombat/wiki/Simplify-Collision)

#### Choose leaderboard score types.
There are a variety of leaderboard score types. Time until the level was beat, amount of gold earned, damage done, damage taken. Picking a score type allows players to compete against each other on the leaderboards!
#### Choose music file in Introduction script.
Choose a different music file if needed. Music helps set the mood, so be sure to check them all out!
* **Further Reading:** [Scripts](https://github.com/codecombat/codecombat/wiki/Scripts)

#### Choose autoplay in Introduction script.
Some levels are better if they start autoplaying or not. Often times, auto-playing with a failure is a good way of teaching how to solve a puzzle. Use Scripts to your advantage!
* **Further Reading:** [Scripts](https://github.com/codecombat/codecombat/wiki/Scripts)

## Verify
It is important to verify your levels work with heroes of varied speed and toughness.
#### Playtest with a slow/tough hero.
Sometimes slow heroes can't reach the objective in time. Sometimes heroes can be too strong and tank everything you throw at them! It is important to test these things to verify that the player must accomplish the goal, instead of simply surviving.
* The slowest hero is **Okar Stompfoot** wearing **Defensive Boots**

#### Playtest with a fast/weak hero.
Conversely, some heroes can be so fast that they outrun everything. Or, maybe, consistently low-health characters randomly die. While CodeCombat encourages players to upgrade their armor as the worlds progress, it is important to check that there is no random miscellaneous damage constantly being dealt. Check which world the level should belong and downgrade the armor by a tier or two. Can it still be beat, with a good solution?
* The fastest hero is **Pender Spellbane** wearing **Softened Leather Boots** and the **Ring of Speed**

#### Playtest with a couple random seeds.
If the outcome of your level depends on some random variables, (which ogres to spawn, how many coins spawn,) it is important to test a few seeds.
* You can test a few seeds by solving the level then clicking **Submit**, **Skip** and then, on completion, the **Esc** key, rinse and repeat ~10 times. Each time you press **Submit** a new seed is used. **Skip**ping exits the real-time playback, then once the level is complete **Esc** closes the victory pop up.

#### Make sure the level ends promptly on success and failure.
If a level only has an *existence* of 30 seconds, and the last ogre always dies on the 28th second, you don't want the level to end after 3 seconds! Or maybe the hero dies 15 seconds in, it is important to check the level ends *when* they lose so they can debug what went wrong, instead of losing track of what's happening 10 seconds later.
## End Optional
These tasks are not important to the release of a level. However, they help us keep track of which tasks still need to be done to a level. If you can do them, great!
#### Add Clojure/Lua/CoffeeScript.
It's important to write up the code for the extra languages offered by CodeCombat. However, we don't expect everyone to know the structure of all the languages, so this can be left up for other contributors to submit a patch.
#### Write a loading tip, if needed.
If there is a tip that is short and sweet and absolutely must be delivered to the player, use the loading tip to deliver it.
## Chief Artisan Only
Don't worry about these tasks, these will be performed by the Chief Artisans at CodeCombat. However, it is always educational to see how things work behind the scenes!
#### Create achievements, including unlocking next level.
Create the achievements for this level. Always one for the completion of the level, sometimes extra for optional goals (statement-count, bonus-goals.) Be sure to set the rewards appropriate for the final location for the level. If inserting somewhere in the middle of the campaign, include the level after it as a reward.
#### Add to a campaign.
Go to the campaign editor and add the level to the campaign. Move the level circle to where it needs to be. Pay attention to where it is placed, as the level flags must be taken into consideration. Rearrange the side panel so the level is easily findable when giving a quick look.
#### Choose level options like required/restricted gear.
Inside the campaign editor, add required/restricted gear. Some important categories to include/limit: `feet, `eyes`, `neck`, `wrist`, `minion`. Restrict weapons if the level is a building level. Double/triple check per level. 
#### Release to adventurers via MailChimp.
Create a blurb about the level for the Adventurer team and send it out.
#### Mark whether it requires a subscription.
Some levels which are of exceptional quality will be included as optional, subscriber-only levels for users to enjoy.
#### Release to everyone via MailChimp.
Include in the final campaign, open to the public.
#### Check completion/engagement/problem analytics.
Monitor potential problems with the level to make sure it isn't too hard for players.
#### Add a walkthrough video.
Record a video giving a step-by-step solution to the level.