# Hit Detection

An often-asked question is "how to detect if a node was touched?". This is called *hit detection* or *hit testing*, the process of determining whether an input event occured on a particular node.

While this is frequently needed in user interaction, hit detection is not limited to just that. It does not matter whether you are testing a touch location to be inside a given node, or a bullet node.

## Simple Hit Test

Every node has the `hitTestWithWorldPos` method which tests if a given point (in world coordinates) is within the node's bounding box. In addition to the bounding box this check also takes the `hitAreaExpansion` [property of CCResponder](http://www.cocos2d-swift.org/docs/api/Classes/CCResponder.html#//api/name/hitAreaExpansion) into account.

	// Objective-C
	CGPoint otherNodePos = [otherNode convertToWorldSpace:otherNode.position];
    if ([node hitTestWithWorldPos:otherNodePos]) {
        // otherNode's position is within the node's bounding box + hitAreaExpansion
    }

	// Swift
	let otherNodePos = otherNode.convertToWorldSpace(otherNode.position)
    if node.hitTestWithWorldPos(otherNodePos) {
        // otherNode's position is within the node's bounding box + hitAreaExpansion
    }

## The node's boundingBox

Every node has a `boundingBox` property that returns a CGRect whose origin is the lower left corner of the node in the node's parent coordinates, with the size equal to `contentSizeInPoints`.

So if you wanted a node's boundingBox in world (scene) coordinates, you would also have to convert the rect's origin to world coordinates.

	// Objective-C
	CGRect bbox = [node boundingBox];
    bbox.origin = [node convertToWorldSpace:bbox.origin];

	// Swift
    var bbox = node.boundingBox()
    bbox.origin = node.convertToWorldSpace(bbox.origin)

This gives you the node's axis-aligned bounding box in world coordinates. 

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
*Axis-aligned* means the bounding box does not take the node's (or its parent's) rotation into account.
</td></tr></table>

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
Converting all coordinates to world space is good practice if you find working with and converting between coordinate systems confusing. You can easily convert any coordinate to the world coordinate system, that way you don't need to worry about whose coordinate system you are currently working with. This only comes at a slight extra cost of having to convert both node's coordinates rather than converting one node's coordinates into the coordinate system of another node.
</td></tr></table>

## Rect contains point or intersects rect

The [CGGeometry Reference](https://developer.apple.com/library/mac/documentation/GraphicsImaging/Reference/CGGeometry/index.html) list a number of useful functions to test whether a point is inside a rectangle, or rectangles intersect, and so on.

The most useful functions for hit testing are:

- [CGRectIntersectsRect](https://developer.apple.com/library/mac/documentation/GraphicsImaging/Reference/CGGeometry/index.html#//apple_ref/c/func/CGRectIntersectsRect) - Tests whether one CGRect overlaps (intersects) another CGRect
- [CGRectContainsPoint](https://developer.apple.com/library/mac/documentation/GraphicsImaging/Reference/CGGeometry/index.html#//apple_ref/c/func/CGRectContainsPoint) - Tests whether a CGPoint is inside a CGRect

So if you wanted to test if a point lies within the bounding box of a node, and assuming the point is the position of another node, you would do:

	// Objective-C
    CGRect bbox = [node boundingBox];
    bbox.origin = [node convertToWorldSpace:bbox.origin];
    CGPoint worldPoint = [otherNode convertToWorldSpace:otherNode.position];
    if (CGRectContainsPoint(bbox, worldPoint)) {
        // point lies inside node's bounding box
    }

	// Swift
    var bbox = node.boundingBox()
    bbox.origin = node.convertToWorldSpace(bbox.origin)
    let worldPoint = otherNode.convertToWorldSpace(otherNode.position)
    if CGRectContainsPoint(bbox, worldPoint) {
        // point lies inside node's bounding box
    }

The above examples need to be adapted to your actual nodes, the `node` and `otherNode` variables are placeholders.

The above example testing both node's bounding boxes works as follows:

	// Objective-C
    CGRect bbox = [node boundingBox];
    bbox.origin = [node convertToWorldSpace:bbox.origin];
    CGRect otherbbox = [otherNode boundingBox];
    otherbbox.origin = [otherNode convertToWorldSpace:otherbbox.origin];
    if (CGRectIntersectsRect(bbox, otherbbox)) {
        // bbox intersects with (overlaps) otherbbox
    }

	// Swift
    var bbox = node.boundingBox()
    bbox.origin = node.convertToWorldSpace(bbox.origin)
    var otherbbox = otherNode.boundingBox()
    otherbbox.origin = otherNode.convertToWorldSpace(otherbbox.origin)
    if CGRectIntersectsRect(bbox, otherbbox) {
        // point lies inside node's bounding box
    }

If you need this frequently it is strongly recommended to wrap this code in a method, preferably placing it in a CCNode(hittest) [Objective-C category](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/CustomizingExistingClasses/CustomizingExistingClasses.html) for easy access.


## Point in Radius/Circle (distance check)

You may be wondering about other tests, for instance how to determine if a point is within a circle defined by radius. That is actually a simple distance test that you can perform using the built-in `ccpDistance` and `ccpDistanceSq` (distance squared) methods.

	// Objective-C
    float distanceSquared = ccpDistanceSQ(centerOfCircle, point);
    if (distanceSquared < (radius * radius)) {
        // point is within radius (circle)
    }

	// Swift
    var distanceSquare = ccpDistanceSQ(centerOfCircle, point)
    if distance < (radius * radius) {
        // point is within radius (circle)
    }

In this example the `ccpDistanceSQ` method was used, which returns the squared distance. This is preferred whenever possible because you can easily compare the squared distance with the squared radius (hence: `(radius * radius)`). Why? Because it avoids having to take the square root that `ccpDistance` uses internally. Taking the square root of a number is a relatively expensive operation. Though it won't be noticable in terms of framerate unless you were to run `ccpDistance` many times per frame.

## Other Hit/Distance Tests

There are many other hit and distance tests you can perform but they are beyond the scope of this guide. Following is a list of tests you may want to perform with links to *one* possible solution - but be aware that some solutions are far from trivial and solutions may not easy to come by in a specific programming language such as ObjC or Swift.

- [Circle intersects circle](http://stackoverflow.com/questions/1736734/circle-circle-collision) - this is simply a variation of the distance check above, where if the distance between the circle's center points is less than the sum of the radii the circles intersect.
- [Rect intersects with / contains circle](http://stackoverflow.com/questions/401847/circle-rectangle-collision-detection-intersection)
- [Polygon contains point](http://stackoverflow.com/questions/217578/point-in-polygon-aka-hit-test)
- [Point on non-transparent pixel of a sprite/image (pixel-perfect collision detection)](http://www.learn-cocos2d.com/2011/12/fast-pixelperfect-collision-detection-cocos2d-code-1of2/)
- [Distance of point from line segment](http://stackoverflow.com/questions/849211/shortest-distance-between-a-point-and-a-line-segment)
- [Distance of point to rectangle](http://gamedev.stackexchange.com/questions/44483/how-do-i-calculate-distance-from-a-point-to-a-rectangle)
