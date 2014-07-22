Dragging a Physics Node onto the stage creats an instance of CCPhysicsNode (insert link to api), the Cocos2D class which handles collisions and gravity. In order to simulate physics between bodies, they must be the children of a CCPhysicsNode so that they are living in a "physical world" with the other bodies. Since each CCPhysicsNode defines its own world, in order to connect bodies using joints, or have bodies collide, they must be the children of the same CCPhysicsNode.


SpriteBuilder makes assigning bodies to be the children of a CCPhysicsNode extremely easy due to its drag-and-drop nesting on the timeline.
NextPrevious