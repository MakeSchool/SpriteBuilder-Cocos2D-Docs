#Load ccb files in code

The CCBReader class provides multiple methods to load ccb files in code. The most important ones are:

+ (CCNode*) load:(NSString*) file
+ (CCNode*) load:(NSString*) file owner:(id)owner
+ (CCScene*) loadAsScene:(NSString*) file
+ (CCScene*) loadAsScene:(NSString *)file owner:(id)owner;
The file name is the name of the ccb file. The file ending .ccbi is optional. For more information on the owner parameter read the code connections section.

##Scene transitions with SpriteBuilder

SpriteBuilder allows to create multiple scenes, however, the tranisitions between these scenes need to be defined in code. A typical scene transition using SpriteBuilder will look similar to this:

	- (void)gameOver {
    	CCScene *recapScene = [CCBReader loadAsScene:@"RecapScene"];
    	[[CCDirector sharedDirector] replaceScene:recapScene];
	}
##Casting the loaded node

If the CCBReader is used to load a node of a specific type and a developer needs to access specific properties of that node a cast can be required.

A common example is loading a CCParticleSystem:

	CCParticleSystem* myParticles = (CCParticleSystem*) [CCBReader load:@"MyParticleSystem"];

In order to treat the loaded node as an instance of CCParticleSystem a cast is required