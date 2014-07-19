
Cocos2D comes with a large number of options 

#Chaining Actions Together
 
 Cocos2D has a class called CCActionSequence which allows you to string together CCActionFiniteTimes to be played one after another.  This allows extended animation sequences to be designed and saved in a single CCAction and then applied to any node.  CCActionSequences works with recursivly defined sequences, stringing together sequences of sequences.

#Running Actions in Parallel

In order to create CCActionSpawn will execute two actions in parallel, allowing a sprite to rotate and move position at the same time for instance.


Using these two classes together provides access to the full power of CCActions and For more information