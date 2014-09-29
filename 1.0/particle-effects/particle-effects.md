#Particle Effects

SpriteBuilder provides an integrated particle effect editor. It provides many template particle effects and easily allows to customize them. Cocos2D also supports particle effects created by the third party tool *Particle Designer*, as of now this is not covered in this tutorial.

##Creating Particle Effects in SpriteBuilder
Particle effects are represented by CCB files. When creating a new CCB file *Particles* can be selected as a template:

![image](Particle_CCB.png)

Once a particle effect is created and selected the right inspector pane provides all the different options to change particle effect behaviour:

![image](Particle_Editor.png)

The last tab in the right pane reveals the Particle Effect library that provides predefined templates. A template can be selected by double clicking on it. A current particle effect can be stored as a template by providing a name and selecting the *Create* button:

![image](Particle_Library.png)

##Textures for Particle Effects
When creating particle effects from scratch instead of using a template a developer needs to provide a custom texture. The texture provided should represent one single particle in front of a transparent background, the texture is replicated by the particle system as needed. Example for a particle effect texture:

![image](particle_stars.png)

##Adding Particle Effects to a scene
Particle effects can be added to a scene in SpriteBuilder or can be loaded in code and added to a scene dynamically at runtime.

###Adding Particle Effects in SpriteBuilder
Since particle effects are regular CCB files they can be added as Sub CCB files to any scene in SpriteBuilder.

###Adding Particle Effects at runtime in Code
Particle effects can be loaded just as any other CCB file, using the `CCBReader`. A brief example:

	// load particle effect and cast CCNode to CCParticleSystem
	CCParticleSystem *fire = (CCParticleSystem *)[CCBReader load:@"Fire"];
	// make the particle effect clean itself up, once it is completed
	fire.autoRemoveOnFinish = YES;
	// place the particle effect on the seals position
	fire.position = ccp(100,100);
	// add the particle effect to the scene
	[self addChild:fire];

##See Also

- [Clone Angry Birds with SpriteBuilder: Add particle effects](https://www.makegameswith.us/tutorials/getting-started-with-spritebuilder/particle-effect/)
