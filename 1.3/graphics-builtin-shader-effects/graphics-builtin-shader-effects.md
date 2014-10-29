#CCEffects

CCEffects is a feature introduced in Cocos2D 3.2 that allows developers to create visual effects without writing custom shaders. Each effect type is represented by a `CCEffect` subclass:

- CCEffectBloom
- CCEffectBrightness
- CCEffectContrast
- CCEffectBlur
- CCEffectGlass
- CCEffectHue
- CCEffectPixellate
- CCEffectReflection
- CCEffectRefraction
- CCEffectSaturation

##Applying CCEffects

There are two different ways to apply CCEffects, either by assigning the effect to the `effect` property of a `CCSprite` or by creating a `CCEffectNode`.

With the first option the effect is only applied to the sprite. By using a `CCEffectNode` an effect can be applied to all the child nodes of that effect node.

Here is a simple example of applying a blur effect to a sprite:

    // pixelation is very simple, you only need to choose a block size
    _spaceship.effect = [CCEffectPixellate effectWithBlockSize: 5];

##CCEffectStacks

Effect Stacks allow developers to combine multiple effects.

    // Effects like changing the contrast and the brightness are one liners.
    CCEffectContrast *contrastEffect = [CCEffectContrast effectWithContrast:0.2];
    _brightnessEffect = [CCEffectBrightness effectWithBrightness:sin(0)];
    
    // A CCEffectStack allows you to combine multiple CCEffects and apply them to a Sprite
    CCEffectStack *effectStack = [[CCEffectStack alloc] initWithEffects:@[contrastEffect, _brightnessEffect]];

##See Also

- [Introduction to CCEffects in Cocos2D 3.2](https://www.makegameswith.us/gamernews/402/cocos2d-32-with-cceffects-is-coming)
