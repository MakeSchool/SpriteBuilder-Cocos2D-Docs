# Working with CCTiledMap

Cocos2D supports tilemaps loaded from a TMX file via CCTiledMap and related classes. This article explains how to use tilemaps. For limitations of the implementation see [CCTiledMap Limitations](./tilemaps/cctiledmap-limitations).

## Editing TMX Tilemaps

To use CCTiledMap you must create a tilemap in the TMX format. The most popular TMX editor (but not the only one) is [Tiled](http://mapeditor.org), hence the class name. iPad users may want to try [iTileMaps](https://itunes.apple.com/app/itilemaps/id432784227).

### Use only supported Formats and Orientations

CCTiledMap will only load *Base64* (compressed or uncompressed) TMX formats and handles only orthogonal and regular isometric tilemaps. Staggered isometric and hexagonal tilemaps are not supported.

See [CCTiledMap Limitations](./tilemaps/cctiledmap-limitations) for a comprehensive list of limitations.

### Add TMX and Tilesets to Xcode

You will need to add both the TMX file and the tileset images it uses to your app's Xcode project.

## Creating a CCTiledMap

Assuming you have a valid TMX file and the tileset images it uses added to your Xcode project, you can load the tilemap using CCTiledMap as follows:

	// Objective-C
    CCTiledMap* tiledMap = [CCTiledMap tiledMapWithFile:@"orthogonal-test1.tmx"];
    [self addChild:tiledMap];
    
    // Swift
    let tiledMap = CCTiledMap(file: "iso-test-vertexz.tmx")
    addChild(tiledMap)

### Understanding the CCTiledMap's position

The tilemap has its anchorPoint set to 0,0 which means the lower left corner of the tilemap begins where the tilemap's position is at, with the tilemap extending to the right and up.

For isometric tilemaps specifically this can mean that the initial tilemap might only show the empty area in the lower left part of the map's rhombus shape unless you change the tilemap's position.

This means if you want to translate the tilemap to the left and down, for instance to move closer to the center of the tilemap, you have to subtract that amount from the tilemap's position. In other words, a position of -100,-100 would move the map 100 points to the left and down.

This can make for seemingly complex calculations. For instance, the following code demonstrates how to find the center location of a tilemap in points, and then changing the map's position so that its center is centered on the screen.

    // Objective-C
    CGSize viewSize = [CCDirector sharedDirector].viewSize;
    CGSize mapPointSize = CGSizeMake(tiledMap.mapSize.width * tiledMap.tileSize.width,
                                     tiledMap.mapSize.height * tiledMap.tileSize.height);
    tiledMap.position = CGPointMake(-mapPointSize.width / 2.0 + viewSize.width / 2.0,
                                    -mapPointSize.height / 2.0 + viewSize.height / 2.0);

	// Swift
    let viewSize = CCDirector.sharedDirector().viewSize()
    let mapPointSize = CGSize(width: tiledMap.mapSize.width * tiledMap.tileSize.width,
                              height: tiledMap.mapSize.height * tiledMap.tileSize.height);
    tiledMap.position = CGPoint(x: -mapPointSize.width / 2.0 + viewSize.width / 2.0,
                                y: -mapPointSize.height / 2.0 + viewSize.height / 2.0);

First, the map size in points needs to be calculated. You could do that once and store the result in a property because you're probably going to need that often.

The position is then calculated by dividing the map's point size by two, and then adding half the view's size to the result in order to move the tilemap to the center. Remember that the tilemap's anchor is in the lower left corner, so without adding half the view size you would actually center the tilemap on the lower left corner of the screen.

The resulting value is also negated just by adding the leading minus sign. After all you want the map to move towards the left and down, which moves the tilemap's position in the negative coordinate space.

### Adding Child Nodes to CCTiledMap

You can add any node as child to a CCTiledMap. But there are a few things to consider:

- If layers are supposed to move at different speeds and certain nodes should move along with specific layers, it is best to add those nodes as children to the specific layer. That way the node's position will automatically be relative to the layer's position.
- Same for draw order: child nodes added to the CCTiledMap node default to be drawn over the tile layers. If you want added nodes to be drawn somewhere in between tile layers it is best to add those nodes to the desired tile layer node. This is a lot easier than adjusting the zOrder property of all child nodes, including the tile layer nodes' zOrder.
- If you do change the CCTiledMap's position you can't add stationary nodes (ie GUI, HUD, etc) to the CCTiledMap itself since they will move along with it. To fix this, add the stationary nodes to the same parent as the CCTiledMap, and add them after the CCTiledMap so they default to be drawn on top of the tilemap.

## Accessing Tile Layers

To obtain a reference to a layer you use the CCTiledMap's `layerNamed:` method to obtain a reference to the given layer:

	// Objective-C
    CCTiledMapLayer* tileLayer = [tiledMap layerNamed:@"Layer 0"];
    NSLog(@"layer tileset image: %@", tileLayer.tileset.sourceImage);

	// Swift
    let tileLayer = tiledMap.layerNamed("Layer 0")
    NSLog("layer tileset image: %@", tileLayer.tileset.sourceImage)

In this example the layer logs the name of the tileset's source image.

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
Avoid calling `layerNamed:` frequently as it is rather expensive, it performs both isKindOfClass and isEqualToString on every child node until a match was found. Instead get the layers you need once upon startup, then assign the references to variables in a class property or ivar for future use.
</td></tr></table>

### Understanding the Layer's position

You can apply the same position magic for the tilemap to individual layer nodes as well. For instance if you wanted to scroll each layer individually, you can do so by using the tilemap position code but applying it to several layers, perhaps with different scrolling speeds to create a parallax effect.

However, do keep in mind that the layer nodes are children of the tilemap node, therefore their positions are relative to the map's position! If you want to move the layers, it is probably best to move only the layer nodes while leaving the tilemap's position unchanged at 0,0 at all times. 

Otherwise you would have to account for the tilemap's position in any code that changes a layer node's position, which will increase the complexity and potential for errors in such code.

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
Either move the CCTiledMap's position, or the position of one or more layers. Avoid changing the position of both tilemap and layer nodes.
</td></tr></table>

### Understanding Tile Coordinates

In a tilemap you can access a given tile using tile coordinates rather than points. A tile coordinate is always an integer value in the range `0` to `layerSize - 1`. 

A tile coordinate multiplied with tileSize (mapTileSize) gives you the point coordinates of a tile. To be precise, the lower left corner of the tile.

Tile coordinates have their origin (0,0) in the upper left corner of the tilemap, with positive X coordinates extending to the right, and positive Y coordinates extending downwards. This is the same coordinate system as Cocoa uses, and differs from Cocos2D's lower-left corner coordinate system where positive Y coordinate extend upwards. Thus when converting between point/pixel and tile coordinates you have to properly invert the Y coordinate.

The reason for this coordinate system is that Tiled traditionally uses it. So if you highlight a tile in Tiled, write down its coordinates, and then access the tile in code using the coordianted from Tiled you will get the correct tile.

### Getting & Setting Tiles using GIDs

If you have a CCTiledMapLayer reference you can get and change the layer's tiles. Following example code illustrates getting a tile GID (global unique identifier, ie a unique number used to identify a specific tile in all loaded tilesets), changing a tile by setting a different GID at a certain tile coordinate, and lastly two removing a tile which is identical to setting its tile GID to 0.

	// Objective-C
    uint32_t tileGID = [tileLayer tileGIDAt:CGPointMake(7, 7)];
    [tileLayer setTileGID:tileGID + 1 at:CGPointMake(7, 7)];

    [tileLayer removeTileAt:CGPointMake(6, 7)];
    [tileLayer setTileGID:0 at:CGPointMake(6, 7)];

	// Swift
    let tileGID = tileLayer.tileGIDAt(CGPoint(x: 7, y: 7))
    tileLayer.setTileGID(tileGID + 1, at: CGPoint(x: 7, y: 7))
        
    tileLayer.removeTileAt(CGPoint(x: 6, y: 7))
    tileLayer.setTileGID(0, at:CGPoint(x: 6, y: 7))

A few things of note:

- Using coordinates that are out of the bounds of the layer's coordinates (0,0 to layerSize) is a programmer's error and will result in an assertion.
- A tile GID that's out of bounds will be assumed as 0, thus removing the tile. If you suddenly have "holes" in your map and use the `setTileGID:at:` method you're most likely using GIDs that are out of bounds.
- A GID is unique across all loaded tilesets. If you have 5 tilesets, each containing 4x4 = 16 tiles then the first tileset's GIDs will be in the range 1-16, the second tileset's GIDs will be in the range 17-32 and so on with the highest valid GID being 5x16 = 80. 
- GIDs are assigned to every possible tile slot in a tileset, whether that tile has actual graphics or is fully transparent does not matter. If you need frequent programmatic access to tiles it is best to design the order of tiles in tilesets to best suit your needs.
- Tile GID 0 is reserved for the "empty tile" (no tile).
- The first GID of a tileset is recorded in [CCTiledMapTilesetInfo](http://cocos2d.spritebuilder.com/docs/api/Classes/CCTiledMapTilesetInfo.html) which you can access via the [tileset property of CCTiledMapLayer](http://www.cocos2d-swift.org/docs/api/Classes/CCTiledMapLayer.html#//api/name/tileset). The last GID of a tileset is the next tileset's firstGid minus one, or you have to calculate it yourself using the properties in CCTiledMapTilesetInfo or you can just define it if you have a fixed number of tilesets with fixed sizes.

<table border="0"><tr><td width="48px" bgcolor="#ffd0d0"><strong>Caution</strong></td><td bgcolor="#ffd0d0">
When removing or reordering tilesets the GIDs can change. Depending on the editor used, this could even happen when adding tiles. If this happens frequently you may want to design a mapping from "tileset name" + "local GID" to actual GID by using the firstGid property of CCTiledMapTilesetInfo to map from "local GID" to GID and vice versa.
</td></tr></table>

## Accessing Object Layers and Objects

In CCTiledMap object layers aren't actual layers (they aren't nodes). Objects are also not drawn to the screen.

The CCTiledMap instance provides access to all object groups (where "group" is synonymous with "layer") via the objectGroups array which contains one [CCTiledMapObjectGroup](http://cocos2d.spritebuilder.com/docs/api/Classes/CCTiledMapObjectGroup.html) for each Object Layer in the tilemap.

The CCTiledMapObjectGroup class provides you with the `objectNamed:` method to get an object by its name, provided a name was given to the object. Note that like layerNamed: this method enumerates all objects and performs isEqualToString on the object's name property, thus making it unsuitable for frequent (runtime) use.

Instead you should enumerate over all objects as the game starts, and convert them as needed into custom data objects or nodes. Following code sample illustrates how to enumerate all objects of the map's first object layer.

	// Objective-C
    CCTiledMapObjectGroup* objectGroup = tiledMap.objectGroups.firstObject;
    for (NSMutableDictionary* objectDict in objectGroup.objects) {
        NSLog(@"object data: %@", objectDict);
    }

	// Swift
    let objectGroup : CCTiledMapObjectGroup = tiledMap.objectGroups.firstObject as CCTiledMapObjectGroup
    for objectDict in objectGroup.objects {
        NSLog("object data: %@", objectDict.description)
    }

Each object is actually a NSMutableDictionary with key/value pairs as they appear in the TMX file. So the objects essentially represent "raw data". Following is an example output of the above code fragment using an object layer with a rect, polygon and tile object:

	object data: {
    	height = "101.25";
	    width = "75.75";
    	x = 656;
	    y = 628;
	}
	object data: {
    	polygonPoints = "0,0 126.25,162 0,101.25 101,20.25";
	    x = 808;
    	y = 709;
	}
	object data: {
    	gid = 37;
	    x = 732;
    	y = 527;
	}

## Accessing Properties

Most Tilemap objects can have properties, which are simply key value pairs where the key is always a string and the value is either a number or a string. 

Following is a list of objects and their class names where you will find a `properties` property of type NSMutableDictionary to access each object's tilemap properties:

- Map (CCTiledMap, CCTiledMapInfo)
- Tile Layers (CCTiledMapLayer, CCTiledMapLayerInfo)
- Object Layers (CCTiledMapObjectGroup)
- Tileset (CCTiledMapTilesetInfo)
- Tiles (CCTiledMap via [propertiesForGID:](http://cocos2d.spritebuilder.com/docs/api/Classes/CCTiledMap.html#//api/name/propertiesForGID:))

As with layerNamed: and objectNamed: before there's usually a corresponding propertyNamed: method. Access via propertyNamed: is fast since it's just a NSDicationary key lookup.

However the propertiesForGID: method does add some overhead because the GID is wrapped in NSNumber first. If you frequently need to access tile GIDs it is recommended to cache the returned dictionary objects.

You can enumerate properties as follows, here using the CCTiledMap's properties but the same principle applies to all properties dictionaries:

	// Objective-C
    for (NSString* propertyKey in tiledMap.properties) {
        NSLog(@"property: %@ = %@", propertyKey, tiledMap.properties[propertyKey]);
    }

	// Swift
    for (propertyKey, propertyValue) in tiledMap.properties {
        NSLog("property: %@ = %@", propertyKey as NSString, propertyValue as NSString)
    }

Example output:	

	property: test = 1234
	property: test2 = this is a string
	
Both property keys and values are NSString objects. If a number value is expected you will have to convert it first, for instance using NSString's built-in [intValue](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSString_Class/index.html#//apple_ref/occ/instp/NSString/intValue) method. It is best to avoid doing so frequently at runtime, if needed, cache values locally.


