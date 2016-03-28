Collision is an expensive part of any game, so when creating levels it is important to be considerate towards those with lower-end computers. Each movement-enabled collision Thang needs to check every other collision Thang to check for collisions! With 100 units in the scene, they each need to check against each other! That's 100 * 99 collision checks! That can be up to 9,900 math-heavy calculations, per frame!

To make a level that is easily accessible to everyone, it is important to simplify some of the collisions in the level. Take this example:

[<img width="50%" src="http://files.codecombat.com/wiki-images/before.jpg"/>](http://files.codecombat.com/wiki-images/before.jpg)

It sports a lot of detail! A dense forest surrounding a path through the woods. However, let's see how many collidable objects there are:

[<img width="50%" src="http://files.codecombat.com/wiki-images/count.png"/>](http://files.codecombat.com/wiki-images/count.png)

... 200+? The Collision system is going to have to check collision from the hero and any additional units we add 200+ times per frame! But, there is a way to solve this. Using the square 'Obstacle' Thang, we can create a simpler collision shape for the level. First, however, we must disable the collision for the Thangs we don't want to collide. For each Thang go into it's components and change it's collision category to `"none"`. This way heroes no longer collide with any of the trees.

[<img width="50%" src="http://files.codecombat.com/wiki-images/none-collision.png"/>](http://files.codecombat.com/wiki-images/none.png)

Now, finally, it's time to map out the basic square shapes to create a new, simpler collision shape:

[<img width="50%" src="http://files.codecombat.com/wiki-images/numbered.jpg"/>](http://files.codecombat.com/wiki-images/numbered.jpg)

Tada! Down from 200 to 11!

## Walls

Walls are a special case! You don't need to to this Collision Simplification for any Thang in the "Wall" category (Dungeon Wall, Ice Wall, etc)

## Keyboard Shortcuts

There are two keyboard shortcuts in the level editor that help with this process:

**Ctrl+\**  will toggle display of collision boxes.

**Alt+c** will toggle the selected Thang's collision box on and off.