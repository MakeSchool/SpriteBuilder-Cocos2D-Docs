#Nodes in Cocos2D


##Handeling Touch Events: CCResponder

Cocos2D handles user inputs through a class called CCResponder.  CCNode inherits from CCResponder, allowing all visual elements access to the user interaction information.  Although CCResponder takes care of the work of recognizing user interactions for you, it's important to know what matheds it makes available.  For both touch and mouse events you can write code to be run when a touch/click begins and ends, as well as when the finger/mouse is moved while pressing down.

##Subclasses of CCNode

In Cocos2D *every visible object* in a scene is a subclass of
[CCNode](http://www.cocos2d-iphone.org/api-ref/3.0-rc1/Classes/CCNode.html). Even `CCScene` is a `CCNode` subclass.

The most important `CCNode` subclasses are:

* **CCSprite**: Represents an image or an animated image. Used for characters,
  enemies, etc. in your gameplay.
* **CCNodeColor**: A plain colored node.
* **CCLabelTTF**: A node that can represent text in any TTF font.
* **CCButton**: A interactive node that responds to touch input.
* **CCLayoutBox**: A node that arranges it's child nodes vertically or horizontally. Replaces `CCMenu` which was part of Cocos2D 2.x.

##What CCNodes Interact with

-Scene Heirarchy:  CCNode can access information about a node's parent, can add and remove children, and define the zOrder of the node, which determines its draw order.

-Actions:  Control the animations and actions run on the node.

-Callbacks: Allow the user to schedule functions which will be called repeatedly or after a delay as a callback function.

-Transformations and Rendering:  Advanced features which allow lower level manipulation of a Node's apperance


##Important CCNode properties
`CCNode` has a couple of important properties that will be used in most games:

* **contentSize**: the size of the node in the unit specified by contentSizeType property
* **position**:  position (x,y) of the node in the unit specified by the positionType property.
* **anchor point**: the anchor point is the center point for rotations and the reference point for positioning this node.
* **visible**: defines if `CCNode` is visible or not

The position of a node is always expressed relative to its parent node, by default relative to the bottom-left corner of the parent. Cocos2D supports multiple sizing types and position types that can be used to create dynamic layouts. For more details read this [tutorial on dynamic layouts with Spritebuilder and Cocos2d](https://www.makegameswith.us/gamernews/361/dynamic-layouts-with-spritebuilder-and-cocos2d-30).

The following diagram visualizes a couple of these properties.

![image](Node_Positioning.png)

- The two reference points that define a position of a node within another node are the *position reference corner* of the parent and the *anchor point* of the node. 
- By default the reference corner is the bottom-left corner. In the diagram above the reference corner is at the top-left.
- The anchor point is (0.5, 0.5) by default. The anchor point can have values between 0 and 1 for the x and y component. 0 means the left/bottom edge, 1 means the right/top position
- The *contentSize* is the size of the *boundingBox* of the `CCNode`.

###Anchor point
As mentioned above, the anchor point is not only used as reference point for positioning nodes, it is also the center of rotation (when using the rotation properties of `CCNode`). 

![image](AnchorPoint.png)
