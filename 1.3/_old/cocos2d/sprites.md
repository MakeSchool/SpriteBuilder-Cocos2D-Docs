#Working with Sprites

Sprites are a very important part of Cocos2D, they are used to render textures to the screen. 
This documentation will cover following aspects:

- Creating textured sprites
- Changing a sprite texture
- Sprite Frame Animations
- Using 9 Patch Sprite Images

##Creating a textured Sprite

The easiest way to setup a textured Sprite is the following line of code:

	CCSprite *hero = [CCSprite spriteWithImageNamed:@"hero.png"];
	
`spriteWithImageNamed:` utilizes `CCFileUtils` to automatically find the image in the right resolution, you do not have to specify the resolution manually. The line above also works for images contained in *Smart Sprite Sheets* created by SpriteBuilder. In case you are using folders in SpriteBuilder you need to include the complete path to the image, e.g.:
	
	CCSprite *hero = [CCSprite spriteWithImageNamed:@"gameAssets/hero.png"];
	
The content size of the sprite will automatically be the size of the texture.

##Changing the texture of an existing Sprite

To change the texture of an initialized Sprite the *spriteFrame* property can be used:

	hero.spriteFrame = [CCSpriteFrame frameWithImageNamed:@"hero_dead.png"];
	
##Sprite frame animations
Sprite frame animations are used in basically every 2D game. A sequence of different 2D images gets replaced at a defined interval forming an animation:

![image](sprite-frame-animation-diagram.png)

SpriteBuilder provides an easy way to create Sprite frame animations which will be discussed in the next chapter.