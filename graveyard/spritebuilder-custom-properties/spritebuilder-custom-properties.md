# Custom Properties in SpriteBuilder

Custom properties can be used to set properties of Cocos2D game objects without using code. This feature is especially useful when using SpriteBuilder as a level editor. This way different properties of the level can be changed without using code.

One possible example is the scrolling speed of a side scroller. If a developer creates a side scroller where the scrolling speed can change for each level this is a great use case for custom properties. Instead of creating specific instances for the different Levels the developer can use the same `Level` class for all levels and only manipulate the custom property.

In SpriteBuilder custom properties can be added by selecting a node and choosing *Object > Custom Properties...* from the top menu:

![image](customproperties.png)

**The custom class of the selected node needs to contain all properties that are added to the custom properties.**

Custom properties should be used as often as possible to define a slightly different behaviour without creating different subclasses, e.g.:

- Changing behaviour of enemies in a level
- Storing tutorial instructions
- Defining the amount of lifes for a level

##Custom properties in sub ccb files

It can be very useful to be able to change custom properties of sub ccb files on a per instance basis. SpriteBuilder makes this possible, however, all properties that shall be overriden need to be defined in the actual ccb file, not in the imported sub ccb file.