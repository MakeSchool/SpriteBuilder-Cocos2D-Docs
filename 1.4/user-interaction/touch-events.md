# Touch Events

All nodes inherit from [CCResponder](http://www.cocos2d-swift.org/docs/api/Classes/CCResponder.html) which provides the user interaction functionality.

## Enabling Touch Events

To receive touch events for a node, you have to enable `userInteractionEnabled` and implement at a minimum the `touchBegan:withEvent:` method in the node's subclass. 

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
Implementing the `touchBegan:withEvent:` method is mandatory for touch events to work even if you only need to use `touchMoved:withEvent:`.
</td></tr></table>

So to enable touch events run the following code in the node's subclass, typically you would add this to `init` or `didLoadFromCCB` or `onEnter` methods:

	// Objective-C
	self.userInteractionEnabled = YES;
	self.multipleTouchEnabled = YES; // required for tracking multiple touches
	
	// Swift
	userInteractionEnabled = true
	multipleTouchEnabled = true // required for tracking multiple touches
	
## Customizing Input Behavior

The [`claimsUserInteraction` property](http://www.cocos2d-swift.org/docs/api/Classes/CCResponder.html#//api/name/claimsUserInteraction) will continue to send touch events to the node that received the initial touch events. This allows the user to touch a node, then move outside the node while still sending the touch events to the touched node. Without this property, the node would stop receiving touch events if the touch moved away from the node.

If the [`exclusiveTouch` property](http://www.cocos2d-swift.org/docs/api/Classes/CCResponder.html#//api/name/exclusiveTouch) is enabled, the node will be the only one to receive touch events but only if the initial touch began event occured on the node with `exclusiveTouch` enabled.

The [`hitAreaExpansion` property](http://www.cocos2d-swift.org/docs/api/Classes/CCResponder.html#//api/name/hitAreaExpansion) allows you to expand the node's bounding box in all directions by the given amount (in points).

## Implementing Touch Event Methods

There are four touch events that correspond to the different phases a touch goes through: began, moved, ended or cancelled. The latter two are mutually exclusive, and this is important to consider!

For instance a system event or gesture recognizer may actually cancel touch events, which will cause the *ended* event to never run. But if you rely solely on *ended* to end your touch events, that will likely cause bugs. A best practice, until you need to handle *cancelled* events specifically, is to simply forward the cancelled event to the ended event, as shown in these example touch event method implementations:
 
 	// Objective-C
 	-(void) touchBegan:(CCTouch *)touch withEvent:(CCTouchEvent *)event {
	}

	-(void) touchMoved:(CCTouch *)touch withEvent:(CCTouchEvent *)event {
	}

	-(void) touchEnded:(CCTouch *)touch withEvent:(CCTouchEvent *)event {
	}

	-(void) touchCancelled:(CCTouch *)touch withEvent:(CCTouchEvent *)event {
		[self touchEnded:touch withEvent:event];
	}


	// Swift
	override func touchBegan(touch : CCTouch, withEvent: CCTouchEvent) {
    }
    
    override func touchMoved(touch : CCTouch, withEvent: CCTouchEvent) {
    }
    
    override func touchEnded(touch : CCTouch, withEvent: CCTouchEvent) {
    }
    
    override func touchCancelled(touch : CCTouch, withEvent: CCTouchEvent) {
        touchEnded(touch, withEvent: withEvent)
    }

Note again that implementing the touchBegan method is mandatory for touch events to be sent to the node.

## CCTouch and CCTouchEvent

As you can see, the touch event methods receive [CCTouch](http://www.cocos2d-swift.org/docs/api/Classes/CCTouch.html) and [CCTouchEvent](http://www.cocos2d-swift.org/docs/api/Classes/CCTouchEvent.html) objects. They are light-weight, platform-independent wrappers for the platform-specific touch event objects (ie UITouch, UIEvent and NSTouch, NSEvent).

The CCTouch event specifically allows you to convert the touch location to either the node or the world coordinate space via [`locationInNode:`](http://www.cocos2d-swift.org/docs/api/Classes/CCTouch.html#//api/name/locationInNode:) and [`locationInWorld`](http://www.cocos2d-swift.org/docs/api/Classes/CCTouch.html#//api/name/locationInWorld).

## Touch Event Update Rate

Touch events are sent as often as once per frame, meaning you'll receive 60 updates per second at most.

While this sounds like a lot, it can still easily happen that a user swipes across the screen so quickly that the distance between the previous and current touch location can be several dozen if not hundreds of points apart.

If, for instance, you allow the user to draw lines by moving the finger across the screen you will inevitably see jagged lines rather than smooth curves, more so the faster the finger is moved. You can only counteract this effect through interpolation or smoothing the edges using an appropriate algorithm.

