# OS X Input Events: Mouse & Keyboard

On OS X you may want to react to Mouse and Keyboard events. Both are handled by [CCResponder](http://www.cocos2d-swift.org/docs/api/Classes/CCResponder.html) and thus available for all nodes.

## Enabling Mouse / Keyboard Events

To receive Mouse & Keyboard events you have to enable `userInteractionEnabled` for the node that should receive these events.

	// Objective-C
	self.userInteractionEnabled = YES;
	
	// Swift
	userInteractionEnabled = true

## Implementing Mouse Events

You implement the mouse event functions as follows:

	// Objective-C
	-(void) mouseDown:(NSEvent *)theEvent {
	}

	-(void) mouseUp:(NSEvent *)theEvent {
	}

	-(void) mouseDragged:(NSEvent *)theEvent {
	}
	
	// Swift
    override func mouseDown(theEvent: NSEvent) {
    }
    
    override func mouseUp(theEvent: NSEvent) {
    }
    
    override func mouseDragged(theEvent: NSEvent) {
    }    

There are two additional variants of these three mouse events:

- Events beginning with `rightMouse` deal with the same events but originating from the right mouse button.
- Events beginning with `otherMouse` deal with events originating from additional mouse buttons. 

The mouse event methods will run whenever a mouse button is first pressed or released, with the exception of the dragged event which will be called whenever the mouse moves while the corresponding mouse button is held down.

The app's title bar is not considered part of the window and clicking on it will not start generating mouse events for the app because doing that will drag the window.

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
Since even 3+ button mice may not actually generate these events (without a correctly functioning driver) and very few OS X users have a 3+ button mouse to begin with it is strongly recommended to refrain from relying on `otherMouse` events. At best they may be used as optional, additional input methods.</td></tr></table>

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
The dragged events will continue to fire even if the user drags the mouse cursor outside of the application window. Therefore be prepared to gracefully handle negative X/Y coordinates and coordinates larger than the game window's size!
</td></tr></table>

### ScrollWheel Event

To get scroll wheel information you have to implement the following event:

	// Objective-C
	-(void) scrollWheel:(NSEvent *)theEvent {
	}

	// Swift
	override func scrollWheel(theEvent: NSEvent) {
	}

The event's [`deltaY` property](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSEvent_Class/#//apple_ref/occ/instm/NSEvent/deltaY) tells you how many "steps" the scroll wheel has turned since the last event.

The deltaX and deltaZ properties may be used by multi-directional scroll wheels, but these are rare.

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
In System Preferences the user can change the **Scroll direction: natural** setting. This affects the deltaY values. With "natural" scroll direction, scrolling towards the user will create positive deltaY values but if "natural" scroll direction is disabled, rolling the wheel towards the user will generate negative deltaY values. Therefore you can not assume that a given scroll direction will be the same for all users, and depending on what you use the scroll wheel for you may want to offer a setting for users to inverse the scroll wheel direction.
</td></tr></table>


### Mouse Location

The [NSEvent](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSEvent_Class/) object provides you with mouse information.

Most importantly, if you want to get the current mouse location (in screen coordinates) you would do:

	// Objective-C
	CGPoint mousePosOnScreen = [NSEvent mouseLocation];
	
	// Swift
	let mousePosOnScreen = NSEvent.mouseLocation()

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
Note that the mouse's screen location is relative to the lower-left corner of the computer's main screen. Additional monitors can extend the desktop area *in any direction* but won't alter the mouse location's origin, so if the user has an additional monitor set up as extending the desktop towards the left, the X coordinates will actually be negative when the mouse cursor is on the monitor to the left!
</td></tr></table>
	
You will typically want the location of the mouse within the view (window) of the app or in world (scene) coordinates, for that you need to use the event's location instead:

	// Objective-C
	CGPoint mousePosInWindow = [theEvent locationInWindow];
	CGPoint mousePosInWorld = [theEvent locationInWorld];
	CGPoint mousePosInNode = [theEvent locationInNode:node];
	
	// Swift
	let mousePosInWindow = theEvent.locationInWindow()
	let mousePosInWorld = theEvent.locationInWorld()
	let mousePosInNode = theEvent.locationInNode(node)

If the Cocos2D view covers the entire window both *InWindow* and *InWorld* methods will return the same location. 

Furthermore, you do not need to further convert this location as it's origin is already at the lower-left corner, with positive X extending to the right and positive Y extending upwards, just like the regular Cocos2D coordinate system.

### Detecting Double-Clicks
	
Finally, the `clickCount` can be used to determine a double-click:

	// Objective-C
	BOOL doubleClicked = ([theEvent clickCount] == 2);
	
	// Swift
	let doubleClicked = (theEvent.clickCount() == 2)

## Implementing Keyboard Events

<table border="0"><tr><td width="48px" bgcolor="#d0f0ff"><strong>Info</strong></td><td bgcolor="#d0f0ff">
In Cocos2D v3.4.3 the OS X keyboard events were added to CCResponder. In earlier versions the keyboard events are not available.
</td></tr></table>

To process key events you have to implement these methods:

	// Objective-C
	-(void)keyDown:(NSEvent *)theEvent {
	}

	-(void)keyUp:(NSEvent *)theEvent {
	}

	// Swift
	override func keyDown(theEvent: NSEvent) {
	}

	override func keyUp(theEvent: NSEvent) {
	}
	
The keyboard event methods are called for each key that is pressed down or released. 

### Recognizing specific keys

You must use the [NSEvent keyCode property](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSEvent_Class/#//apple_ref/occ/instm/NSEvent/keyCode) to test which key's state changed. 

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
Using keyCode is the only way to ensure that the same physical key on the keyboard will need to be pressed on any keyboard. Using the `characters` string would only give you the letter of the key pressed after it went through the system's locale where it may have been transformed to a different letter. So while a developer using a US keyboard may find the '/' character to be suitable for making the character "jump", most european users would end up swearing at that developer because they are forced to press `Shift+7` in order to print the letter '/' that would then be recognized as making the character jump. Clearly it is not advisable to base your game's input on letters. And on top of that, you would have to test for both upper and lower case variants of a letter, too. By using the keyCode `kVK_ANSI_Slash` you ensure that all users regardless of their locale will have to press the same physical key "left of Right-Shift" in order to make the character jump.
</td></tr></table>

To get access to the key code constants you have to:

	// Objective-C
	#import <Carbon/Carbon.h>
	
	// Swift
	import Carbon

Add this to the class where you want to use the key code constants. A full list of the [key code constants is available here](http://stackoverflow.com/a/22662708/201863). Alternatively, just type `kVK_ANSI_A` or a similar 'kVK' constant in Xcode, then right-click the constant and choose *Jump to Definition* to open the framework header where the key codes are defined.

To give you a simple example that allows the user to make the character jump by either pressing the 'J' or 'Space' key:

	// Objective-C
	-(void)keyDown:(NSEvent *)theEvent {
		switch (theEvent.keyCode) {
			case kVK_ANSI_J:
			case kVK_Space:
				[self makeCharacterJump];
				break;
				
			default:
				// ignore unsupported keys
				break;
		}
	}

	// Swift
	override func keyDown(theEvent: NSEvent) {
	    switch Int(theEvent.keyCode) {
	    case kVK_ANSI_J, kVK_Space:
    	    self.makeCharacterJump()
        	break
            
	    default:
    	    // ignore unsupported keys
        	break
        }
    }

### Continuous Key Presses

A continuous keypress needs to be implemented by storing the state of a key, typically in a boolean property of the class. This bool would give you a permanent record whether a given key is currently pressed down. You set the bool to YES/true in the key down event, and you set it back to NO/false in the key up event.

In this example you may want to allow the player to jump higher the longer the jump key is pressed. Therefore you need to test over the course of several frames whether the jump key is still held down. You can do it like so, assuming that `jumpKeyPressed` is declared as a property (or ivar) of the class:

	// Objective-C
	-(void)keyDown:(NSEvent *)theEvent {
		switch (theEvent.keyCode) {
			case kVK_ANSI_J:
			case kVK_Space:
				jumpKeyPressed = YES;
				break;
		}
	}
	-(void)keyUp:(NSEvent *)theEvent {
		switch (theEvent.keyCode) {
			case kVK_ANSI_J:
			case kVK_Space:
				jumpKeyPressed = NO;
				break;
		}
	}

	// Swift
	override func keyDown(theEvent: NSEvent) {
	    switch Int(theEvent.keyCode) {
	    case kVK_ANSI_J, kVK_Space:
			jumpKeyPressed = true
        	break
        }
    }
	override func keyUp(theEvent: NSEvent) {
	    switch Int(theEvent.keyCode) {
	    case kVK_ANSI_J, kVK_Space:
			jumpKeyPressed = false
        	break
        }
    }

Note that it is good practice to avoid using the name of the character or key code in variable names. Typically a key will have a function, so it's best to use a variable name that reflects the function that it performs (here: "jump") rather than the key.

For one, key assignments may change which would require renaming the variable. Then there may be multiple keys assigned to the same function, as in the example above. Lastly, it improves code readability. Imagine having to remember what kind of function was assigned to the `keyPressed_S` variable at any time. Bugs where you perform the wrong action based on a variable stand out more when you realize that: if the `timeWarpKeyPressed` variable is true it actually runs the "save game" method. It wouldn't be that obvious if you used `keyPressed_S` as the variable name.
