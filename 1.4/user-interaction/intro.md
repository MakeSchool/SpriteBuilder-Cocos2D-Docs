# User Interaction

All about user interaction respectively user input:

- touch input events
- keyboard & mouse events for OS X
- hit detection (detect if a node was touched)

The following user interaction methods are not included in Cocos2D. Instead you just use the iOS/OS X/Android framework methods provided to you:

- [Accelerometer input via CoreMotion](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/motion_event_basics/motion_event_basics.html#//apple_ref/doc/uid/TP40009541-CH6-SW4)
- [Gesture Recognizers](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/GestureRecognizer_basics/GestureRecognizer_basics.html#//apple_ref/doc/uid/TP40009541-CH2-SW2) simply need to be added to `[CCDirector sharedDirector].view`
- [MFI Game Controller input](https://developer.apple.com/library/ios/documentation/ServicesDiscovery/Conceptual/GameControllerPG/Introduction/Introduction.html)
- Virtual/OnScreen Joystick - an implementation that's up to date with cocos2d v3.x can be found in [Scott Lembcke's Galactic Guardian project](https://github.com/slembcke/GalacticGuardian.spritebuilder), specifically look in [Controls.m](https://github.com/slembcke/GalacticGuardian.spritebuilder/blob/master/Source/Controls.m) which also showcases switching between MFI Game Controllers and OnScreen Virtual Joysticks.
