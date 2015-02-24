#Working with Text in SpriteBuilder
SpriteBuilder provides two options for rendering text on the screen - Label TTF and Label BM-Font.  TTF stands for true type font, and BM stands for Bitmap Font.  A TTF is rendered using fonts built into the platform that is rendering the text, while a BM font uses an external file that specifes the bitmaps for each letter to render.  Each type has its advantages and uses, which will be explored below.

Labels also have the ability to support localization.  To enable localization simply select the localize box in the properties panel.  For more information on localization, see the advanced section on [localization](link)

#Label TTF
TTF fonts rely on the fonts built into the platform.  These built in fonts have a large number of editable properties which allow you to customize the look of the text using font apperance and font effects.  Some of the key propreties that can be set are:

-Font name/size: Select the base font to use for the text, and set the size of the font.  Note that when you drag the edges of the box on the screen it adjusts the scale, not the font size.  The box will automatically re-size to fit the text, and the font size should be changed directly to avoid blurring the text

-Font Color/Opacity: Set the color and visibility of the font.

-Font Outline: Specify the color, opacity and width of the outline for the letters.

-Font Shadow: Set the color, blur radius and offset for a shadow effect cast by the font.


#Label BM-Font
Cocos2D can render bitmap fonts created using external editor.  After creating a new BM-Font, specify the font file in the properties panel.  The label text can also be set in the properties panel, and the text can be changed programatically using a code connection.  Since each character is rendered as a seperate Sprite, the text can be more efficiently rendered than a LabelTTF when ferquent changes occur, and individual letters can be programatically accessed through the child property of the Label BM-Font.

For more information on Cocos2D's font rendering see [the official API](http://cocos2d.spritebuilder.com/docs/api/Classes/CCLabelBMFont.html)