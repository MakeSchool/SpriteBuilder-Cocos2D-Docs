# Physics

SpriteBuilder and Cocos2D use the [Chipmunk2D physics engine](https://chipmunk-physics.net/). The Cocos2D integration provides an Objective-C programming interface while SpriteBuilder offers visual editing of physics shapes and joints, and their properties.

You will learn how to add physics to your game in this section.

## Table of Contents

- [Working with Physics Bodies](./physics/editing-physics) is the SpriteBuilder physics editing guide that explains the relationship between Physics Node and Physics Bodies and how to edit a physics body's collision shape with best practices.
- [Editing Body Properties](./physics/editing-body-properties) explains a physics body's properties in detail, lists nodes which shouldn't have physics enabled, and how to use the collision type, category and mask. *Note*: Though this article uses SpriteBuilder it contains information that's also useful for developers not using SpriteBuilder.
- [Editing Physics Joint](./physics/editing-joints) shows how to create and edit physics joints in SpriteBuilder, illustrating the different kinds of joints and their specific properties.
- [Programming Physics](./physics/physics-programming) delves into the programming interface of the Chipmunk2D physics engine with many code examples: debug drawing, creating physics bodies with one or multiple shapes, making joint connections, enumerating and removing joints, and last but not least collision callback methods and collision categories and masks.
- [Simulation Stabilits](./physics/simulation-stability) is an abstract paper with tips on how to improve physics simulation stability or at least to prevent joint connections from "exploding".