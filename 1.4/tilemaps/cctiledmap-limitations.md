# CCTiledMap Limitations

The CCTiledMap class has a number of limitations that you need to be aware of.

## Unsupported TMX map formats
- CSV and XML formats are not supported
	- Workaround: use a Base64 (compressed or uncompressed) format
		
## Unsupported TMX map types
- Hexagonal
- Staggered Isometric (Isometric map whose shape is a rectangle rather than a diamond/rhombus shape)
	
## Unsupported TMX features
- Image Layers
- Layer Opacity
- Properties are immutable (ie NSNumber instances)
- Object Rendering (including tile objects)
- Terrain features
- Tile Animations
- Tile Collision Information
- Tile Render Order
	
## Other Limitations
- Only one tileset image allowed for each tile layer.
	- Workaround: create & edit multiple layers, one for each tileset. Leave tiles "empty" as needed.
- There is no SpriteBuilder support for CCTiledMap yet.
- Tileset images must be manually added to the Xcode project at the correct location. 
	- Meaning: If the image is referenced in the TMX file with a relative path, this relative path must be added as a folder reference so that the path also exists in the app bundle. For ease of use it is recommended to store tileset images alongside the TMX file in the same folder or in a subfolder therein.

## Changes from previous versions

In Cocos2D v1 and v2 the tilemap classes had features that are now unavailable or changed significantly.

- Tiles can not be converted to sprites anymore
	- This improves rendering performance and memory usage. Converting a tile to CCSprite meant the tile remained in memory as a CCSprite, which has about a tenfold higher memory usage than a "raw" tile (ie 64 bytes compared to ~500 bytes for a sprite).
