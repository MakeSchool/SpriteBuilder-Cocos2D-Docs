
#Joints

Joints are used to connect physics bodies with each other.  SpriteBuilder 1.1 introduces the ability to create joints visually.

##Initializing Joints

SpriteBuilder has three types of joints available in the Node Library:
- `Physics Pivot Joints:` This joint provides a point at which two bodies connect and around which they can pivot
- `Physics Distance Joint:` Links two bodies together and keeps them at a fixed distance
- `Physics Spring Joint:` Links two bodies together elastically

To make a connection between two bodies simply drag the appropriate node from the node library onto the stage.  Next, connect the bodies to the joint by clicking on one of the two circles below the joint and dragging a connection between it and the body on the stage.

![image](connect.gif)

Note: In order to make a connection between two bodies they must both be the child of a CCPhysicsNode and they must both have physics enabled.

##Properties of All Joints:

Although each joint type is used under different circumstances, there are certain properties that they all have in common.

![image](generalProperties.png)

- `Body A & Body B:`  Specify the elements that the joint links together.  These fields are automatically filled in when connections are made as shown in initializing joints.  Clicking the X will detach the joint from that body.

- `Collide bodies:` If this box is checked the connected bodies will not be able to pass through each other

![image](noCollide.gif)
![image](collide.gif)

- `Anchor A & Anchor B:` Specify the coordinates on the physics bodies at which the joint is connected.  Moving the joint on screen will update these fields automatically.  If one of the bodies is static and the other is dynamic, the static body should be attached as body A, and the dynamic body should be body B.

- `Breaking Force:` It is possible to specify a force under the stress of which a joint will “break” allowing the two physics bodies to separate.  By default this is set to infinity so the joint will never break.

- `Maximum Force:`  This sets the maximum “push back” that the joint will provide.  Unlike the breaking force, the joint will still exist if this force is exceeded, however it will bend or deform appropriately.