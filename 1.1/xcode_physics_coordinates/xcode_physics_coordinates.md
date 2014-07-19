#Axis Conventions

When working with physics in games there is traditionally a large amount of math involved.  Cocos2D and the chipmunk engine handle most of the mathematical grunt work, however a basic understanding of the systems that the engines use when making calculations is important for uensuring that inputs to the API have the desired results.

The building block of any physics interaction is the vector.  A vector is a unit which has both magnitude and direction.  This is important because when a force is applied to an object the engine needs to know not only how much force to apply, but also what direction to apply it in.  Within Cocos2D a standard cartesian coordinate system is used for positioning, and by extension since the vector says the direction to go from a location, the vectors that Cocos2D uses follow standard axis conventions as well

#Rotational and Cartesian Conventions

The cartesian coordinate system is split into four quadrants by the x axis and y axis.  The quadrants are numbered 1-4 starting with the positive x, positive y quadrant and moving counter-clockwise.  Additionally, the positive x axis is where this progression begins, so it is considered 0 degrees in most cases.  As a result, counter clockwise rotation is considered positive rotation (following the quadrants), and clockwise motion is considered negative.  This convention is used when applying torques and specifying angles away from the x-axis.  All Cocos2D angles are represented by degrees, not pi-radians.

When creating a vector the x and y parameters are in terms of the standard axis conventions, so positive x is facing to the right and positive y is facing up.  As a result, a positive x positive y vector would point from the origin into the first quadrant, and negative x negative y vector would point into quadrant 3.
