# Glossary

## A-Z

- **Action** - Refers to all classes that inherit from [CCAction](http://www.cocos2d-swift.org/docs/api/Classes/CCAction.html). Actions animate properties of a node over time. Actions can be in a sequence and repeated. Actions can be used to time events using [CCActionDelay](http://www.cocos2d-swift.org/docs/api/Classes/CCActionDelay.html) and [CCActionCallBlock](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallBlock.html) or [CCActionCallFunc](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallFunc.html) in a [CCActionSequence](http://www.cocos2d-swift.org/docs/api/Classes/CCActionSequence.html).
- **Director** - The core class in Cocos2D. Acts as view controller, manages the render loop, presents scenes.
- **Layer** - A concept of grouping nodes together so that an entire branch of the node hierarchy can be animated separately from other layers. Most nodes can be used as the parent node for a layer but typically [CCNode](http://www.cocos2d-swift.org/docs/api/Classes/CCNode.html) is chosen for this task. Used to refer to the no longer existing class CCLayer.
- **Loading Scene** - Refers to the concept of introducing an intermediary scene ("loading scene") whose only purpose is to load the next scene's assets after the incoming transition has ended. Once the next scene's assets are loaded, the loading scene presents (optionally with a transition) the next scene. The loading scene would typically display a loading icon or text, which may or may not be animated.
- **Node** - Refers to the [CCNode](http://www.cocos2d-swift.org/docs/api/Classes/CCNode.html) class but is often used to refer to any class inheriting from CCNode: sprites, labels, etc all inherit from CCNode. Most nodes display content on the screen.
- **Retain Cycle** - A memory management error that prevents two or more objects from deallocating. In its simplest form, object A holds a strong reference to object B, while object B holds a strong reference to object A. Both objects can no longer deallocate because they are essentially waiting for the other object to deallocate first. Matt Gallagher wrote an article with [rules to avoid retain cycles](http://www.cocoawithlove.com/2009/07/rules-to-avoid-retain-cycles.html) which perfectly apply to a hierarchical object structure like the parent-child relationship of Cocos2D nodes.
- **Scene** - A [CCScene](http://www.cocos2d-swift.org/docs/api/Classes/CCScene.html) class contains the currently visible, active nodes. Scenes are presented by the Director and can be replaced by other scenes at any time, optionally animated with a transition.
- **Transition** - Refers to the [CCTransition](http://www.cocos2d-swift.org/docs/api/Classes/CCTransition.html) class that animates the change from one scene to another scene.
- **View** - Refers to the Cocos2D view. It can refer to either the CCGLView or CCMetalView classes in iOS apps, or the CCGLView class in OS X apps.

## Todo
- CCB (CCBi, SpriteBuilder Document File)
- GUI
- Particle
- Physics (World)
- Body
- Joint
- Batch Drawing
- Sprite
- Texture
- Image
- Label
- Tilemap
- Timeline
	- Timeline Cursor, Timestamp
- Keyframe
- Node Tree (Hierarchy, Scene/Node Graph)
- Sprite Sheet (Texture Atlas)
- Anchor Point
- Sibling Node
- Parent Node
- Children


#### Not specifically CC/SB
- Shader
- OpenGL
- Metal
- Cocoa (UIKit)
