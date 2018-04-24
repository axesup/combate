Documents from the database are loaded into the application through [Backbone](http://backbonejs.org/) [Models](http://backbonejs.org/#Model) and [Collections](http://backbonejs.org/#Collection). These are extended in the [CocoModel class](https://github.com/codecombat/codecombat/blob/master/app/models/CocoModel.coffee). There's also the [SuperModel class](https://github.com/codecombat/codecombat/blob/master/app/models/SuperModel.coffee) which coordinates the loading and populating of these models.

## Saving

Models that are not versioned save just as they normally do with Backbone Models.

To save a new version of a versioned model, use the CocoModel's cloneNewMinorVersion and cloneNewMajorVersion. Typically, the process is to modify the model as normal with 'set', then clone with the changes and save the clone.

Backbone does not natively support nested documents, which CodeCombat relies heavily on. Currently, the only way to set a subdocument is to set the root level property. See how LevelBus.coffee does this with LevelSession.

Patching is supported by the server. LevelBus.coffee also shows how this is handled.