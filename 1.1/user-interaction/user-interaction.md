#User Interaction

Cocos2D 3.x provides an easy to use touch handling system. Every `CCResponder` can receive touches. `CCNode` inherits from `CCResponder` providing all `CCNode` subclasses with touch functionality. Additionally Cocos2D 3.x provides UI components that integrate User Interaction, for example `CCButton`. These will be discussed in the next chapter.

This chapter will provide information on adding custom user interaction to a Cocos2D application. Because `CCNode` is the only `CCResponder` subclass in Cocos2D we for simplicity will refer to touch handling using `CCNode` instances.

##Enabling touch handling on a CCNode

Any `CCNode` subclass can call following line to activate touch handling:

	self.userInteractionEnabled = YES;

> In most cases the user interaction should be enabled in the `onEnter` method.

##Receiving touches

Each `CCNode` subclass can implement as many of the four available methods as it wants to consume:

- `-(void)touchBegan:`
- `-(void)touchMoved:`
- `-(void)touchEnded:`
- `-(void)touchCancelled:`

The touch position provided as parameter of the above methods is expressed in the coordinate system of the *OpenGLView*. In most cases the position needs to be transformed to the node space of the receiving node.

This can be done as following:

	- (void)touchBegan:(UITouch *)touch withEvent:(UIEvent *)event
	{
	    // tranform touch location to this node's coordinate system
	    CGPoint touchLocation = [touch locationInNode:self];
	}
###Passing touches on in the responder chain

If you decide to not handle a touch and want to pass it on to the next touch responder in the responder chain, you need to call the according touch method on the `super` class.

##Enabling multi touch
`CCNode` instances in Cocos2D also support multi touch. Multi touch can be activated with the following line:

    self.multipleTouchEnabled = YES;

If multiple touches occur the corresponding touch handling methods will be called multiple times. Touching the screen of a device with three fingers will lead to `touchBegan:` beeing called three times.

Developers need to keep track of the amount of active touches manually, for example by storing references to them.


##Customizing a Node's hit test
A class called `CCResponderManager` detects which `CCNode` subclass has been touched by calling the `hitTestWithWorldPos:` method. By default `CCNode` implements this method by testing if the touch position is within the node's bounding box (position + contentSize).

If a `CCNode` subclass wants to provide a different touch detection shape it can override this method.

Additionaly there's a convenient way to increase the touch area of a `CCNode` by using the `hitAreaExpansion` property.

##See Also

- [Tutorial on Touch Handling](https://www.makegameswith.us/gamernews/366/touch-handling-in-cocos2d-30)
- [Tutorial on using Accelerometer](https://www.makegameswith.us/gamernews/371/accelerometer-with-cocos2d-30-and-ios-7)