### Index

* [Intro](#intro)
* [Debugging](#debugging)
* [Other-ways](#other-ways)

#### Intro

When you are creating levels from the level editor, you'll usually see a message that says **Infinite loop detected, unable to load level**. This guide will introduce you to debugging your own level from the level editor. 

#### Debugging

The first thing you do when getting out of the error message is by going to the console log of the browser.
* Go open the console using Windows:`CMD`+`Shift`+`J` and Mac: `CMD`+`ALT`+`J`.
* Check if there's any message like, `Error: Unable to load thang`.
* If it's something related to cannot spawn thang type, then it's the referee code that's probably wrong. Check if there's actually the thang in the spawnable and buildable component of the referee. 
* This also happens when there is too many thangs. So try deleting some if you have over 50+ moving thangs.
* Only have one hero in a level, if there's two heroes with some extra component, it'll return an error

#### Other ways

If you can't seem to debug, please feel free to ask for help on slack.codecombat.com or discourse.codecombat.com and we'll help you!