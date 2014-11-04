#Collision Detection

Cocos2D provides a sophisticated collision detection API. 

##Physics Body Collision properties
`CCPhysicsBody` has many properties that help defining the behaviour of physics bodies when they collide:

- `sensor` - If set to true no physical collision with this object will occur. A collision with this object will only call a collision handler delegate.
- `collisionGroup`- If two phyiscs bodies share the same collision group they will not collide 
- `collisionType` - Is used to generate collision callbacks.
- `collisionCategories`- An array of NSString category names of which this physics body is a member. A value of nil means that a body exists in all possible collision categories.
- `collisionMask` - An array of NSString category names that this physics body wants to collide with. The categories/masks of both bodies must agree for a collision to occur. A value of nil means that this body will collide with a body in any category.

##Listening for collisions
In order to listen to collisions a class needs to subscribe as the delegate of a `CCPhysicsNode`. A class will get informed about all collisions that happen between objects that are children of that `CCPhysicsNode`. The listening class needs to conform to the [`CCPhysicsCollisionDelegate`](http://www.cocos2d-iphone.org/api-ref/3.0-rc1/Protocols/CCPhysicsCollisionDelegate.html) protocol. 

##Implementing collision callbacks
Once a class has set itself as as the delegate of a `CCPhysicsNode` it needs to implement collision callback methods. Cocos2D uses a special mechanism where the callback methods use the `collisionType` of a `CCPhysicsBody` to determine the actual name of the callback method.

For example these collision types:

	bear.physicsBody.collisionType = @"Bear";
    ground.physicsBody.collisionType = @"Ground";
    
Would result in a collision callback like this:

	- (BOOL)ccPhysicsCollisionBegin:(CCPhysicsCollisionPair *)pair bear:(CCNode *)bear ground:(CCNode *)ground {
	    // collision handling
	}
	
##Collision Sequence
`CCPhysicsCollisionDelegate` provides multiple callbacks that are called at different steps of the collision sequence:
 
- `ccPhysicsCollisionBegin:typeA:typeB:` - Will be called on the first fixed time step (not necessarily frame) that two physics shapes collide for the first time 
- `ccPhysicsCollisionPreSolve:typeA:typeB:` - The pre-solve method gives you a chance to modify the outcome of the collision
- `ccPhysicsCollisionPostSolve:typeA:typeB:` - The post-solve method lets you find out what the outcome of a collision was 
- `ccPhysicsCollisionSeparate:typeA:typeB:` -  is called when two physics objects stop touching for the very first fixed time step

The begin and and the pre-solve collision methods require a boolean return type. Returning `NO` from either of the two will ignore the collision for that physics calculation step.

##See Also

- [Clone Angry Birds: add Collision detection](https://www.makegameswith.us/tutorials/getting-started-with-spritebuilder/collision-detection/)