In our [[Thang Component System]] architecture, the Systems fulfill three roles.

1. Systems are unto Levels as [[Component]]s are unto [[Thang]]s. For example, if I want my Level to have gravity, I add the `Movement` System and configure its gravity to 9.81 m/s^2.
2. They also serve as namespaces for the Components. As an example, the `Physics` System doesn't actually do anything on its own yet, but it was a good place to put `physics.Physical` Component, which controls the size, shape, rotation, and position of all physical Thangs.
3. They can coordinate behavior across those Components. For example, the `Collision` System will look at all the Thangs which have the `collides` property set and update its Box2D-based collision simulation once per frame, instead of each Thang with a `Collides` Component trying to figure out its own collision interactions.

![Example: the Movement System](https://s3.amazonaws.com/files.codecombat.com/wiki-images/movement_system.png)

You can also live-edit the code for any System directly within the Systems tab of the Level editor, just like in the [[Component]] example.

To see all the entity data for, say, the `Movement` System, I can just go to [http://localhost:3000/db/level_system/movement](http://localhost:3000/db/level_system/movement).
