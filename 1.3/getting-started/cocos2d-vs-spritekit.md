# Cocos2D compared to Sprite Kit

Are you wondering what Cocos2D has to offer above and beyond Sprite Kit?

Cocos2D's offering is actually quite compelling, if you know what to look for in a game engine. Sprite Kit may be popular thanks to Apple including it in their SDKs, but the matter of fact is that Sprite Kit was designed based on Cocos2D's principles, idioms and programming interface. If you've been using Sprite Kit already, you'll feel right at home with Cocos2D!

This page intends to highlight Cocos2D's features that you won't find in Sprite Kit, not now and (for some) not ever.

## Why Cocos2D is the Better Choice ...

Cocos2D has/is/does ...

- **Open Source** - Get the source code for both Cocos2D and SpriteBuilder, stable release or latest development build - it’s up to you. Learn what's going on behind the scenes, apply custom modifications, understand and fix issues yourself.
- **Frequent updates**, with timely bugfix releases. Whereas Sprite Kit is tied to a (on average) bi-annual iOS update cycle.
- **Approachable developers and responsive community**. Most Cocos2D engineers come from the community, they don't cloak themselves in secrecy or dazzling marketing speak.
- **Runs on Android**, no Java, C or C++ programming required. Build, run and debug on Android devices directly from within Xcode with the [SpriteBuilder Android Plugin](https://store.spritebuilder.com/products/spritebuilder-android-plugin-starter).
- **SpriteBuilder, the visual design tool** optimized for game development with asset management, timeline animations, physics editing, native GUI controls, screen resolution scaling, texture atlas generator, just to name a few features. Xcode Playground doesn’t even begin to compare with SpriteBuilder.
- **Visual effects** are easier to use, faster and more impressive than what you can do with SKEffectNode, and most effects can be combined on the same node. Visual effects include:
	- Bump-Mapped 2D Lighting, Bloom, Blur, Refraction, Reflection, Pixelation, Outline, Drop Shadow, Motion Streak, Hue/Color, Contrast, Saturation, Brightness, Color Inversion, and of course particle emitters.
- **Optimized Renderer** with OpenGL (ES) and Metal support. Rendering is generally at least as fast as Sprite Kit, if not faster, and also supports auto-batching draw calls.
- **Unrestricted Graphics Programming**, including shaders. Leverage the full power of OpenGL (ES) or Metal any time you need it. A straightforward API for basic rendering tasks (ie drawing textured polygons) is also available which uses OpenGL or Metal transparently, depending on settings and device.
- **Physics engine is faster and highly configurable** with both Objective-C and optional C programming interface for even more speed and control. Key enhancements over Sprite Kit's physics are:
	- *Separate collision callbacks* definable for each user-defined collision type combination, plus wildcard callbacks (“body x collided with any other body”).
	- *Autogeometry* generates new collision shapes within milliseconds, great for destructible terrain.
	- *Action animation support* for kinematic bodies.
- **Native GUI Nodes and GUI Design Features**:
	- Controls: Button, Slider, Textfield, Scroll View, Table View, plus custom controls.
	- Layout: vertical or horizontal direction, and grid layouts. Align nodes to any corner, auto-adjust position, scale, size based on screen size.
	- Bitmap and Truetype Font labels, with support for NSAttributedString.
- **Complete audio playback engine (ObjectAL)** with OpenAL support for short sound effects and AVAudioPlayer for streaming audio. Plays nice with background (iPod) music, too.
- **Isometric & Orthogonal Tilemaps**, with support for Tiled’s TMX file format.

These are just the main outstanding features Cocos2D offers on top of Sprite Kit's feature set. There are even more improvements in detail, for instance built-in easing actions or a node that draws color gradients. 

You may want to browse the [Cocos2D-SpriteBuilder Class Reference](http://cocos2d.spritebuilder.com/docs/api/index.html) to learn more about the available classes.

## See Cocos2D & SpriteBuilder in Action ...

### Galactic Guardian Demo Game
<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/9lUs4I_PNq0?rel=0" frameborder="0" allowfullscreen></iframe>

### Bump-Mapped Lighting & Particle Effects

<iframe width="640" height="480" src="https://www.youtube-nocookie.com/embed/g5fCq8qJJQA?rel=0" frameborder="0" allowfullscreen></iframe>

### Shader Effects Demo
<iframe width="568" height="320" src="//www.youtube-nocookie.com/embed/7dyj6NkM8Ew?rel=0&amp;showinfo=0" 
frameborder="0" allowfullscreen></iframe> 

