#Recieving Information from SpriteBuilder in Code

A callback function is a function that is run after a task is complete.  Within SpriteBuilder it is possible to setup callback functions on nodes that take user input.  Decendents of CCControl in SpriteBuilder (button, text field) have a property called Selector.  This is the name of a method which will be called once the user input is finished.  Code that should be executed anytime the values in these user interactive fields are altered should be placed in these methods.

For more information on manipulating visual elements, see the [code connections](link) section.

This section should probably be moved to the Xcode portion of the documentation