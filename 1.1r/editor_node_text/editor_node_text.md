#Working with Text Fields
Text Fields allow you to gather textual input from users and then respond to it using a callback.  It is a subclass of CCControl, so it will recognize when the user touches the field and open up the iOS keyboard to recieve their input.  Once the return key is pressed the keyboard will be dismissed and if a selector callback is defined in the second panel of the properties menu it will be called, allowing you to programmatically respond to user input.

#Properties of Text Field

The Sprite frame defines the image that will be used to fill the CCController's size.  SpriteBuilder has a default text box that can be used for inputs, or you can create your own image in another application with the dimensions of the CCControl that is consistent with the style of the rest of your game.

Padding is for all sides, therefore depending on the size of the box and the font size, if the padding is set to high it will cover the text.  Finding a balance between these size properties is key to ensuring that the text box works well with the rest of the layout.