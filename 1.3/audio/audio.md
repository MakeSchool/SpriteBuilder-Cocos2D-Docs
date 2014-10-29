#Audio in Cocos2D

Cocos2D comes bundled with *OALSimpleAudio* a library that provides a simple API for playing sound effects. The relevant features are[ covered by our tutorial](https://www.makegameswith.us/gamernews/355/playing-sounds-in-cocos2d-30).

##Playing a basic sound effect
The `OALSimpleAudio` class provides multiple convinience methods to play sounds. The `sharedInstance` method can be used to access an instance of the class and play a sound:

	// access audio object
	OALSimpleAudio *audio = [OALSimpleAudio sharedInstance];
	// play background sound
	[audio playBg:@"your_file_name" loop:YES];

##See Also

- [Audio Tutorial for Cocos2D 3.0](https://www.makegameswith.us/gamernews/355/playing-sounds-in-cocos2d-30)