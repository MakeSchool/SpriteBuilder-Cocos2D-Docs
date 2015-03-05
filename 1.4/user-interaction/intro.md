# User Interaction

All about user interaction respectively user input:

- [Touch Events](./user-interaction/touch-events) shows how to enable receiving touch events and how to process touch events in code.
- [Core Motion](./user-interaction/core-motion-integration) shows how to create and use a Core Motion instance to receive accelerometer or gyroscope events in a Cocos2D app. In addition, accelerometer filtering and the accelerometer's coordinate system are explained.
- [OS X Input Events](./user-interaction/osx-input-events) explains by example how to implement OS X Keyboard & Mouse events, how to detect double-clicks, how to correctly recognize keys based on their key code, and how to simulate a continuous keypress.
- [Hit Detection](./user-interaction/hit-detection) helps you determine if a touch/click was on a specific node using rect intersection tests, a distance/radius test and hints at further reading regarding other hit testing algorithms.

The following user interaction articles are external links that you might find useful:

- [Accelerometer input via CoreMotion](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/motion_event_basics/motion_event_basics.html#//apple_ref/doc/uid/TP40009541-CH6-SW4) on Apple's iOS Event Handling Guide.
- [Gesture Recognizers](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/GestureRecognizer_basics/GestureRecognizer_basics.html#//apple_ref/doc/uid/TP40009541-CH2-SW2) simply need to be added to `[CCDirector sharedDirector].view`. Note that some classes like CCScrollView and CCTableView use UIGestureRecognizers themselves which could be conflicting with your gesture recognizers.
- [MFI Game Controller input](https://developer.apple.com/library/ios/documentation/ServicesDiscovery/Conceptual/GameControllerPG/Introduction/Introduction.html) and *Virtual/OnScreen Joysticks* - An implementation of both for Cocos2D v3.x can be found in [Scott Lembcke's Galactic Guardian project](https://github.com/slembcke/GalacticGuardian.spritebuilder), specifically look in [Controls.m](https://github.com/slembcke/GalacticGuardian.spritebuilder/blob/master/Source/Controls.m) which switches between MFI Game Controllers and OnScreen Virtual Joysticks depending on whether a physical game controller is available.
