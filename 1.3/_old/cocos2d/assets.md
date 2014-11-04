#Assets in Cocos2D

When using Cocos2D without SpriteBuilder assets are not autosized. Instead developers need to provide assets in different resolutions. By default Cocos2D uses filename suffixes to identify the assets in the different resoutions. The relevant suffixes are:

- **no suffix** - default iPhone assets
- `-hd` (iPhone retina assets)
- `-iphone5hd` (iPhone 5 retina assets)
- `-ipad` (iPad assets)
- `-ipadhd` (iPad retina assets)

Example filename using suffix:

	hero-ipad.png
	
##Expert options
`CCFileUtils` is the class that takes care of finding resources in the correct resolution. By default it uses the `CCFileUtilsSearchModeSuffix` described above. A second available option is the `CCFileUtilsSearchModeDirectory` that uses sub directories for different resolutions (SpriteBuilder uses this option). Most developers will not have to change the settings of `CCFileUtils`.
