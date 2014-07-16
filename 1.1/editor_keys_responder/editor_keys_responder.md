#Handeling Touch Events
Cocos2D handles user inputs through a class called CCResponder.  CCNode inherits from CCResponder, allowing all visual elements access to the user interaction information.  Although CCResponder takes care of the work of recognizing user interactions for you, it's important to know what matheds it makes available.  For both touch and mouse events you can write code to be run when a touch/click begins and ends, as well as when the finger/mouse is moved while pressing down.


#The CCNode Class
All of the visual components in a Cocos2D class are children of the CCNode class.  As a result, CCNode is the class which defines all of the foundational methods and properties not handled by CCResponder which are essential to creating a game.  Some of the most important tasks that CCNode controls are:

-Position and Size: CCNode controls the position, scale, content size, rotation, skew, and anchor points for visual elements

-Scene Heirarchy:  CCNode can access information about a node's parent, can add and remove children, and define the zOrder of the node, which determines its draw order.

-Actions:  Control the animations and actions run on the node.

-Callbacks: Allow the user to schedule functions which will be called repeatedly or after a delay as a callback function.

-Transformations and Rendering:  Advanced features which allow lower level manipulation of a Node's apperance




#Learning More
The CCNode class is the foundation of all visual aspects of a Cocos2D game, and as a result learning about it will help increase your understanding of how a Cocos2D game functions.  The full reference for CCNode can be found [here.](www.cocos2d-swift.org/docs/api/classes/CCnode.html)