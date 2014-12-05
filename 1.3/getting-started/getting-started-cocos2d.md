# First Steps with Cocos2D

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
Skip this guide if you intend to use SpriteBuilder. You should only read this guide if you <strong>expressly decided not to use SpriteBuilder at all</strong>. In that case, consider that you will have to write program code for everything and manage your resource files (assets) manually.
</td></tr></table>

## Downloading Cocos2D

Since SpriteBuilder includes Cocos2D, there's no need to nor any benefit from downloading Cocos2D separately.

Still, you can get the latest Cocos2D version from the [Cocos2D Downloads page](http://www.cocos2d-swift.org/download). You may also want to [pull Cocos2D from GitHub](#!/docs/1.3/develop/cocos2d-build-from-sources).

## Creating a Cocos2D-Only Project

Every new Cocos2D project must be created via SpriteBuilder, see [this thread](http://forum.cocos2d-swift.org/t/installing-cocos2d-swift/15916). 

Once a SpriteBuilder project was created you can remove any connection to SpriteBuilder (not recommended). Here's what you need to do.

### Create a new SpriteBuilder Project

1. Open SpriteBuilder and run **File => New => Project**.
2. With the new project created, run **File => Publish** once.
3. Open the SpriteBuilder project's Xcode project by running **File => Open Project in Xcode** from within SpriteBuilder.
4. You can close SpriteBuilder now.
5. In Xcode, create a new Objective-C class and make it a subclass of CCScene. In this example I'll name it "MyFirstScene".
5. In Xcode, open `AppDelegate.m` and locate the `-(CCScene*) startScene` method. Change the method to return an instance of a CCScene subclass and `#import` the corresponding scene's header. For example:
```
	#import "MyFirstScene.h"
	
	...
	
	- (CCScene*) startScene
	{
	    return [MyFirstScene node];
	}
```

6. You can delete the following:
	- The `Published-iOS` and `Published-Android` groups. They contain resource files published by SpriteBuilder.
	- The default scene created by SpriteBuilder: `MainScene.*` files.

### Upgrading Projects

Since SpriteBuilder allows you to upgrade a Cocos2D project to the latest version of Cocos2D, it is highly recommended to leave all other files in the `.spritebuilder` folder untouched. 

Doing so enables you to upgrade the Cocos2D version in your project by simply opening the `.spritebuilder` project in the updated version of SpriteBuilder, then confirm the upgrade message.

Moving or renaming the Xcode project, or deleting other SpriteBuilder files in that project may render your project unusable by SpriteBuilder. In that case you would have to manually manage updating Cocos2D in your project. 

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
You may think you'll never need to upgrade Cocos2D, but that day <strong>will</strong> come! Apple releases new projects on a yearly basis. Apple requires developers to (properly) support the new devices in new apps and app updates. However new devices may require an updated version of Cocos2D. Many Cocos2D projects are in development and subsequently being updated for more than a year. So it's wise to keep your project upgradable with ease via SpriteBuilder.
</td></tr></table>

