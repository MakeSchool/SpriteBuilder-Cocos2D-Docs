#Working with the CCDirector

Cocos2D structures scene managment so that a single class, the CCDirector, oversees the loading, unloading and status of all scenes in the game.  The CCDirector provides a mediated interface with OpenGL as well, allowing the render loop to bo paused or stopped, and setting different OpenGL properties like the pixel format and alpha blending.  These methods are detailed in the CCDirector API [here.](http://www.cocos2d-swift.org/docs/api/Classes/CCDirector.html)

The CCDirector is a singleton.  This means there is one and only one for the whole game, which makes sense since it oversees the loading and unloading of all other scenes/game content.  As a result, in order to access the CCDirector the standard syntax is [[CCDirector sharedDirector] methodName].