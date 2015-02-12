# Audio Programming with ObjectAL

Cocos2D and SpriteBuilder come bundled with the [ObjectAL audio engine](http://kstenerud.github.io/ObjectAL-for-iPhone/). It is essentially a clever wrapper around AVAudioPlayer and OpenAL that leaves the time-critical sound effect playback to OpenAL while streaming audio is (typically) played through AVAudioPlayer (if available).

The essential ObjectAL classes are documented in the [Cocos2D Class Reference](http://www.cocos2d-swift.org/docs/api), they all carry the `OAL` prefix. The [complete ObjectAL documentation](http://kstenerud.github.io/ObjectAL-for-iPhone/documentation/index.html) includes an introduction and guide with several code examples.

Apportable has specially modified ObjectAL to also work (well) on Android with OGG audio files.

## "Simple" Audio

Like the CocosDenshion audio engine before it that ObjectAL superseded, ObjectAL provides a *simple* audio interface in the form of the singleton class `OALSimpleAudio`. It is sufficient for most uses and can be combined with more advanced concepts.

### Referencing Audio Files

In order to play back audio files, you have to specify the relative path to the audio file as well as its original file extension.

For instance, if the audio file's name is `game-music.wav` in SpriteBuilder and it resides in the *Audio* folder in SpriteBuilder, you would need to write `Audio/game-music.wav` where a path to an audio file is required by ObjectAL.

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
Do not use the audio file's published file extension, ie `.m4a` or `.ogg`, but the file extension of the file as you see it in SpriteBuilder. By using the file extension of the audio file as it appears in SpriteBuilder you guarantee that the correct file will be played on all platforms and regardless of the audio format (in case you decide to change it).
</td></tr></table>


### Playing Music

To play a music track, or more precisely playing a streaming audio file with AVAudioPlayer, you will use the playBg method:

**Objective-C:**

	[[OALSimpleAudio sharedInstance] playBg:@"Audio/game-music.wav" loop:YES];

**Swift:**

	OALSimpleAudio.sharedInstance().playBg("Audio/game-music.wav", loop:true)

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
Only a single background (music) track can be played/preloaded at a time with OALSimpleAudio.
</td></tr></table>

### Playing Sound Effects

