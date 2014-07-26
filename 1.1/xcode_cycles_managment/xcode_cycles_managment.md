##Creating a Scene
The default SpriteBuilder and Cocos2D projects come with one scene. For most games you will have to create additional scenes. You can either create scenes in SpriteBuilder or in code.
	
* Create a Scene CCB-File in SpriteBuilder and load the scene in code utilizing CCBReader:   
  
		CCScene *gameplayScene = [CCBReader loadAsScene:@"Gameplay"];
  
* Create a subclass of `CCScene` in Xcode and intialize:    
  
		CCScene *gameplayScene = * [GameplayScene scene];
		
###When to create the Scene content
For most games you will create the content for your scenes in SpriteBuilder or in the `init` method of your `CCScene` subclass. However, when certain scenes need to allocate a lot of memory it can be helpful to create the actual scene content in the `onEnter` method and removing it when `onExit` is called. This way the memory is only used when the scene is active on the stage.


##Switching between Scenes
The `CCDirector` is responsible for presenting and hiding scenes.
The easiest way to replace a scene, without a transition is using the `replaceScene:` method:

	[[CCDirector sharedDirector] replaceScene:gameplayScene];
	
Using this method the `CCDirector` will replace the currently active scene with the `gameplayScene`.

###Transitioned Scene Changes
If you want to provide a transition effect for swapping the scene you can use the `replaceScene:withTransition:`. It takes a `CCTransition` as parameter. A `CCTransition` can be easily created using one of the initializer methods that provide pre defined transition effects:

	CCTransition *transition = [CCTransition transitionCrossFadeWithDuration:1.f];
    [[CCDirector sharedDirector] replaceScene:gameplayScene withTransition:transition];

To get an overview of the different available transitions and the transition options, take a look at the Cocos2D class reference for [CCTransition](http://www.cocos2d-iphone.org/api-ref/3.0-rc1/Classes/CCTransition).

###Using the Scene Navigation stack
Another option instead of replacing scenes is pushing and popping scenes. When you push a new scene, the old scene gets deactivated but remains in a the stack of scenes. When you pop a scene that scene gets removed from the navigation stack and the top most controller of the navigation stack gets presented.

Cocos2D provides methods to pop and push scenes with or without transitions:

* `pushScene:withTransition:`
* `popScene:withTransition:`
* `pushScene:`
* `popScene`

Additionally there is a `popToRootScene` method that empties the complete navigation stack and returns to the first scene.

When building User Interfaces with multiple scenes (e.g. menu structures) you should use the navigation stack instead of manually replacing scenes. The most common pattern is to provide a *back* button that pops the latest scene on the navigation stack.


