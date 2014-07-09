Chaining timelines together causes one timeline to begin as soon as the previous timeline ends  SpriteBuilder makes chaining timelines simple using a dropdown menu at he bottom of the timeline.

![image](chain_timeline.png)

#####
Is there equivelent of timeline animations in Cocos2D/is there a way to initiate timelines in code
######


##Infinite Animations
Timeline chaining provides a simple method for creating animations that loop infinitely.  By chaining a timeline to itself the animation will start over everytime it reaches the end of the timeline, thereby creating an infinite loop.  Additionally, if you want a delay between each time the animation plays, simply extend the duration of the animation past the point where motion ends, and the animation will loop through the entire duration, creating the apperance of a delay.

For an example of how to use infinite animations in a game, take a look at the Peeved Penguins tutorial (link)