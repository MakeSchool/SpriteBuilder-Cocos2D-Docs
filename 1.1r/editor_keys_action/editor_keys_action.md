#Manipulating Nodes
Actions are the primary method in Cocos2D for manipulating nodes, which are the building blocks of all visual elements in Cocos2D.  As a result, CCActions are extraordinarily powerful and can be used to create animations as well as programatically alter the screen's contents.  The same way that CCResponder exposed a small number of essential properties and methods to its children, CCAction has very little built in functionality, and most of the power is delegated to its four direct children.

#The Four Children of CCAction
CCAction has four direct children; two of the children control the movement and animation of nodes, and the other two provide special functionality that can be applied to actions.


-CCActionRepeateForever - This class creates an action which is repeated forever.

-CCActionFiniteTime:  Since CCActionRepeateForever only handles infinite events, CCActionFiniteTime is responsible for handeling all actions that have a definite end point.  This task is logically broken into two more sub classes: CCActionInstant and CCActionInterval
	-CCActionInstant: This class handles all actions that happen in a single frame update, thereby occuring instantly to the user.  Examples of instant actions are fliping a sprtie, showing/removing a sprite, or calling a function.
	-CCACtionInterval:  This class handles any actions that happen over a period of time.  This includes movements, rotations, and visibility transformations.  See the section on animation in code for an exploration of CCActionInterval's children.


CCActionFollow - This class is used to create an action that causes the camera to follow a node.  For an example of its use see the peeved penguins tutorial

CCActionSpeed -  Thi class allows an action to be run at different speeds without changing the time intervals set within the action.  It is ideal for creating the apperance of time slowing down or speeding up.  However, because it is not descended from CCActionInterval it cannot be put into the middle of a sequence, it must be triggered directly.