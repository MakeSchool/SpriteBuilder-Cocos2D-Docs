CCB files provide you with a way to encapsulate data.  By creating a system or animation once within a CCB file you can then instantiate it as many times as you want, and when you update the CCB, every instance will change automatically.

There are 5 different CCB file types.  While all of the files are .ccbs, when you select the appropriate file type it comes pre-configured  with the appropriate sizes and base nodes.  While in some situations it is possible to generate CCB files that act equivelently (adding a sprite to a node file will allow the same behavior as generating a sprite CCB file), in other situations certain setttings cannot be configured after the file has been generated (you cannot set the content area for a scene the way you do a layer since it is assumed the scene will take up the full screen).  Selecting the proper file type for different purposes will make your life easier, but if you are just starting out with SpriteBuilder don't worry too much about the differences between a node file and sprite file - you will learn the advantages and limitations of each file type in time.

The five different types of ccb-files are:

- **Scenes** will fill the full area of the device.
- **Nodes** are logically represented by a single point. Use this type for creating character animations or other game components.
- **Layers** are nodes with a content size. This is useful, for instance, when creating levels or contents for scroll views.
- **Sprites** are sprite nodes. This is useful, for instance, when you want to add a physics body to a single sprite.
- **Particles** are particle systems. Use this option for creating stand alone particle systems.


Note: Since all of these different file types have the same extension (.ccb), different ccb types cannot have the same name.  For example, you cannot both a node and scene called "Hero".

One aspect of including CCB files in scenes is that you can set animations and physics propreties in many cases both within the CCB file and on the stage you place it on.  As a result it is possible to create effects that have a direct influence on each other but are generated in entirely different locations which can create confounding effects that are hard to debug.  Therefore, it's extremely improtant to apply animations and physics in logical places since otherwise it can be hard to determine where the undesired effect is coming from.

One of the best properties about CCB files is that they encapsulta data so that you  don't have to maniuplate it directly on your main scene.  As a result, when you drag and drop a CCB file onto the stage you will not be able to alter the content size or anchor point in the inspector.  Instead, you will interact with the file as a whole, altering the scale of the file on the screen, the rotation and position of the object, and even the skew.  To edit the anchor point or content size, open the CCB file and work with these properties directly.