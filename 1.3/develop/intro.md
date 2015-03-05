# Developer Reference

This section contains references and guides for experienced users who want to work with and ultimately modify the SpriteBuilder and Cocos2D source code.

Some of these articles assume that you are familiar working with git/github and source control in general.

## Table of Contents

- [Custom Drawing in v3](./develop/custom-rendering) provides an example on how to override the CCNode `draw:transform:` method and writing custom rendering code using the CCRenderer API introduced in Cocos2D v3. Also shows how to properly enclose regular OpenGL code in a render queue block.
- [Creating Node Plugins](./develop/plugin-node) details how to create a SpriteBuilder node plugin to add editing support for as yet unsupported or custom node types.
- [Creating Export Plugins](./develop/plugin-export) explains the basics of writing a SpriteBuilder export plugin, in case you need a different format than the built-in CCB(i) files. Consequently you would have to write your own reader class, more or less analog to CCBReader.
- [CCB File Format](./develop/file-format-ccb) is a reference of the CCB file structure, which is essentially just an XML file. This article may not be up to date with the latest SpriteBuilder version.
- [CCBi File Format](./develop/file-format-ccbi) details the structure of the binary CCBi files created from the original CCB file during the publish process. This article may not be up to date with the latest SpriteBuilder version.
