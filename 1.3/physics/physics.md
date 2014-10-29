#Physics

Cocos2D comes with an integrated physics engine that makes it very easy to create physics based games. SpriteBuilder allows setting up physics properties conveniently.  

##Features of the physics engine

- Physics body simulation
- Joint simulation
- Collision detection
- etc ...

##Hierarchy of a physics scene

Each `CCNode` can store a `CCPhysicsBody` within the `physicsBody` property. All physics bodies have to be children of a `CCPhysicsNode`.  A `CCPhysicsNode` provides a physics world where the gravity can be manipulated and collisions can be captured. 

![image](../_images/conceptual/physics-object-hierarchy-diagram.png)

> Note: The default parent-child transform in a node hieararchy does not apply for physics bodies. This means physics bodies do not move together with their parents. The only way to connect physics bodies with each other is using joints.

##Basic physics body properties 

Following poperties are used most often to define the behaviour of a physics body:

- physics body shape (can only be set during initialization)
- mass
- friction 
- density
- elasticity
- type (static vs. dynamic)
- collisionType, collisionCategory, collisionMask (discussed in *Collision Handling* chapter)
- affectedByGravity
- allowsRotation

##Static and dynamic physics bodies

Cocos2D supports two types of physics bodies: static bodies and dynamic bodies. The type of a physics body is determined by the `type` property on `CCPhysicsBody`. Static physics bodies are never affected by gravity or collisions, they remain in their initial position infinitely. Because their position does not need to be recalculated static physics bodies use less computation power than dynamic ones. A typical example for a static physics body is a ground in a game. 

Dynamic physics bodies change their position and velocity when they collide with other physics bodies and they can be affected by gravity.


