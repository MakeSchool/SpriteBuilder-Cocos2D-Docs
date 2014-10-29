#Scenes in Cocos2D

In Cocos2D you have to have a `CCScene` as the root node of your scene graph. `CCScene` is a subclass of `CCNode`. Any `CCNode` subclass can be added to a scene by using the `addChild:` method. By default any `CCScene` is initialized as a full screen node. Only one `CCScene` can be active at a time. The currenty active scene is considered *on the stage*.

##Scene Graph and Scene Management

Each `CCScene` stores a hierarchy of different `CCNode` instances. `CCScene` itself is an invisible node that is only used as a container. Most `CCNode` subclasses are used to present an object on the screen (a single color surface or a texture). The hierarchical structure of `CCNode` instances is called the *scene graph*.

The following diagram shows multiple different scenes and scene graphs of a game:
![image](scenegraph.png)
	
The diagram represents three different scenes of which each contains
multiple nodes. There are a couple
of takeaways from this diagram:

* **CCDirector** is the instance that controls which scene gets presented on the stage. One can tell `CCDirector` to present the main menu,
  the gameplay scene or the highscore scene. `CCDirector` will only
  present one scene at a time.
* **CCScenes** are used to build a logical group of objects. In
  Cocos2D this always means one scene represents one screen. One will
  have scenes for menus, leaderboards, gameplay, etc. Scenes itself don't have
  a representation, their sole goal is to group `CCNode` instances.
* **CCNodes** Basically anything that is visible in Cocos2D
  is a subclass of `CCNode`.

Games in Cocos2D consist of different scenes. The flow of the game is defined by telling the `CCDirector` when which scene shall be presented (menu first, then gameplay, then leaderboard). The content of the scenes is a compilation of different nodes.
A `CCNode` can again contain other `CCNode` instances. The hierarchy of `CCNode` instances in a scene is called the scene graph.