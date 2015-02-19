# User Interaction

All about user interaction respectively user input:

- Touch events
- Accelerometer & Gyroscope updates via Core Motion
- Keyboard & Mouse events (OS X only)
- Hit Detection/Testing (determine if a touch/click was on a specific node)

The following user interaction methods are not included in Cocos2D. Instead you just use the iOS/OS X/Android framework methods provided to you:

- [Accelerometer input via CoreMotion](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/motion_event_basics/motion_event_basics.html#//apple_ref/doc/uid/TP40009541-CH6-SW4)
- [Gesture Recognizers](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/GestureRecognizer_basics/GestureRecognizer_basics.html#//apple_ref/doc/uid/TP40009541-CH2-SW2) simply need to be added to `[CCDirector sharedDirector].view`. Note that some classes like CCScrollView and CCTableView use UIGestureRecognizers themselves which could be conflicting with your gesture recognizers.
- [MFI Game Controller input](https://developer.apple.com/library/ios/documentation/ServicesDiscovery/Conceptual/GameControllerPG/Introduction/Introduction.html) and *Virtual/OnScreen Joysticks* - An implementation of both for Cocos2D v3.x can be found in [Scott Lembcke's Galactic Guardian project](https://github.com/slembcke/GalacticGuardian.spritebuilder), specifically look in [Controls.m](https://github.com/slembcke/GalacticGuardian.spritebuilder/blob/master/Source/Controls.m) which switches between MFI Game Controllers and OnScreen Virtual Joysticks depending on whether a physical game controller is available.
