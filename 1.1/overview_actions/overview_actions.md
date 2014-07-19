#Using Actions to Manipulate Nodes

Although nodes  serve as the building blocks for Cocos2D games, it's actions, along with physics and touch feedbock, which bring the game to life.  In brief, actions provide an interface for manipulating the properties of nodes (size, position, rotation) during the game's runtime.  As a result, actions can be used to create animations and create game components like moving platforms or disapearing blocks.

All actions are descended from the class CCAction.  Some actions require a single frame, and the result will appear to be instantaneous in the game (flipping a node over, having a node disapear).  Other actions will happen over a period of time, with the game engine automatically interpolating the movement and apperance of the node over that time.  Still other actions can be set to repeat indefinetly, providing an easy way to make background images or looping character animations.

Understanding how to use actions will help you bring your game to life.