#What is z-ordering

The z-order for an image drawn in Cocos2D is what determines its draw order when rendering to the screen.  Images with a higher z-order will be drawn later than objects with a low z-order.  The result is that if two images occupy the same space on screen, the object with the higher z-order will be drawn on top of the one with the lower z-order, giving it the apperance of being in front of that object.  As a result, even though Cocos2D is a 2D game engine, the z-order serves as a sudo 2rd dimension.

Normally the z-order of an object in a SpriteBuilder project is determined by its positioning on the timeline heirarchy.  That's why if a background is placed at the top of the timeline heirarchy it will draw over all of the other itmes and they won't be visible onscreen.

In order to set the z-order of an object manually, simply access the z order in code and set it to the desired value.  Since every visual element is a descendent of CCNode, anywhere that the visual asset is in scope you can alter its z-order by using instance.zOrder.