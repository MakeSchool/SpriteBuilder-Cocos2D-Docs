# Scene Transitions

When presenting a scene via CCDirector you can optionally animate the transition via a CCTransition instance. This will load the new scene, and show it alongside the previous scene for the duration of the transition animation. 

The previous scene is said to be transitioning *out* while the new scene is said to be transitioning *in*.

## Playing a Transition Animation

A [CCTransition](http://www.cocos2d-swift.org/docs/api/Classes/CCTransition.html) instance can be used to animate every scene change for which there is a corresponding "with transition" method available in [CCDirector](http://www.cocos2d-swift.org/docs/api/Classes/CCDirector.html). They are:

	presentScene:withTransition:
	pushScene:withTransition:
	popSceneWithTransition:
	popToRootSceneWithTransition:

To present a scene with a transition, simply create an instance of the CCTransition class with the initializer that creates the desired transition effect, and then present the scene with the transition. For example:

#### Objective-C
	id scene = [MyScene node];
	id transition = [CCTransition transitionFadeWithDuration:2.0];
	[[CCDirector sharedDirector] presentScene:scene withTransition:transition];
	
#### Swift
    var scene = MainScene.node() as CCScene
    var transition = CCTransition(fadeWithDuration: 2.0)
    CCDirector.sharedDirector().presentScene(scene, withTransition: transition)

## Animating the Scenes during transition

By default, both scenes will neither run any scheduled selectors/blocks nor will any of the actions in the scene run. Basically both scenes are paused, or inactive.

To change this behavior so that you can see animations, particle effects, movement and what not happening even while the transition animation is playing, simply set these transition properties to YES:

#### Objective-C
	transition.outgoingSceneAnimated = YES;
	transition.incomingSceneAnimated = YES;

#### Swift
    transition.outgoingSceneAnimated = true
    transition.incomingSceneAnimated = true
		
## Improving Transition Performance

Since rendering and perhaps even animation two scenes at the same time can easily double the load on the device, the performance of transition animations may suffer. You have two options to alleviate or at least improve the situation.

First, you can change the scale of each scene:

#### Objective-C
	transition.outgoingDownScale = 4.0;
	transition.incomingDownScale = 2.0;

#### Swift
	transition.outgoingDownScale = 4.0
	transition.incomingDownScale = 2.0

The above example will downscale the outgoing scene to 25% (scale divided by four), thus rendering far fewer pixels. At the same time the incoming scene is scaled down to half its original size (scale divided by two). 

After the transition finishes the incoming scene will suddenly switch to full scale rendering however, which may be an undesirable side-effect. Typically it's best to scale only the outgoing scene.

You can also change whether Transitions should be animated with full Retina resolution:

#### Objective-C
	transition.retinaTransition = NO;

#### Swift
	transition.retinaTransition = true

The above code disables Retina rendering on Retina devices for the duration of the transition. This can greatly enhance transition performance on Retina devices but will leave non-Retina devices unaffected. Still, it is quite effective and during a scene transition animation one can hardly notice the difference between full Retina resolution and standard (point-based) resolution.

You may also be able to squeeze out a little more performance by changing the transition's texture pixel and depth stencil formats:

#### Objective-C
	// use a 16-Bit pixel color format (default: RGBA8888)
	transition.transitionPixelFormat = CCTexturePixelFormat_RGBA4444;
	
	// use an 8-Bit depth stencil format (default: 24-Bit)
	transition.transitionDepthStencilFormat = GL_DEPTH24_STENCIL8_OES;

#### Swift
    // use a 16-Bit pixel color format (default: RGBA8888)
    transition.transitionPixelFormat = CCTexturePixelFormat.RGBA4444
    
    // use an 8-Bit depth stencil format (default: 24-Bit)
    transition.transitionDepthStencilFormat = GLuint(GL_DEPTH24_STENCIL8_OES)

## Load Time and Transitions

To play a transition animation you need to present a new scene. In order to do that, you need to create a scene instance. This new scene however may take some time to load, especially if it needs to load textures and other resources. The effect is that a transition animation will not start playing until after the new scene has been fully initialized.

You can only play the transition animation in parallel to loading resource files by making use of private API methods. For instance CCTextureCache provides means to load textures asynchronously. However while loading the textures you can obviously not use any of the currently being loaded textures in the transition animation. 

Therefore transitions can not be used to implement a loading screen animation. Instead you can transition to a loading scene, and transition out of the loading scene when it has finished loading the resources required by the next scene.


## Transitions and Memory Usage

Technically when presenting a new scene both scenes are in memory in the frame where the new scene is presented, regardless of wheter you are using a transition or not.

However with scene transitions both scenes remain in memory for a longer time, possibly several seconds. This can raise additional memory warnings. It is not uncommon to hear a Cocos2D game crashing while presenting a new scene because that's when memory usage is highest.

In such instances the aforementioned loading screen will also help to prevent memory pressure, provided that you do not start preloading resource files in the loading scene's init but rather in [`onEnterTransitionDidFinish`](http://www.cocos2d-swift.org/docs/api/Classes/CCNode.html#//api/name/onEnterTransitionDidFinish) or later.

In such a case (and assuming correct memory management, ie no retain cycles, leaks) the in-between loading scene will allow the previous scene's memory to deallocate during the time of the transition before it starts loading the next scene's resource files.

## Types of Transitions

The available [transitions are documented in the class reference](http://www.cocos2d-swift.org/docs/api/Classes/CCTransition.html).
