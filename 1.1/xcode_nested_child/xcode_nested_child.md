#CCNode's Add/Remove Child Methods

Every scene in Cocos2D is built from a root node.  As a result the entire heirarchy of the scene can be constructed using each nod's addChild method.  Variants on this method can also specify tags or z-orderings.  As a result, if you are building a scene from scratch, you will need to initialize it in a specific order so that nodes can be added as the children of appropriate other nodes.

When adding a child it inherits some of the properties of its parents, so if the parent is currently running, when the child is added it will immediatly run its onEnter function.  Additionally,  Additionally, the child node will inherit the parent's coordinate system and will be included in CCActions that are performed on the parent node.