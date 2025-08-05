[[Game Programming Patterns]]
Imagine a forest in a video game with thousands of trees, each tree has its own mesh, texture, leaves etc etc.
That's a lot of information to handle every single frame and even more information to send between cpu and gpu each frame with a bus.

So instead of modeling (code object) each tree with a different instance of class, we can do another thing.

There is this key observation that many trees share the same properties, same mesh same texture. Sure some of them may contain it in a different format from each other, but that doesn't change the point.

We continue by splitting the object in half.
Firstly having a class that shares the common stuff, lets call it *TreeModel*. and then having a *Tree* class that contains a reference to that TreeModel class that on its own contains the common items between the tress.
And when passing along data and instantiation trees, for many of them, have a single reference that's being passed around that contains the heavy lifting data.
This pattern looks a lot like a Type Object pattern is purely about efficiency, and having less classes. Any memory benefit we get is just a bonus.
![[treeFlyweightExamplepng.png]]
This all is good for storing stuff in memory, but that doesn't help rendering.

To minimize the amount of data we have to push to GPU, we want to be able to send the shared model, the *TreeModel* just once, Then each of trees unique data, position etc etc. This all is actually very well implemented in modern graphics APIs, they support sharing with GPU two steams of data, one with common attributes and other with list of instances and their parameters that will be used to vary that first chunk of data each time it's drawn.

This patter is the only one in *Gang of Four* that has an actual hardware support.

###### Now with a concrete example, lets head through the general pattern itself.

Flyweight, like its name implies, comes into play when you have objects that need to be more lightweight, generally because there is too many of them.

the pattern solves the issue of getting large data in and out of everywhere by separating it out into two kinds, The stuff that's not specific to single instance, and stuff that's specific and not shareable.

the non specific thing is called *intrinsic state*
and the specifics are called *extrinsic state*

Basically this pattern defines a clever way of resource sharing for efficiency.

Now more clever use and example of this pattern, that is less intuitive which makes it a bit more magical to use.

##### A Place To Put Down Roots
We define a surface of a map, it is tile based, basically a huge grid of tiles, each one covered in one kind of terrain.

Each terrain has a few properties that affect gameplay. 
- A movement cost,
- A flag indicating if its a water terrain
- A Texture.

Because we game programmers are paranoid about efficiency, there’s no way we’d store all of that state in each tile in the world. Instead, a common approach is to use an *enum* for terrain types:
We create a terrain type enum for each of them.

Then a huge 2d array with all the terrain tiles in them.
**Page 40**