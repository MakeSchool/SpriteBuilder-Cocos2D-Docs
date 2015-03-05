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
- Object Rendering
- Terrain features
- Tile Animations
- Tile Collision Information
- Tile/Object Render Order

## Other Limitations
- Only one tileset image per tile layer.
	- Workaround: create & edit multiple layers, one for each tileset. Leave tiles "empty" as needed.
- Tiles can not be converted to sprites anymore (as in Cocos2D v1/v2).
	- This improves rendering performance and memory usage. See [this forum thread for details](http://forum.cocos2d-swift.org/t/v3-1-beta-tilemaps-tileat-function/13298). In essence, converting any tile to CCSprite increased the tile's memory footprint roughly tenfold.
