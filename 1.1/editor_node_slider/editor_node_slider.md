#Working with Sliders
Sliders provide an input method that allows the user to select values anywhere along a continuous range.

As with a button it is possible to set images for the various states of the slider.  Each state (default, highlighted, disabled) uses two images - one for the background bar, and one for the handle that moves along the slider.  It is generally best practice to have these images be similar with slight variance in highlighting/color.  The control should be responsive but not intrusive and should incorporate well with the look of the rest of your game

#Getting the value from a Slider

In order to use the information that the user inputs using the slider a code connection must be setup between the slider and the Xcode project.  This is done using the second tab of the properties panel.  In addition to the standard code connection panel for setting a custom class and instance name for the slider, there is also a CCControl panel which allows a Selector and Target to be specified.

A selector is the name of the method to call once user input has been recieved.  Because of the continuous nature of sliders there are two different ways the selector can be called: continuously or once the input is over.  If the continuous box is selected, the selector method will be called as the slider moves, allowing you to provide instant feedback to the user if they are adjusting a property of an object such as opacity.  If the box is not selected than the selector method will only be called once, once the user stops moving the handle along the bar, providing only the final value that is selected.


For more information about setting up code connections between SpriteBuilder nodes, see [this section](link) of the documentation.