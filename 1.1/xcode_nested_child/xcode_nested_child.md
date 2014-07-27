#Working with children of nodes
Nodes can be added as children of other nodes. This way a node hierarchy is created. 

###Adding Children

You can add a node using the `addChild:` method. All children of a `CCNode` are moved together with their parents. The position of a `CCNode` is always relative to its parent. The only exception is `CCNode` instances that have a `physicsBody` - this is covered in the physics chapter.


###Removing children

To remove a `CCNode` from another `CCNode` a developer will mostly use the `removeFromParent` method on the node that shall be removed. 

###Drawing Order of Children

By default children have a higher drawing order than their parents and are added on top of them. A developer can modify the drawing order by providing a separate *z* value. In this case the `addChild:z:` method should be used. The *z* order can also be changed by setting the `zOrder` property of the `CCNode`. 

The *z* value overrides the drawing order that is usually defined by the order the nodes have been added (the node added the latest is drawn on the top).

The drawing order is defined like this:

1. Draw all children with a *z* value below 0. The lowest value is drawn first.
2. Draw self
3. Draw all children with a *z* value of >= 0. Nodes with the same *z* value will be drawn in the reverse order of insertion.

If you, for example, wanto to draw a child node *under* its parent node, you can use a negative *z* value:

	[parentNode addChild:childNode z:-1];

##Working with multiple coordinate systems
By default positions of nodes are always expressed relative to their parent. Sometimes a developer will need to transform these positions into different coordinate systems. 

*An example:* A developer wants to check if the arm of a character has left the screen. The position of the arm is relative to the character's body. The developer needs a mechanism to retrieve the coordinates of the arm in the screen coordinate system.

Transferring coordinates into another coordinate system is a two step process in Cocos2D:

1. Retrieve the world coordinates using:   


		CGPoint worldPosition = [parentNode convertToWorldSpace:childNode.position];  
       
2. Use the world position and transform it to the node space of the target node:  
       
       
		GPoint scenePosition = [scene convertToNodeSpace:worldPosition];
       
A developer can use this mechanism to express a position in any node space.