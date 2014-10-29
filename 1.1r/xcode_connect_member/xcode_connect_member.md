#Connecting member variables

A second way to connect SpriteBuilder and code is creating member variable connections. This allows a developer to access SpriteBuilder nodes from code. This, for example, can be useful to update the text displayed in a score label from code.

There a two different types of member variable connections. You need to select the node for which you want to create a code connection.

###Document Root connections

![image](docroot.png)

When *Doc root var* is selected in the member variable connection dropdown, SpriteBuilder will create a code connection with the *Document root*. The *Document root* is the root node of the current scene. When you choose this type of connection you need to fulfil two requirements:

- The *Document root* needs to have a custom class. If the score label is in your *Gameplay* scene you need to select the root *CCNode* of your *Gameplay* scene and set a custom class
- In the custom class that you set up you need to either add a property called *scoreLabel* or member variable called *_scoreLabel*.

When the *CCBReader* loads this scene with the code connection it will automatically assign a reference to the label you selected and store it in the *scoreLabel* property or *_scoreLabel* member variable. 

> Note: If you are using sub ccb files you need to be aware when using code connections.  Specifying the root node as target will refer to the root node of the sub ccb file, not to the root node of the scene the sub ccb file has been added to.

###Owner connections
![image](owner.png)

When *Owner var* is selected in the member variable connection dropdown, SpriteBuilder will create a code connection with the *Owner* of this node. The owner can be defined at runtime when the node is loaded in code, using one of the following two methods (depending if a node or a scene is loaded):

	CCScene *scene = [CCBReader loadAsScene:@"MyScene" owner:myObject];
    CCNode *node = [CCBReader load:@"MyNode" owner:myObject];
    
Requirements:

- The owner class needs either a property called *scoreLabel* or member variable called *_scoreLabel*.

Use the owner connection if you need to decide which class will be connected to the node at runtime.

> Note: The loaded node/scene does not maintain a strong reference to the `owner`. You need to retain the `owner` manually.
