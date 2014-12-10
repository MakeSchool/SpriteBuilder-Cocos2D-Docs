# Working with Actions

<table border="0"><tr><td width="48px" bgcolor="#d0f0ff"><strong>Info</strong></td><td bgcolor="#d0f0ff">
Read the [Action Concepts](./concepts/cocos2d-actions) article for a conceptual overview of the action system, how it works, what to use it for and when not to use it. Specifically reas the section that explains where actions can be problematic, and why.

This article will focus on the implementation details.
</td></tr></table>

Cocos2D's action system is a way to animate a node's properties either instantaneously or (most commonly) over time.

## Actions Overview

Actions can be divided into three classes:

- Instant actions inherit from [`CCActionInstant`](http://www.cocos2d-swift.org/docs/api/Classes/CCActionInstant.html)
- "Over Time" actions inherit from [`CCActionInterval`](http://www.cocos2d-swift.org/docs/api/Classes/CCActionInterval.html)
- "Special" actions inherit directly from [`CCAction`](http://www.cocos2d-swift.org/docs/api/Classes/CCAction.html)

You'll find more information and a list of individual actions in the class reference. Click the class names above to open the class reference. Also see the [CCNode reference](http://www.cocos2d-swift.org/docs/api/Classes/CCNode.html), specifically the "Working with Actions" section.

## Creating Actions

If an action provides a custom initializer (see class reference) you should always use the action class' custom initializer rather than the ones inherited from super classes. In fact almost all actions use either a custom initializer or the `actionWithDuration:` initializer of the `CCActionInterval` class.
		
A simple example with a move action:

#### Objective-C
	id move = [CCActionMoveTo actionWithDuration:2.4 position:CGPointMake(123, 444)];

#### Swift
	var move = CCActionMoveTo(duration: 2.4, position: CGPointMake(123, 444))

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
The generic type `ìd` or `CCAction*` are frequently used over the action's actual class name as it is more convenient to type and easier to change action classes while experimenting. You typically won't call methods or access properties of actions either. At best you'll set a tag (CCAction property) or reverse the action (CCActionFiniteTime method).
</td></tr></table>
	
## Running Actions

Actions need to be run on a node for them to have any effect. Of course the node itself also needs to be in the node tree and must not be paused for actions to run.

#### Objective-C
	[node runAction:move];
	
#### Swift
	node.runAction(move)


An action runs until it "completes". Once an action has run its course, it is automatically removed from the node and deallocates - that is unless you kept a reference to the action in an ivar or property.

## Copying Actions

All actions implement the [NSCopying](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSCopying_Protocol/index.html) protocol, which means they can receive the `copy` message and will correctly reset their internal state. The copied action will be exactly like a newly instantiated action.

<table border="0"><tr><td width="48px" bgcolor="#d0f0ff"><strong>Info</strong></td><td bgcolor="#d0f0ff">
The performance difference (if any) between copying or creating a new action instance with the same parameters is negligible.
</td></tr></table>

### Running the same Action on multiple Nodes

To run the same action on multiple nodes without having to create multiple actions using the same parameters, you can simply copy an existing action.

#### Objective-C
	id move = [CCActionMoveTo actionWithDuration:2.4 position:CGPointMake(123, 444)];
	
	// run the first action normally
	[node1 runAction:move];
	
	// additional nodes must run a copy of the original action!
	[node2 runAction:[move copy]];
	[node3 runAction:[move copy]];

#### Swift
    var move = CCActionMoveTo(duration: 2.4, position: CGPointMake(123, 444))
        
    // run the first action normally
    node1.runAction(move)
        
    // additional nodes must run a copy of the original action!
    node2.runAction(move.copy() as CCAction)
	node3.runAction(move.copy() as CCAction)

Notice the forced cast to `CCAction` in the Swift example. This is necessary because the [copy method of `NSObject`](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSObject_Class/index.html#//apple_ref/occ/instm/NSObject/copy) returns a [`AnyObject`](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TypeCasting.html#//apple_ref/doc/uid/TP40014097-CH22-XID_516).

Note that you can also copy the action for the first node. Thus the above code can also be written more consistently as:

#### Objective-C
	[node1 runAction:[move copy]];
	[node2 runAction:[move copy]];
	[node3 runAction:[move copy]];

#### Swift
    node1.runAction(move.copy() as CCAction)
    node2.runAction(move.copy() as CCAction)
	node3.runAction(move.copy() as CCAction)

This is just a more generic version of the above code. You needn't worry about the performance of copying actions, nor copying one action more than necessary. The performance impact is negligible, probably not even measurable.

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
Each node has to run its own instance of every action! The same action must not be run on multiple nodes without copying (or reversing) it. Running the same action on multiple nodes will result in undefined behavior, and will only have one of the actions (typically the one that was run last) performing its task.
</td></tr></table>

### Re-Using an Action at a later time

To re-use an action you would normally just copy an existing instance (see above). Creating a copy as in `[anAction copy]` returns a version of the action that has been reset to its initial state.

Since actions that run to completion will automatically deallocate, you will have to keep a strong reference to any action that you like to re-use. Typically you just need to create a property or ivar without the `weak` keyword, or an array. Then assign respectively add any actions to it that you want to re-use at a later time.

#### Objective-C
	@interface MyClass : CCNode
	{
		id _reusableAction;
		..

#### Swift
	class MyClass: CCNode
	{
    	var _reusableAction : CCAction?
	    ..

At the time of re-use, be sure to send the re-used action the copy message:

#### Objective-C
	// assigning an action to an ivar and run the action
	_reusableAction = [CCActionMoveTo actionWithDuration:2.4 position:CGPointMake(123, 444)];
	[node runAction:_reusableAction];

	// at a later time you can re-use the same action by running a copy of it
	[node runAction:[_reusableAction copy]];

#### Swift
    // assigning an action to an ivar and run the action
    _reusableAction = CCActionMoveTo(duration: 2.4, position: CGPointMake(123, 444));
    node.runAction(_reusableAction);
        
    // at a later time you can re-use the same action by running a copy of it
    node.runAction(_reusableAction!.copy() as CCAction);
    
Note that the `_reusableAction` property in the Swift example is declared as an optional (it initially doesn't have a value) and therefore needs to be unwrapped via the exclamation mark suffix.

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
Do not call `init` again on an action! This used to be recommended in Cocos2D versions prior to v3 - before actions implemented the `NSCopying` protocol - but this only ever worked correctly for specific actions and can only be advised against in any Cocos2D version due to the potential for undefined behavior, memory leaks, and crashes.
</td></tr></table>

## Reversing Actions

Some actions inheriting from `CCActionInterval` can be reversed. This means the action runs in the opposite direction, from end to start. So instead of moving to a specific location, the reverse would be to move from the destination to the current location.

To reverse an action send it the `reverse` method before running it:

#### Objective-C
	[node runAction:[move reverse]];
	
#### Swift
	node.runAction(move.reverse())

Like `copy` the `reverse` method returns a new instance of the action. It is therefore not necessary to combine copy and reverse, for example if you want an action run from start to finish, and then reverse it. In that case it is sufficient to reverse the original action.

## Stopping Actions

Sometimes it may be necessary to stop an action prematurely. Besides `[node stopAllActions]` you can also stop individual actions.

If you have a reference to an action, you can stop that action by reference:

#### Objective-C
	[node stopAction:move];
	
#### Swift
	node.stopAction(move)
	
If you don't have a reference to an action you need to tag the action when creating it. For instance:

#### Objective-C
	CCAction* move = [CCActionMoveTo actionWithDuration:2.4 position:CGPointMake(123, 444)];
	move.tag = 123;
	[node runAction:move];

#### Swift
    var move = CCActionMoveTo(duration: 2.4, position: CGPointMake(123, 444))
    move.tag = 123;
   	node.runAction(move)

	
You can then remove an action by its tag:

#### Objective-C
	[node stopActionByTag:123];
	
#### Swift
    node.stopActionByTag(123)

Note that this will only remove the first action with this tag. If you need to stop multiple actions with the same tag, try to tag them differently. But if this isn't feasible, you can use the following snippet to remove all actions with the same tag:

#### Objective-C
    while ([node getActionByTag:123] != nil) {
        [node stopActionByTag:123];
    }
    
#### Swift
    while (node.getActionByTag(123) != nil) {
        node.stopActionByTag(123)
    }


## Obtaining Running Actions

To get a reference to a running action, you can just simply store the action after creating it in an ivar or property. But you can also tag it and do:

#### Objective-C
	id actionWithTag123 = [node getActionByTag:123];

#### Swift
	var actionWithTag123 = node.getActionByTag(123)

Note that this will return nil if there's no action with the given tag. It will also return only the first action with the given tag.

You can also test whether there are any active actions in the first place:

#### Objective-C
	if (node.numberOfRunningActions > 0) {
		NSLog(@"node is running 1 or more actions");
	}

#### Swift
    if node.numberOfRunningActions() > 0 {
        NSLog("node is running 1 or more actions");
    }

And you can check whether actions may be paused. This is the case when either the node is paused, or one of the node's parents is paused, or when the node isn't currently in the node tree. Therefore just checking the paused state isn't enough, you have to test for the active state:

#### Objective-C
	if (node.runningInActiveScene) {
		NSLog(@"node is active (not paused), so actions aren't paused either");
	}
	
#### Swift
	if node.runningInActiveScene {
        NSLog("node is active (not paused), so actions aren't paused either");
    }

## Running Code with Actions

Two actions allow you to run a selector ([CCActionCallFunc](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallFunc.html)) respectively run a block ([CCActionCallBlock](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallBlock.html)). Running a block is preferred, as it is more powerful and flexible.

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
Typically call block/func actions are only used within a sequence (see below) as there's very little use for them otherwise, since you could just call the method in question respectively run the code directly.
</td></tr></table>

How to create a call block action:

#### Objective-C
	id block = [CCActionCallBlock actionWithBlock:^{
		// run code here
	}];

#### Swift
    var block = CCActionCallBlock { () -> Void in
        // run code here
    }

The block takes no parameters and returns no value.

How to create a call func action:

#### Objective-C
	id callFunc = [CCActionCallFunc actionWithTarget:self selector@selector(theMethod)];
	
#### Swift
    var callFunc = CCActionCallFunc(target: self, selector:Selector("theMethod"))

Where `theMethod` must be implemented by the target with the following signature:
	
#### Objective-C
	-(void) theMethod {
    	NSLog(@"call func action ran my method");
	}

#### Swift
    func theMethod() -> Void {
        NSLog("call func action ran my method");
    }

The selector takes no parameters and returns nothing (void).

### When not to use CallBlock/Func

The following is typically overkill:

#### Objective-C
	id block = [CCActionCallBlock actionWithBlock:^{
		[node removeFromParent];
	}];
	[node runAction:block];

#### Swift
    var block = CCActionCallBlock ({ () -> Void in
        node.removeFromParent();
    })
   	node.runAction(block)
       	
Unless there's a reason to defer the execution to the next frame, the above can be reduced to simply running the code (here: calling the method) directly:

#### Objective-C
	[node removeFromParent];

#### Swift
	node.removeFromParent()

## Sequences and Spawning Actions

You can run a series of actions in sequence, and even have some actions run in parallel while the sequence is running.

To setup a complex, linear sequence with spawning actions:

#### Objective-C
	// create individual actions used in sequence
	id move = [CCActionMoveBy actionWithDuration:5 position:CGPointMake(222, 111)];
	id wait = [CCActionDelay actionWithDuration:2];
	id rotate = [CCActionRotateBy actionWithDuration:2.0 angle:90];
	id fade = [CCActionFadeOut actionWithDuration:1.5];
	id block = [CCActionCallBlock actionWithBlock:^{
		// run completion code here ...
	}];
	id remove = [CCActionRemove action];
	
	// spawn these actions in parallel (all at once) and wait for the longest-running to finish
	id spawn = [CCActionSpawn actionWithArray:@[rotate, fade]];
	
	// run the sequence
	id sequence = [CCActionSequence actionWithArray:@[move, wait, spawn, block, remove]];
	[node runAction:sequence];

#### Swift
    // create individual actions used in sequence
    var move = CCActionMoveBy(duration: 5, position: CGPointMake(222, 111))
    var wait = CCActionDelay(duration: 2)
    var rotate = CCActionRotateBy(duration: 2.0, angle: 90)
    var fade = CCActionFadeOut(duration: 1.5)
    var block = CCActionCallBlock { () -> Void in
        // run completion code here ...
    }
    var remove = CCActionRemove()
    
    // spawn these actions in parallel (all at once) and wait for the longest-running to finish
    var spawn = CCActionSpawn(one: rotate, two: fade)
    
    // construct the sequence, then run it
    let sequenceActions = [move, wait, spawn, block, remove]
    var sequence = sequenceActions[0]
    for var i = 1; i < sequenceActions.count; i++
    {
        sequence = CCActionSequence(one: sequence, two: sequenceActions[i])
    }
    node.runAction(sequence);

<table border="0"><tr><td width="48px" bgcolor="#d0f0ff"><strong>Info</strong></td><td bgcolor="#d0f0ff">
Notice how the Swift version requires constructing the sequence by repeatedly using the `one:two:` initializer. There is currently no Swift initializer for `CCActionSequence` and `CCActionSpawn` that takes an array as input. See [issue #1116](https://github.com/cocos2d/cocos2d-swift/issues/1116).
</td></tr></table>

This sequence first runs the move action, then pauses (waits) for 2 seconds. After that the spawn action will run the rotate and fade actions simultaneously. The sequence only continues after the longest-running action in the spawn group finishes, which in this case is the rotate action. 

A block then runs to perform any custom code when the sequence is complete. Lastly the sequence runs the remove action which removes the node from the node tree.

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
The CCActionSpawn action serves little purpose outside of a sequence. In such a case it would be equivalent to running the spawned actions individually. The spawn action only allows you to more easily test whether all spawned actions have finished or not, though you can achieve the same even more conveniently with a sequence and a call block/selector action at the end.
</td></tr></table>

### Sequence Example: "Ping-Pong" Loop Forever

This sequence will have a node move from A to B, then move back to A. The sequence repeats forever (until stopped):

#### Objective-C
	id move = [CCActionMoveTo actionWithDuration:2.4 position:CGPointMake(123, 444)];
	id sequence = [CCActionSequence actionWithArray:@[move, [move reverse]]];
	id forever = [CCActionRepeatForever actionWithAction:sequence];
	[node runAction:forever];
	
#### Swift
    var move = CCActionMoveTo(duration: 2.4, position: CGPointMake(123, 444))
    var sequence = CCActionSequence(one: move, two: move.reverse())
    var forever = CCActionRepeatForever(action: sequence)
    node.runAction(forever)


## Easing Actions

Easing actions wrap an existing action to change the action's progress over time.

![Interpolation Example](../spritebuilder/keyframe-editor-easing-example-animation.gif "Interpolation Mode Example Animation")

To create an easing action you initialize it with an existing action that inherits from `CCActionInterval`:

#### Objective-C
	id move = [CCActionMoveTo actionWithDuration:4 position:CGPointMake(654, 321)];
	id easeMove = [CCActionEaseInOut actionWithAction:move];
	[node runAction:easeMove];

#### Swift
    var move = CCActionMoveTo(duration: 4, position: CGPointMake(654, 321))
    var easeMove = CCActionEaseInOut(action: move)
    node.runAction(easeMove);

## More Actions

Please refer to individual action class' references for additional details and code examples. See the [`CCAction` reference](http://www.cocos2d-swift.org/docs/api/Classes/CCAction.html) and its subclasses.
