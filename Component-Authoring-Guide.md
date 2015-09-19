#Component Authoring Guide
Contained within will be some tips and tricks as well as solutions for common "gotchas" that might afflict the inexperienced Artisan.

##General Tips
###Structure
The following is a broad overview of what occurs under the hood:
####World
[World Base Class](https://github.com/codecombat/codecombat/blob/master/app/lib/world/world.coffee)  
The world contains a set of Systems, Thangs and their Components.
####System
[System Base Class](https://github.com/codecombat/codecombat/blob/master/app/lib/world/system.coffee)  
Systems are a set of actions that are performed on applicable Thangs.  
* The Collision System ensures collision objects don't overlap.
* The AI System controls the logic for the NPCs, such as Yaks or Ogres.

####Thang
[Thang Base Class](https://github.com/codecombat/codecombat/blob/master/app/lib/world/thang.coffee)  
Thangs are individual entities which contain Components.
* An Arrow is a Thang.
* An Ogre is a Thang.

####Component
[Component Base Class](https://github.com/codecombat/codecombat/blob/master/app/lib/world/component.coffee) 
Components are parts which sum to make an entire Thang.
* A common Peasant is made up of the following:
 * Acts
 * FindsPaths
 * Allied   
...
 * Sees
 
###Spells
Describe how to efficiently make a spell here.
###Abilities
Describe how to make an ability.
###AI
####Casting Spells
* Enemies consist of very rudimentary intelligence. Spell-based enemies (such as Shaman,) employ the component 'ai.AutoCasts' for their spell repertoire, which automatically cycles through all their available spells and attempts to cast them if they are off cooldown.
 * Note that the actual logic (who they are casting on, when to cast,) is locked in the individual function defined inside the spell.

###Spawning
* If your Thang spawns another Thang (such as shooting or summoning,) you must include a "requiredThangTypes" in the config schema, as this preloads the assets required.
* If spawning in a location, be sure to check to see if the position to spawn is actually 'clear' of obstacles. 

##Common Gotchas
* When creating a programmable action (such as bash or summon,) it needs to be added to the programming.Plans PlannableMethods array.