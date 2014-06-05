#Setup physics in code

Physics bodies and physics nodes can also be created in code.

##Setting up a Physics Node in code
A physics node can be created with the following line:

    CCPhysicsNode *physicsNode = [CCPhysicsNode node];
##Setting up Physics Bodies in code
To setup a physics body in code the class `CCPhysicsBody` is used. It provides multiple `bodyWith...` class methods to initialize physics bodies:

- `bodyWithCircleOfRadius:(CGFloat)radius andCenter:(CGPoint)center`
- `bodyWithRect:(CGRect)rect cornerRadius:(CGFloat)cornerRadius`
- `bodyWithPillFrom:(CGPoint)from to:(CGPoint)to cornerRadius:(CGFloat)cornerRadius`
- `bodyWithPolygonFromPoints:(CGPoint *)points count:(NSUInteger)count cornerRadius:(CGFloat)cornerRadius` 
- `bodyWithPolylineFromRect:(CGRect)rect cornerRadius:(CGFloat)cornerRadius` 
- `bodyWithPolylineFromPoints:(CGPoint *)points count:(NSUInteger)count cornerRadius:(CGFloat)cornerRadius looped:(bool)looped` 
- `bodyWithShapes:(NSArray *)shapes`

The physics body is a property of `CCNode`. This is in example how to turn any `CCNode` subclass into a physics object:

    bear.physicsBody = [CCPhysicsBody bodyWithCircleOfRadius:10 andCenter:ccp(20, 20)];



