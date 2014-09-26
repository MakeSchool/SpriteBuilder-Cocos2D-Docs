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

##CCEffectStacks

Effect Stacks allow developers to combine multiple effects.

##See Also

- [Introduction to CCEffects in Cocos2D 3.2](https://www.makegameswith.us/gamernews/402/cocos2d-32-with-cceffects-is-coming)
