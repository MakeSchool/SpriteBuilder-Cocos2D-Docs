# Glossary

## A-Z

- **Action** - Refers to all classes that inherit from [CCAction](http://www.cocos2d-swift.org/docs/api/Classes/CCAction.html). Actions animate properties of a node over time. Actions can be in a sequence and repeated. Actions can be used to time events using [CCActionDelay](http://www.cocos2d-swift.org/docs/api/Classes/CCActionDelay.html) and [CCActionCallBlock](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallBlock.html) or [CCActionCallFunc](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallFunc.html) in a [CCActionSequence](http://www.cocos2d-swift.org/docs/api/Classes/CCActionSequence.html).
- **Batch Drawing** - The process of drawing similar things in quick succession by not having to change OpenGL state (ie drawing multiple items with a single "draw call"). Cocos2D automatically optimizes nodes for batch drawing.
- **Body** - The non-visual physics representation of a node. A body has one or more collision shapes attached.
- **bpp* stands for "bits per pixel". A 24 bpp texture allows the full color range of 16.7 million colors.
- **CCB** - Refers to a SpriteBuilder document (text file, plist format) which carries the `.ccb` file extension. CCB stands for **C**o**C**os**B**uilder. The SpriteBuilder project used to be known as CocosBuilder.
- **CCBi** - A SpriteBuilder document in compressed binary form optimized for in-app loading. The *i* stands for b*i*nary.
- **Director** - The core class in Cocos2D. Acts as view controller, manages the render loop, presents scenes.
- **Document** - SpriteBuilder document. See also **CCB**.
- **Draw Call** - Refers to the overhead caused by OpenGL context switching, this usually happens when changing the GL state (ie different blend modes) or when binding a different texture. A draw call overhead is quite significant therefore it is crucial to keep the number of draw calls to a minimum via Batch Drawing.
- **GUI** - Graphical User Interface. Refers to designing and programming user interface views and controls.
- **Image** - Refers to a image resource file.
- **Interpolation** - A technique that changes the value of a property between two keyframes over time. Interpolation can be linear, instance or one of the SpriteBuilder easing modes.
- **Joint** - A connection between two bodies defining a constraint between the two bodies.
- **Keyframe** - A point in the Timeline which marks the values a node should have at that point. The property value is interpolated between two keyframes depending on the interpolation mode.
- **Layer** - A concept of grouping nodes together so that an entire branch of the node hierarchy can be animated separately from other layers. Most nodes can be used as the parent node for a layer but typically [CCNode](http://www.cocos2d-swift.org/docs/api/Classes/CCNode.html) is chosen for this task. Used to refer to the no longer existing class CCLayer.
- **Loading Scene** - Refers to the concept of introducing an intermediary scene ("loading scene") whose only purpose is to load the next scene's assets after the incoming transition has ended. Once the next scene's assets are loaded, the loading scene presents (optionally with a transition) the next scene. The loading scene would typically display a loading icon or text, which may or may not be animated.
- **Node** - Refers to the [CCNode](http://www.cocos2d-swift.org/docs/api/Classes/CCNode.html) class but is often used to refer to any class inheriting from CCNode: sprites, labels, etc all inherit from CCNode. Most nodes display content on the screen.
- **Node Tree** - (Also: *Node Hierarchy*, *Scene Graph*, *Node Graph*) Refers to the tree-like structure composed of nodes. Also refers to the Node Tree in the SpriteBuilder Timeline where you can select, move, rename nodes.
- **Particle** - Essentially a light-weight sprite controlled by a Particle Emitter. Has no physics and can not be modified by the user except indirectly through particle emitter properties.
- **Physics Simulation** - The process of calculating physics movements and collisions.
- **Retain Cycle** - A memory management error that prevents two or more objects from deallocating. In its simplest form, object A holds a strong reference to object B, while object B holds a strong reference to object A. Both objects can no longer deallocate because they are essentially waiting for the other object to deallocate first. Matt Gallagher wrote an article with [rules to avoid retain cycles](http://www.cocoawithlove.com/2009/07/rules-to-avoid-retain-cycles.html) which perfectly apply to a hierarchical object structure like the parent-child relationship of Cocos2D nodes.
- **Scene** - A [CCScene](http://www.cocos2d-swift.org/docs/api/Classes/CCScene.html) class contains the currently visible, active nodes. Scenes are presented by the Director and can be replaced by other scenes at any time, optionally animated with a transition.
- **Sibling Node** - Refers to a node with the same parent (ie in the same level of the Node Tree).
- **Sprite** - The node that draws a texture on the screen with various properties such as rotation, scale, opacity.
- **Sprite Sheet** - Also known as Texture Atlas. A large image created by combining multiple images into one. Using sprite sheets reduces memory usage and draw calls.
- **Texture** - An in-memory representation of an image that can be rendered to the screen via a Sprite or otherwise. Textures are necessary because graphics chips can not process images directly.
- **Tilemap** - Sprites arranged in a rectangular or isometric grid, forming a map.
- **Timeline** - The bottom-center area in SpriteBuilder containing the Node Tree and the Keyframe Editor.
- **Timeline Cursor** - The vertical blue line in the SpriteBuilder Keyframe Editor that highlights the animation's current time stamp.
- **Timestamp** - The "location in time" the current Timeline is at, for instance at timestamp 00:04:12.
- **Transition** - Refers to the [CCTransition](http://www.cocos2d-swift.org/docs/api/Classes/CCTransition.html) class that animates the change from one scene to another scene.
- **View** - Refers to the Cocos2D view. It can refer to either the CCGLView or CCMetalView classes in iOS apps, or the CCGLView class in OS X apps.
