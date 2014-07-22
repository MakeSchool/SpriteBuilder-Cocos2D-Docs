#Creating Joints in Code

Although SpriteBuilder is able to setup joints that persist for the entire life of a game and to create joints which break under certain forces, it is unable to create joints when an action occurs.  This can be extremely useful for causing two physics bodies to stick together in a dart or launching style application.  To create these connections in Cocos2D when an event occurs the CCPhysicsJoint class can be invoked

CCPhysicsJoint provides four class initializer methods to create different joints in code:

connectedPivotJointWithBodyA:bodyB:anchorA:
connectedDistanceJointWithBodyA:bodyB:anchorA:anchorB:
connectedDistanceJointWithBodyA:bodyB:anchorA:anchorB:minDistance:maxDistance:
connectedSpringJointWithBodyA:bodyB:anchorA:anchorB:restLength:stiffness:damping:

Joints start working the moment they are created. Joints can be deactivated by calling the invalidate method. Here's an example of how to set up a joint in code:

	// create a joint to connect the catapult arm with the catapult
	_catapultJoint = [CCPhysicsJoint connectedPivotJointWithBodyA:_catapultArm.physicsBody bodyB:_catapult.physicsBody anchorA:_catapultArm.anchorPointInPoints];