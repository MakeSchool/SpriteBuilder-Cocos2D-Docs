#Physics Components

Cocos2D uses the Chipmunk physics engine to simulate the interactions of physical bodies.  As a result, .  SpriteBuilder provides the ability to construct complex physics simulations by manipulating the properties of the various bodies involved in the interaction, and an even finer level of control is possible using Xcode and Cocos2D to interact with the physics loop.  The major components of the Cocos2D physics API are:

-Physics Bodies : Nodes can be designated as physics bodies, and they will then have properties such as mass, friction and shape.  Chipmunk uses these properties to determine how the body will interact with the world around it.

-PhysicsCollisions : When two physics bodies occupy the same screen space, Cocos2D detects it and simulates the collision between the two on a frame by frame basis.  This collision loop can be tapped into programatically to give nuanced control over how bodies interact.

-PhysicsJoints : Joints are used to link two physics bodies together.  They can be used to lock two bodies at a certain distance from each other, to cause one body to pivot around another, or to create an elastic connection.

Sections that detail how to perform these operations are provided [here](link) and [here](link).