CodeCombat uses something like an [Entity-Component-System architecture](http://www.gamedev.net/page/resources/_/technical/game-programming/understanding-component-entity-systems-r3013) ([read more](http://www.chris-granger.com/2012/12/11/anatomy-of-a-knockout/)), which is different from an old-school object-oriented game engine. The gist is that Entities are just pointers, and you compose them out of a bunch of Components which encapsulate data, and those are organized by Systems which add behavior and make the world tick.

But instead of "Entities", we call them "Thangs", since ain't no one got time for such a long, boring, irregularly pluralizable words as "Entitity". I mean, "Entity." (See?) So it's a Thang-Component-System architecture instead.

![Configuring the Tharin Thang with some Components](https://s3.amazonaws.com/files.codecombat.com/wiki-images/thang_component_system.png)

Thangs live inside Levels, where they are configured with Components, and the levels are similarly configured with Systems. In addition to Components, Thangs point to [[ThangType]]s, which hold all the art and sound information needed to display them--but ThangTypes have no impact on the Level's [[World]] simulation itself. You can make all the Ogres look like trees and they'll still crush the human soldiers--it'll just look hilarious when you go to play the level. For details, check the full article on [[Thang]]s.

The other big difference is that our Components include behavior. Lots of behavior. In fact, most of them are mostly behavior. Components copy their properties to their Thangs when attached, and some of these properties are methods. The Components all live in the database, so you can code them right from within the [[Level Editor]]--how cool is that? For details, check the full article on [[Component]]s.

Systems are unto Levels as Components are unto Thangs--also containing configuration data and methods, also live-editable from within the Level Editor. See the full article on [[System]]s.
