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

	id move = [CCActionMoveTo actionWithDuration:2.4 position:CGPointMake(123, 444)];

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
The generic type `ìd` or `CCAction*` are frequently used over the action's actual class name as it is more convenient to type and easier to change action classes while experimenting. You typically won't call methods or access properties of actions either. At best you'll set a tag (CCAction property) or reverse the action (CCActionFiniteTime method).
</td></tr></table>
	
## Running Actions

Actions need to be run on a node for them to have any effect. Of course the node itself also needs to be in the node tree and must not be paused for actions to run.

	[node runAction:move];

An action runs until it "completes". Once an action has run its course, it is automatically removed from the node and deallocates - that is unless you kept a reference to the action in an ivar or property.

## Reversing Actions

Some actions inheriting from `CCActionInterval` can be reversed. This means the action runs in the opposite direction, from end to start. So instead of moving to a specific location, the reverse would be to move from the destination to the current location.

To reverse an action send it the `reverse` method before running it:

	[node runAction:[move reverse]];

## Re-Using Actions

.....

....

...

## Stopping Actions

Sometimes it may be necessary to stop an action prematurely. Besides `[node stopAllActions]` you can also stop individual actions.

If you have a reference to an action, use the reference:

	[node stopAction:move];
	
If you don't have a reference to an action you need to tag the action when creating it. For instance:

	CCAction* move = [CCActionMoveTo actionWithDuration:2.4 position:CGPointMake(123, 444)];
	move.tag = 123;
	[node runAction:move];
	
You can then remove an action by its tag:

	[node stopActionByTag:123];
	
Note that this will only remove the first action with this tag. If you need to stop multiple actions with the same tag, try to tag them differently. But if this isn't feasible, you can use the following snippet to remove all actions with the same tag:

    while ([node getActionByTag:123] != nil) {
        [node stopActionByTag:123];
    }

## Obtaining Running Actions

To get a reference to a running action, you can just simply store the action after creating it in an ivar or property. But you can also tag it and do:

	id actionWithTag123 = [node getActionByTag:123];

Note that this will return nil if there's no action with the given tag. It will also return only the first action with the given tag.

You can also test whether there are any active actions in the first place:

	if (node.numberOfRunningActions > 0) {
		NSLog(@"node is running 1 or more actions");
	}

And you can check whether actions may be paused. This is the case when either the node is paused, or one of the node's parents is paused, or when the node isn't currently in the node tree. Therefore just checking the paused state isn't enough, you have to test for the active state:

	if (node.runningInActiveScene) {
		NSLog(@"node is active (not paused), so actions aren't paused either");
	}

## Running Code with Actions

Two actions allow you to run a selector ([CCActionCallFunc](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallFunc.html)) respectively run a block ([CCActionCallBlock](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallBlock.html)). Running a block is preferred, as it is more powerful and flexible.

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
Typically call block/func actions are only used within a sequence (see below) as there's very little use for them otherwise, since you could just call the method in question respectively run the code directly.
</td></tr></table>

How to create a call block action:

	id block = [CCActionCallBlock actionWithBlock:^{
		// run code here
	}];

The block takes no parameters and returns nothing.

How to create a call func action:

	id callFunc = [CCActionCallFunc actionWithTarget:self selector@selector(theMethod)];

Where `theMethod` must be implemented by the target with the following signature:
	
	-(void) theMethod {
    	NSLog(@"call func action ran my method");
	}

The selector takes no parameters and returns nothing (void).

### When not to use CallBlock/Func

The following is typically overkill:

	id block = [CCActionCallBlock actionWithBlock:^{
		[node removeFromParent];
	}];
	[node runAction:block];

Unless there's a reason to defer the execution to the next frame, this can be reduced to simply calling the method directly:

	[node removeFromParent];

Or in this particular case one could just use the corresponding action:

	id remove = [CCActionRemove action];
	[node runAction:remove];


## Sequences and Spawning Actions

You can run a series of actions in sequence, and even have some actions run in parallel while the sequence is running.

To setup a complex, linear sequence with spawning actions:

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

This sequence first runs the move action, then pauses (waits) for 2 seconds. After that the spawn action will run the rotate and fade actions simultaneously. The sequence only continues after the longest-running action in the spawn group finishes, which in this case is the rotate action. 

A block then runs to perform any custom code when the sequence is complete. Lastly the sequence runs the remove action which removes the node from the node tree.

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
The CCActionSpawn action serves little purpose outside of a sequence. In such a case it would be equivalent to running the spawned actions individually. The spawn action only allows you to more easily test whether all spawned actions have finished or not, though you can achieve the same even more conveniently with a sequence and a call block/selector action at the end.
</td></tr></table>

## Easing Actions

Easing actions wrap an existing action to change the action's progress over time.

![Interpolation Example](../spritebuilder/keyframe-editor-easing-example-animation.gif "Interpolation Mode Example Animation")

To create an easing action you initialize it with an existing action that inherits from `CCActionInterval`:

	id move = [CCActionMoveTo actionWithDuration:4 position:CGPointMake(654, 321)];
	id easeMove = [CCActionEaseInOut actionWithAction:move];
	[node runAction:easeMove];

## More Actions

Please refer to individual action class' references for additional details and code examples.
