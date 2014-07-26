#Applying CCActions to Nodes

CCActions exist as independent objects.  As a result, it is possible to apply the same CCAction to any node at anytime in code using the startWithTarget method and specifying which node to run it on.  This causes the action to begin altering the properties of that object.  There is a step method that is called every time the frame is updated with the action, allowing for programatic modifications to the object on top of the actions.  stopAction can be called at anypoint to stop an action in the middle of its execution, otherwise the stop function will be called automatically when the action runs out of sequence to run, and from here any post-action code can be written.

For more information ce the [CCAction Class Reference.](http://www.cocos2d-swift.org/docs/api/Classes/CCAction.html#//api/name/stop)

##Running code from actions

Cocos2D provides two actions that allow running code:

- CCActionCallFunc (uses selectors)
- CCActionCallBlock (uses blocks)

Most developers use this kinds of actions within a sequence. A common pattern is having a `CCActionSequence` and adding a `CCActionCallFunc` or `CCActionCallBlock` as the last action. This pattern provides a callback for a `CCActionSequence`.