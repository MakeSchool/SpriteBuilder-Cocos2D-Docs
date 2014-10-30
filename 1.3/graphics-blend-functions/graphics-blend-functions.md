#Blending visual layers

When putting two layers on top of each other OpenGL provides the ability to control how the two sources of pixel information are merged together and rendered on the screen.  This gives you the ability to select whether the top image is completely opaque and the renderer should ignore all of the original pixel information, or if the two layers should be belded together, allowing the color of the image to be influenced by the background it is on or to create effects like a glow around an image.  SpriteBuilder provides a visual interface for setting these rendering options at the bottom of the properties panel for appropriate node types(color nodes, gradient nodes, particle effects).


![img](../_images/editor/node-color-blendfunc-properties.png)

When placing two pixels on top of each other, the final color that is rendered to the screen is determined using the following equation:

Final Color = Source Color * Source Multiplier + Destination Color * Destination Multiplier

It's important to note that pixel calculations are done in terms of additive color mixing for RGB, not subtractive color mixing as might be done when drawing/painting.  If your blending is not resulting in the colors you expect, check how those colors add in terms of light.

The properties panel gives you complete control over the blending equation - the Source color and destination color are automatically calculated from the provided images, so the Blend src and Blend dst drop downs give you control over the source and destination multiplier.  Using the equation above it is possible to make basic predictions about the resulting colors given certain multipliers.  To have the image appear without blending, set the blend Src to One and the Blend dst to Zero.  To have the image not render at all set the Blend src to Zero and the Blend dst to One.

SpirteBuilder has built in defaults for two of the most common methods of layering images - Normal and Additive.  A Normal layering renders the image as it would be seen with no background.  Additive layering means that the color of the source and destination images will be added together according to the rules of RGB color mixing

More experienced users can also set the rendering factors for the source and destination manually for special mixing effects.  You can read more about working with the OpenGLES renderer [here.](http://www.khronos.org/opengles/sdk/docs/man/xhtml/glBlendFunc.xml)