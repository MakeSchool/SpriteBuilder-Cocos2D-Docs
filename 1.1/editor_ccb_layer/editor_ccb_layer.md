When creating a CCB Layer you will be prompted with the ability to enter a content size.  By default this is set to the size of an iPhone5, so the layer would fill an entire scene.  It's ok if you are unsure what the layer size should be when the layer is created - you will be able to alter it later.

[image](layer_create.png)

A layer generates a canvas similar to a scene with a CCNode as the root.  If you select the CCNode you will have the ability to edit the content size and anchor point for the layer.

Be aware that altering the content size of the layer does not alter the stage size.  When the layer file is first configured these two values will be set to be the same, but if you alter the content size without altering the stage, you may be dragging and dropping content onto a part of the stage that is no longer within your layer view.  For more information about altering the stage size, see ____ portion of the documentation.(link)   

#########
Except this doesn't appear to be true - for some reason whatever's on the stage, even outside the content area, appears on screen

###