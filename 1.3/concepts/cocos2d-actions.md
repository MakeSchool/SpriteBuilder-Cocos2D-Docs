# Cocos2D Actions

Cocos2D Actions are classes that perform a task on the node, typically over time. A very common action is the move action which moves the node in a straight line to the destination point within a given time frame.

Actions are what drive SpriteBuilder's Timeline animation. Every Timeline animation makes use of actions and action sequences under the hood.

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
Sprite Kit's actions behaviors and programming API were very closely modelled after Cocos2D's actions. So for the most part you can read the [Sprite Kit Actions Guide](https://developer.apple.com/library/mac/documentation/GraphicsAnimation/Conceptual/SpriteKit_PG/AddingActionstoSprites/AddingActionstoSprites.html) as if they were talking about Cocos2D to get a high-level grasp of Action concepts. Just remember to return here. :)
</td></tr></table>

## Most Notable Actions

Most Actions fall in either the Instant or Interval category. Rather than discussing the specialized actions that move, scale or rotate actions it's more important to know about the actions with great utility as they are frequently overlooked or misunderstood. They are:

- Instant Actions
	- [CallFunc](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallFunc.html) (aka "perform selector action")
	- [CallBlock](http://www.cocos2d-swift.org/docs/api/Classes/CCActionCallBlock.html) (aka "run block action")
- Interval Actions
	- [Tween](http://www.cocos2d-swift.org/docs/api/Classes/CCActionTween.html)
	- [Delay](http://www.cocos2d-swift.org/docs/api/Classes/CCActionDelay.html) (aka "wait action")
	- [Repeat](file:///depot-koboldkit/cocos2d-iphone/api-docs/html/Classes/CCActionRepeat.html)
- Modifier Actions
	- [RepeatForever](http://www.cocos2d-swift.org/docs/api/Classes/CCActionRepeatForever.html)
	- [Speed](http://www.cocos2d-swift.org/docs/api/Classes/CCActionSpeed.html)
- Combining Actions
	- [Sequence](http://www.cocos2d-swift.org/docs/api/Classes/CCActionSequence.html)
	- [Spawn](http://www.cocos2d-swift.org/docs/api/Classes/CCActionSpawn.html)

## Combining Actions

Running multiple actions via `runAction:` will run those actions in parallel.

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
Two interval actions altering the same node property (ie position) <strong>must not be run in parallel</strong>. A common case being two <i>move</i> actions running at the same time on the same node. The resulting behavior is undefined. Check for such cases if you find action animations freeze, stutter, have timing issues or are not animating to completion.
</td></tr></table>

The **Sequence** action allows you to add multiple actions that run in sequence, one after the other. You can of course run two or more sequences in parallel like regular actions, provided that the interval actions within each sequence can be run in parallel  respectively do not overlap (see *Caution* box above).

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
If your sequence is comprised only of so-called "instant" actions the sequence will run instantly to completion. This will have the same effect as running each action separately, respectively directly setting the node's properties.
</td></tr></table>

The **Spawn** action is used within a sequence to run one or more actions in parallel without interrupting the current action sequence. 

The Spawn action is often misunderstood as the (only) way to run actions in parallel, while in fact you can call runAction: multiple times with different actions to run those actions in parallel. Spawn is only necessary because you couldn't otherwise spawn two or more actions that should run in parallel **in the middle of a sequence**.

The **Repeat** and **RepeatForever** actions take another action as input, and will run that action repeatedly either for a set number of times (Repeat) or indefinitely (RepeatForever). 

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
You can of course use the Spawn, Repeat and RepeatForever actions to spawn or repeat entire action sequences, not just individual actions.
</td></tr></table>

## Executing Code

Both the Perform Selector (**CallFunc**) and Run Block (**CallBlock**) actions perform arbitrary code. They can be added to an action sequence, in order to perform custom code every time the node arrives at given move action's target position for instance. Or as a way to run code at the end of a sequence.

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
The use of Run Block is preferred over Perform Selector for the simple fact that the block has access to all local variables, and thus there's no need to "pass in parameters". Also you can write the block code inline like an anonymous function. [Learn more about blocks here.](https://developer.apple.com/library/ios/documentation/cocoa/Conceptual/Blocks/Articles/00_Introduction.html)
</td></tr></table>

The Perform Selector action can run any selector on the given target, provided the selector takes no parameters and returns no value. If you need parameters, use the CallBlock action.

## Altering Time

There are two ways to alter the duration of an action or sequence.

The **Delay** action enables you to add some delay to a sequence. You can have a node move, then wait, then move again by running a sequence with a move, a delay, and another move action. The delay action simply causes the sequence to do nothing for a given time.

The **Speed** action takes any other interval action as parameter. You then keep a reference to the speed action, preferably as an ivar. Whenever you need to change the speed of the wrapped action you would change the speed property of the speed action. This allows you to create custom easing modes.

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
The speed action can not be added to a sequence.
</td></tr></table>

### Varying Duration for Fixed Speed

To ensure an action animates at the same speed you need to set the duration based on the difference between current and target value and a speed factor. For instance to have move actions move the node at the same speed regardless of distance, you calculate the distance between current and target position and divide it by an arbitrary speed factor of your choosing:

	CGFloat speed = 4.5;
	CGFloat distance = ccpDistance(node.position, targetPosition);
	CGFloat duration = distance / speed;

## When NOT to use Actions

Actions can easily be over- or misused. This section tries to explain areas where actions are unsuitable or can not be used at all.

### Very Short Durations

**Actions are not suitable to run for very short durations.** To understand this it helps to understand the timing behind actions.

Cocos2D updates interval actions at the same rate the screen refreshes, typically 60 frames per second (fps). At 60 fps the minimum duration for an action to complete is `1.0 / 60.0 = 0.0166` seconds. Any duration shorter than this will still run for one frame, because an action's duration is (roughly) a multiple of 0.0166 seconds.

For example, if you specify a duration of 0.02 the action will take two frames to complete and will in fact have an effective duration of 0.0333 seconds at 60 fps. Whether you specify a duration of 0.017 or 0.03 will not have any effect on the duration of the action, it runs for two frames in both cases. This is why you will only see quantized animation changes for actions that run for very short durations or where you alter an action's duration by a value less than 0.0166 seconds.

Now a specific problem surfaces if you replace an action every frame, for instance during the `update:` method but it also applies to code that runs in **touchesMoved**, **accelerometer** and other **input events** that could be or are sent at the same interval as the screen refresh rate.

In such cases there may not be enough time for the action to complete because it is being replaced in the next frame already. The animation may stutter or freeze altogether because **the previous action may not have had a chance to perform its task**. 

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
If a node property changes frequently, and possibly every frame, it's highly recommended and often required to modify the corresponding node property (ie position) directly rather than using an action (ie move). This will also avoid the overhead of creating and deallocating action objects every frame.
</td></tr></table>

### Actions as AI / Gameplay Replacement

Actions are primarily a means to create self-sufficient animations. However in AI or gameplay programming you often need full control over what an actor (typically represented by a node) does in every moment in time. You may often have to change what the actor does, or make decisions based on what the actor currently is doing.

Frequently creating and prematurely stopping actions can be considered a [code smell](http://en.wikipedia.org/wiki/Code_smell) for misusing Actions as gameplay components. It's not something that's specifically bad per se, it always depends on the context - but you should be aware of its potential pitfalls and consequences.

- Creating and stopping actions frequently, possibly hundreds of times per second altogether, can become a performance issue unless you re-use those actions. Likewise if you have many actions running and request them frequently via *getActionByTag* and similar lookup methods.
- Complex game mechanics animated with actions are a source of frequent mistakes, like forgetting to stop certain actions, accidentally running actions in parallel that shouldn't run in parallel, assuming actions run to completion when they might be stopped at any time, or interrupting actions so frequently that they don't animate smoothly. Any of this may cause odd results and can be difficult to debug.
- To keep track of a node's intention (where is it going, and why?) you have to keep this state information up to date seperately from the actions (typically in a node subclass) whenever you run or stop actions. However actions are a public CCNode API, so even other nodes could run or stop actions without modifying the actor's internal state.
- Somewhat exempt from this recommendation are visual-only actions, for instance those running sprite frame animations, fading or colorizing a node. Typically visual glitches are harmless, for instance if you stop or replace a visual action at the wrong time the node may just have the wrong color. But even visual actions may render a node completely invisible, and thus affecting gameplay.

The general recommendation is to avoid extensive use of actions for gameplay logic. Certainly it's easier to run a move action than to integrate a velocity CGPoint every update cycle. But you pay dearly over time as you add more and more actions to perform (interruptible) game logic. 

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
The main purpose of action animations is to play them from start to end (or looping indefinitely) to perform a single, self-sufficient animation. Use actions for gameplay purposes with care and always look for possible alternatives, even if they may require writing more code.
</td></tr></table>

### Move/Rotate Actions conflict with Physics

Physics animates and updates a node's position and rotation properties if it has a non-static CCPhysicsBody. A move or rotate action does the same. Now which one should take precedence if both were running at the same time, updating the same properties?

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
**Do not run move or rotate actions on nodes with dynamic physics bodies.** The resulting behavior is undefined and will most likely not be what you expect.
</td></tr></table>

You can certainly run move and rotate actions on nodes with static or kinematic bodies. But **consider dynamic bodies as exclusively controlled (owned) by physics** as far as the position and rotation properties are concerned.

But the problems don't end here. Consider that you are moving a node with a physics body (dynamic or otherwise) by the use of a move action. If the body being moved were dynamic or kinematic, the move action will have the node ignore any physics collision. But the next time the physics engine updates its internal state, it may try to resolve the collision, countering the movement of the action. 

Ultimately what you may see is that nodes with physics bodies that are animated with move or rotate actions are able to penetrate or pass through collisions or may never reach the action's intended target position or rotation. Or they may simply jitter along the edges of a collision, as the action tries to move the node inside and the physics engine tries to move it back outside again.

