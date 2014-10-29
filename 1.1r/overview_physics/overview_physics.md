#Utilizing 2D Physics in Games

Cocos2D comes pre-packaged with the Chipmunk2D physics engine which makes the process of creating physics based games extremely easy.  A physics engine handles aspects of a physics based game like collision detection, gravity, and connecting objects together.  In Cocos2D nodes can be connected to physics bodies which define the collision area for the node as well as properties like denisty and friction that will affect how the node moves.  

Physics bodies are connected together by a component of Cocos2D known as joints.  There are three main types of joint: pivot joints, which provide a single location around which two bodies pivot; distance joints, which define a seperation that two bodies must maintain; and spring joints, which allow two bodies to oscilate in their distance from each other under a spring force.

The Cocos2D engine can also render particle effects which respond to environmental factors like gravity and particle longevity.

SpriteBuilder makes designing physics interactions and particle effects efficient by providing a visual method of connecting bodies together and altering the properties of those bodies involved in an interaction by simply selecting them and changing the properties in the properties panel.

