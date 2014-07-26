#Code Connections in SpriteBuilder


Code connections are a powerful feature of SpriteBuilder. They are used to add custom code to scenes and nodes created in SpriteBuilder.

##Custom Classes

In the right panel you can set a custom class for any node:

![image](code-connection.png)

Any node added in SpriteBuilder can be backed by a custom class. When a `CCNode` with a custom class gets displayed in the scene, the custom class is instantiated. Cocos2D calls `didLoadFromCCB` on any custom class, as soon as the corresponding node and all the children have been loaded completely.

> Note: It is important that the custom class is a subclass of the node type you chose in SpriteBuilder. For example: You create a hero in SpriteBuilder which is a `CCSprite`. You want to create a custom class for that hero. It needs to be a subclass of `CCSprite`.

###Common use cases for custom classes

####Custom classes for scenes
A developer will use custom classes for almost every scene in his game. One simple example is activating touch handling on a gameplay scene:

- Create a Gameplay scene in SpriteBuilder
- Create a Gameplay class in Xcode, it needs to be a subclass of `CCNode`
- In SpriteBuilder set the custom class of Gameplay to `Gameplay`
- In `Gameplay.m` implement `didLoadFromCCB`
- In `didLoadFromCCB` call `self.userInteractionEnabled = TRUE`

####Custom classes for game objects
Most games will create custom classes for heroes or enemies. For example a developer could create an enemy with a certain movement pattern. 

- Create an Enemy Sprite in SpriteBuilder
- Create a Enemy class in Xcode, it needs to be a subclass of `CCSprite`
- In SpriteBuilder set the custom class of Enemy to `Enemy` 
- In `Gameplay.m` create and apply a `CCAction` in the `init` method
