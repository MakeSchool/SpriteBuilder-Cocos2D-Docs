#Creating Physics Shapes

When physics is enabled on an image the Chipmunk2D physics engine needs a way to determine when that image is colliding with the objects around it.  By default .  In SpriteBuilder the boundaries for an object can be set as a polygon by visually adding vertices to the shape and dragging them to the appropriate locations.  To do the equivelent in Cocos2D the CcPhysicsShape class is used.

Normally a shape is initialized with the physics body, however this may not be sufficient when creating the boundary for a composite shape.  The CCPhysics shape class has methods which allow the user to define cricles, rectangles or polygons as the bounding collision shape.  Additionally, methods fordetecting the collision state of the body are made available if events need to be triggered in the run loop based on collisions.

It should be noted that in most cases it is wiser to go with simpler, representative shapes than to closely map every edge of an image.  Complex shapes require more processing power for analyzing collisions and can cause any code written to modify the reaction substantially more complicated.