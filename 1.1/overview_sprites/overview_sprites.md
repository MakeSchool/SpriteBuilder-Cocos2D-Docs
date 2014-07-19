#What are Sprites

A sprite is simply another name for an image that is used in a 2D game.  In a Cocos2D game many of the assets that you manage will likely be sprites.  Sprites are represented within the game as a subclass of CCNode known as CCSprite.  The CC prefix identifies the class as a member of the Cocos2D API.  To get a sprite image into a game all you have to do is create an instance of CCSprite which specifies the name of the target image, and the sprite will be rendered to the screen.

#Working with Sprite Sheets

Rather than loading images in one at a time, developers frequently opt to put all of their image assets onto a single page so that they can be loaded in all at once, and then when rendering an image to the screen only the appropriate portion of the larger screen is shown.  This single sheet of sprites is known as a SpriteSheet.

Traditionally the process of creating a SpriteSheet requires a developer to use a program such as Photoshop to piece the sprites together by hand, and then specify a grid or pixel map for where each sprite is located in the document.  SpriteBuilder makes this process simple by automatically generating Sprite sheets from a folder of images.  SpriteBuilder also handles automatic image re-sizing for creating games with multiple screen sizes, so that your images look just as crisp on retina and non-retina devices.