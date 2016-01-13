<div style="text-align:center"><img src ="https://popey456963.github.io/s/CoCo.png" /></div>

Hello [Archmages](http://codecombat.com/contribute/archmage)! Welcome to the developer wiki for CodeCombat. These documents are designed to give you everything you need to know, technical and non-technical, to dive into the project. If you see an opportunity to improve the docs, go ahead!

###Index:
* [Contact Us](#contact-us)
* [Starting Off](#starting-off)
* [Reading Material](#reading-material)
* [FAQ](#faq)

####Contact Us

There are a variety of ways to get help with CodeCombat related things.  We have [a developer chat room on Slack](https://coco-slack-invite.herokuapp.com/) (or [HipChat](https://www.hipchat.com/gkaufqwnj) if you prefer not to register).  Most people are in US Pacific Time (~GMT-8) but there are usually a few other players awake at other times.  We have a HipChat room for off-topic discussions [here](http://www.hipchat.com/gaXOD7lQ8).

The [Discourse Forum](http://discourse.codecombat.com/) is another useful place to get help.  For more information check out the [main chat page](https://github.com/codecombat/codecombat/wiki/Chat-Room).

####Starting Off
1. Set up the [Developer Environment](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information).
1. Make a small first commit such as [creating a new Thang name](https://github.com/codecombat/codecombat/issues/53), [adding tips to the loading screen](https://github.com/codecombat/codecombat/issues/710) or [adding documentation](https://github.com/codecombat/codecombat/issues/1237).
1. Check out the [Good for Newbies Issues](https://github.com/codecombat/codecombat/labels/good-for-newbies).
1. Browse the wiki to learn something new!
1. Fix [bugs](https://github.com/codecombat/codecombat/labels/bug).
1. Bring up new ideas in our [Slack channel](https://coco-slack-invite.herokuapp.com).

####Reading Material
######General:
* [[Mission Statement]]
* [Developer Environment](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information) - Start here to get CodeCombat set up on your computer.
* [[Developer Organization]]
* [[Coding Guidelines]]
* [[Technical Overview]]
* [[Third Party Software and Services]]
* [[JSON-Schema]]
* [[Coco Models]]
* [[Testing]]
* [[Git Policies]]

######Frontend Development:

* [[Client Models]]
* [[Views]]
* [[Events, Subscriptions, Shortcuts]]

######Backend Development:

* [[File System]]

######Key Systems:

* [[Versioning]]
* [[Permissions]]

######Game Engine:

* CodeCombat uses a [[Thang Component System]] architecture.
    * A [[Thang]] can be an ogre, a land, an arrow--anything.
    * Thangs are just clusters of [[Component]]s.
    * [[System]]s organize the Components.
* [[World]]s simulate deterministically.
* The [[Surface]] is what we call our graphics layer.
* The [[Tome]] is our spell editor.
* [[Multiplayer]].

######Side Projects:

* [[Treema]], our general interface for editing JSON data with schemas.
* [[Aether]], our transpiler.

####FAQ
######How do I learn Git?

Doing [this](https://www.codeschool.com/courses/try-git) quick course should get you up to speed with Git.

######What are some larger projects I can do?
[[Here's our big project ideas list|Project Ideas List]], which should give you some ideas about what you can contribute on.