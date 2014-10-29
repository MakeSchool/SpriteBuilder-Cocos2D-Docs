#Scenes in Cocos2D

In Cocos2D you have to have a `CCScene` as the root node of your scene graph. `CCScene` is a subclass of `CCNode`. Any `CCNode` subclass can be added to a scene by using the `addChild:` method. By default any `CCScene` is initialized as a full screen node. Only one `CCScene` can be active at a time. The currenty active scene is considered *on the stage*.


##Scene lifecycle
Cocos2D provides multiple lifecyle events that can be relevant for your scenes and other nodes in your scene. These events are trigerred when a scene gets initialized and when it becomes active/inactive. Each of the scene transition events is represented by one method in `CCNode` that gets called by the `CCDirector`. You can override these methods in any `CCNode`. The Objective-C default initializer method `init` gets called when scene/node is initialized from Cocos2D code. When you created your scene/node in SpriteBuilder `didLoadFromCCB` is the designated initializer method. Here is an overview of all the lifecycle methods:

* **init**: The default Obj-C initializer. If the scene is not created in SpriteBuilder you mostly use this method to build the scene by adding different nodes as children.

* **didLoadFromCCB**: **If you created your scene in SpriteBuilder** this method is called when the complete scene is loaded and all code connections are set up. You implement this method to access and manipulate the content of the scene. You cannot access child nodes of the scene or code connection variables before this method is called.

* **onEnter**: This method gets called as soon as the replacement of the currently active scene with this scene begins. If you are using an animated scene transition this method will be called at the beginning of the transition. You can add any code that shall be executed when the scene starts to enter the stage.

* **onEnterTransitionDidFinish**: If you are using an animated scene transition this method will be called when the transition finishes. If you are not using transitions this method is called at the same time as `onEnter`. Implement this method to execute code once the scene has fully entered the stage.

* **onExit**: Is called when the scene leaves the stage. If the scene leaves the stage with a transition, this event is called when the transition finishes.

* **onExitTransitionDidStart**: Is called when the scene leaves the stage. If the scene leaves the stage with a transition, this event is called when the transition starts.

> **Note:** you have to call the super implementation when you override `onEnter`, `onEnterTransitionDidFinish`, `onExit` or `onExitTransitionDidStart`.

