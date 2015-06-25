###Index

* [Pre-Production](#pre-production)
* [Production](#production)
* [Iteration](#iteration)
* [Auto-Saving](#auto-saving)
* [Tasks Checklist](#tasks-checklist)

####Pre-Production

1. **Come up with a level idea**. If this is your first time building a level, we recommend something fairly simple, or a variation of an existing level.

####Production

1. **Create your level**. Go to the [level search page](http://codecombat.com/editor/level) and either make a brand new, blank level, or pick a level from the list and fork it, copying all the existing logic to have something to start from.
1. **Place down Thangs in the Thangs tab**. The Thangs tab is the tab open by default. [Read more...](Thangs Tab)
1. **Configure your Thangs**. Double click on A Thang in Thangs tab to edit its Components. [Read more...](Editing Thang Components)
1. **Setup Scripts**. These add dialogue, goals, music and more to your level. [Read more...](Scripts Tab)
1. **Sample Code**. Add the default code shown to the player when your level starts for the first time. [Read more...](Sample Code)
1. **Add Details**. In the Settings tab, give your Level a description, documentation, and a victory screen. [Read more...](Settings Tab)
1. **Configure Systems**. These control some higher level things associated with systems that don't often need to be changed, like teams, UI and gravity.
1. **Roll your own Components and Systems**. This is rather advanced, and due to security concerns, not enabled by default (we'll be building a community review system in the future so that it can be enabled). If you would like to do some custom logic, you can edit and add systems and components in the level editor but you won't be able to save them. Get in touch with us through our [public HipChat room](http://www.hipchat.com/g3plnOKqa) and we'll help you out. [Read more...](Components And Systems Tabs)
1. **Test test test**. Click 'play' in the upper right corner to play your level.
1. **Save and publish**. Check 'publish' when saving your Level to make it accessible to anyone.

####Iteration

No matter what you're building, regular and frequent iteration is key to making something incredible. Make a level and as soon as it's even a little bit usable, share it with us, with others, with anyone to get feedback. If you're not embarrassed by what you've built when you first demonstrate it, you're waiting too long.

To get feedback:

* Show us and others hanging out in our [public HipChat room](http://www.hipchat.com/g3plnOKqa).
* Post on the Artisan section of our [Discourse forum](http://discourse.codecombat.com/category/artisan).
* Link friends and family to it and have them play it.
* If you want the best possible result, consider UX testing it. It's a tough skill to learn, but extremely valuable.

####Auto-Saving

Whatever edits you make are saved in [localStorage](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage#localStorage) until you save them in the database. This way if you reload the page, any changes you make to the Level, Components and Systems are not lost. These are only stored locally on your browser, though, so if you clear your browser data any backups are lost. And you can only access those changes on the browser of the computer you used to make those changes. It's a fairly simple system to take the edge off the all-too-common case of losing work by closing the tab or reloading accidentally or the tab crashing.

If you want to throw out changes to anything, click 'revert' in the upper right area, and you can select what to revert.

####Tasks Checklist

If you want to include your level in the main campaign, you should add the Tasks checklist in the level settings and check off as many of the tasks as you can. Here are some tips on what some of them mean:

*1-* Choose the Existance System Lifespan and Frame Rate:

    Go into Systems --> Existance System's Configuration Triangle --> Framerate or Max Lifespan

It's good to set it to something around 15, if the level is complicated and running slowly it as low as 10 or 8.  The max lifespan is the time that it takes until the level ends, and it doesn't need to be too long.  The defualt is 60 seconds, but some levels can be as short as 30 seconds, whilst others longer.

*2-* Choose the UI System Paths and Coordinate Hover if needed.  Unless you need path dots to show hero motion for some particular reason in the level, turn the `showPaths` from "paused" to "never" in the UI System.

*3-* Choose the AI System to set the `pathfinding` and Vision System for `line of sight`.  These should usually both be true, but if you have a level where there is just an outer wall and no obstacles (like walls, cliffs or rocks) in the middle, you can set them both to false for much better performance.

_Sample Code - I understand but I can't find the function to do so?_

*4-* To place sample code:

    Double-click on the Hero Placeholder --> Click the programming.Programmable Component --> Find the programmableMethods configuration

You can add the sample code for the plan method, look at our existing levels that have sample code (not just comments) to see exactly how to format it.

*5-* Adjust script camera bounds.  If you are using a small level presets, this will work automatically.  Otherwise, you have to select the visible area in:

    Scripts --> Introduction --> Set Camera and Music --> Surface --> Cameras --> Boundary Configuration

You can click the crosshair button and Ctrl + Alt + Drag to select the camera region

*6-* Choose the music file, it is in the same place as the cameras bounds.  You can skip this one and I'll pick it, or you can choose music 1-5, with 1 being least intense (for laid-back levels) and 5 being most intense (for epic battles).

*7-* Remove/simplify doodad collision.  To make levels faster, you can turn collision handling off for all the little static doodads, and then put bigger obstacle rectangles over them, so there are fewer collision shapes.  Press `Ctrl + \` to toggle the collision overlay.  look for the little trees, ice crystals, barrels, etc.  Then, where there are a bunch of them, select each one and press `Alt + C` to toggle collision (it's collision shape should turn transparent).  Then you can add Obstacle Thangs to cover them.  You can resize the obstacles easily be pressing `Shift + Left/Right/Up/Down` when you have selected one to make it cover the right shape.

If you check out a level like Ice Soccer, you can see there are two big collision obstacles instead of a bunch of stalagmites (which have been deactivated).

*8-* Add IO/Clojure/Lua/Coffee-Script.  If you don't know anything about these languages, don't worry, other artisans and I will add the sample code for these based on the sample code that you write for either JavaScript or Python.

*9-* Click the `Populate i18n button` - If you've pressed it already and nothing has happened, don't worry, I can take care of this too.  It's finicky.

*10-* Check completion/engagement/problem analyitcs - The last several tasks, like this one and adding videos, are for us to do once the level has been released, to tune it based on where players are getting stuck.  Don't worry about getting them all.

I think it will also help if when you get a level ready to go, you post it on the forums, like "New Level: Kelvintaph Brawl", and link to the http://direct.codecombat.com/play/level/kelvintaph-brawl and describe it.  You might think about including a screenshot and a description of the level, and asking for playtests to play it and give feedback.  Once we have improved the level based on suggestions there, we can get it all polished up and ready to put in the main campaign.