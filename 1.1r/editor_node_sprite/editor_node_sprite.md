#Working with Sprites
A sprite is just another name for a 2D image.  In 2D games, almost every visual component will be a sprite.  Sprites can either be added to the scene directly by dragging and dropping them from the assets folder onto the stage area, or they can be created from the node library, and have the image source assigned in the properties panel.


#Working with Sprite 9-slices
A sprite 9-slice functions identically to a sprite in all regards except for the way it scales.  In the properties panel it is possible to set top, bottom, left and right margains as a percentage of the image.  These margins divide the sprite into nine slices.  During a scaling operation the portion of the sprite outside of these margins will not scale, only the middle of the 9 squares will be effected.  Functionally, a Sprite 9-slice, when properly used, will render more efficiently than a standard sprite.