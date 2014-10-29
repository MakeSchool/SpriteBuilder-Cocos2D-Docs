The JSON structure was altered in the 1.1 folder so it will likely break the build system - top level is now an object with fields for each section so that headings can be easily implemented

The file names for the files that were coppied over need to be updated to match the folder names

Files coppied over from existing documentation may contain duplicates - information should be pared down based on new context



Section on CCB Reader?

Section on adjusting the stage size?

Talk about base node of scenes/CCBs?


Section on the layer blending options?


Add a section to build a simple game before the sections where we break everything down?



Find appropriate home for:

## Moving Nodes

In general nodes can be selected on the stage and can be dragged to a new position. As of SpriteBuilder 3.1 you can also select multiple nodes at once and move them all together. Hold the *Shift* (⇧) key and select multiple nodes by clicking onto them. Then drag any of the selected nodes and you will see that the nodes move as a group.


## Changing zOrder
Unlike other properties, the zOrder is not set in the properties inspector in SpriteBuilder. Instead, the zOrder is determined by the ordering of objects in the hierarchy view in the timeline. All objects you add to a ccb file will show up in the hierarchy view. To arrange them, simply drag and drop them to the position that you require.

![image](ccb-order.png)

When loaded into your app, the zOrder of your nodes will be numbered from 0 to (N-1), where N is the number of children the parent node has. 