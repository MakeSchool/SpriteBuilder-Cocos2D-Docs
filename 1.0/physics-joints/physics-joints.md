#Joints

Joints are used to connect physics bodies with each other. As of SpriteBuilder 1.0.3 joints can only be created in code. Joints are represented by the class `CCPhysicsJoint`. 

##Initializing Joints
Cocos2D supports four joint types. They are initialized using class initializer methods:

- `connectedPivotJointWithBodyA:bodyB:anchorA:`
- `connectedDistanceJointWithBodyA:bodyB:anchorA:anchorB:`
- `connectedDistanceJointWithBodyA:bodyB:anchorA:anchorB:minDistance:maxDistance:`
- `connectedSpringJointWithBodyA:bodyB:anchorA:anchorB:restLength:stiffness:damping:`

Joints start working the moment they are created. Joints can be deactivated by calling the `invalidate` method. 
Example of setting up a joint:

	// create a joint to connect the catapult arm with the catapult
	_catapultJoint = [CCPhysicsJoint connectedPivotJointWithBodyA:_catapultArm.physicsBody bodyB:_catapult.physicsBody anchorA:_catapultArm.anchorPointInPoints];