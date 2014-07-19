#Animation in Code

Creating animations in Cocos2D is accomplished by stringing together a series of CCActions, which modify the the properties of CCNode, such that a character or object appears to be moving.  To do this the subclasses of CCActionFiniteTime, which provide methods for modifying a node over a time period, are placed in sequence or parallel.  The end result is the apperance of an object moving.

While SpriteBuilder is great for producing animations on a single sprite or CCB file, by creating animations using CCActions you can apply the same modification sequences to any nodes you want whenever you want as many times as you want.

While it is possible to create frame by frame animations where each frame the sprite is replaced by a new animation in a slightly different position, this will not be the focus of this section.  Instead, this section focuses on using CCActions in order to manipulate the existing sprite.