# Cocos2D 3.1.0 Release Notes:

Since shortly after the release of Cocos2D 3.0.0-rc.1, the Cocos2D team has been working on the major features of 3.1. The biggest changes have been related to rendering, and nearly all of the OpenGL code in Cocos2D has been upgraded and replaced. A lot of great improvements have come out of this!

* **Automatic batching:** No need to use CCSpriteBatchNodes anymore. Everything from sprites, to particles, to gradients are automatically batched when possible!
* **Visibility Culling:** Draw calls are expensive. Don't waste time drawing sprites that aren't even on the screen.
* **Simplified Custom Drawing:** Custom drawing in previous Cocos2D versions required a lot of OpenGL knowledge to use effectively. 
* **Simplified Shaders:** Shaders in Cocos2D 2.x weren't easy to use even for experienced GL developers. You'll still need to learn GLSL, but it will lower the learning curve significantly. With a solid shader foundation in place we can start working on an easy to use system of pre-made effects for non-programmers to use in future versions.
* **Simpler OpenGL Usage:** The interaction between Cocos2D and OpenGL has been simplified for advanced users. Those pesky `ccGL...()` functions are gone. You don't need to be so careful about corrupting Cocos2D's GL state since it doesn't rely on carefully managed state variables.
* **More Efficient Tilemaps:** In many cases, several orders of magnitudes more efficient in GPU and memory usage. The range of visible tiles are calculated, and only those tiles are rendered. There is some experimental functionality for animating tilemaps as well.

Another focus has been on allowing actions and physics to work together. This will be great for anybody that wants to animate their physics objects. This isn't a feature you'll find in other engines like SpriteKit or Unity!

## New APIs:

* New CCAction subclasses: `CCActionEaseInstant`, `CCActionSpriteFrame` and `CCActionSoundEffect`
* New CCNode protocol: `CCShaderProtocol`. The methods are already implemented in CCNode. Add the protocol to your subclasses to expose them.
* `CCBlendMode` class that provides more extensive blending mode settings.
* `CCRenderTexture` can now have custom projections and custom content scales.
* Lots of new goodies in `CCRenderer.h` for implementing custom draw functions.
* New `CCShader` class to replace `CCGLProgram` from Cocos2D 2.x.

## Deprecations:

* `CCNode.blendFunc` has been deprecated and replaced with the much more flexible `CCNode.blendMode`.
* `CCSpriteBatchNode` and `CCParticleSystemBatch` instances should be replaced with CCNode instances. They now do very little other than providing a property for an otherwise unused atlas texture.
* `CCNodeGradient.compressedInterpolation` is now a no-op. Instead, gradients will now correctly fill to the bounds of their rectangles regardless of the direction of the gradient.

## API Changes:

We tried to change the public APIs as little as possible, but a few things had to be broken to make progress.

* Kazmath has been replaced by GLKMath. GLKMath is significantly easier to use and more complete than Kazmath. Additionally, many methods now take or return explicit transforms instead of passing them using global variables.
* `[CCDirectorDelegate updateProjection]` must now return a GLKMatrix4 for the projection.
* `[CCNode transform]` has changed to `[CCNode transform:]` and now requires it's parent's transform to be passed to it as a parameter.
* `[CCNode draw]` has changed to `[CCNode draw:transform:]` to accept a parameter for the renderer and parent transform.
* Subclasses that override `[CCNode visit]` must override `[CCNode visit:transform:]` instead since the GL and transform state is no longer passed using global variables.
* `[CCNode setOpacityModifyRGB:]` and `[CCNode doesOpacityModifyRGB]` no longer do anything. This flag was a partial fix for an uncommon file format (non-premultiplied .pvr files) that was causing a lot of issues with advancing blend mode support. Instead you should premultiply your .pvr files. It's a simple _and complete_ fix.
* Blending mode changes to `CCSpriteBatchNode` and `CCParticleBatchNode` instances are not propagated to their children anymore.
* The `CC_ENABLE_GL_STATE_CACHE` compile time macro has been removed.
* `[CCTiledMapLayer tileAt:]` has been removed as it would have been very difficult to retain the feature while updating the tile map renderer. Instead there is experimental animation block you can apply to tilemaps. This allows you to perform tilemap animation which was the primary use for `tileAt:`.
* `CCTiledMap` no longer supports hexagonal maps. The Tiled map editor (which is the only format Cocos2D can read) has not supported hexagonal maps for several years.

## Private API Changes:

In case you were using them, the following private APIs have also changed. This only includes methods declared in the private headers.

* `CCNode.shaderProgram` has been replaced with `CCNode.shader`.
* `CCNode.glServerState` has been replaced with `CCNode.renderState`.
* `[CCNode transformAncestors]` has been removed.
* `CCGLProgram` has been nearly completely rewritten as `CCShader`. It should be much easier to use without losing functionality.
* `CCSprite` methods relating to batch nodes have been removed.
