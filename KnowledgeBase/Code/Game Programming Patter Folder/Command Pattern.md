[[Game Programming Patterns]]

A Command is a thingified method call.
*Basically a method call wrapped in an object*

##### Concrete examples and pseudo Implementations
One example of command pattern is handling key presses in video game.

Below is a dead simple implementation in a game loop.
![[Pasted image 20250801234151.png]]
This has a lot of issues, s.t. you would not want to press B a lot of time :D
And we lose the possibility to remap the button in game, i mean we can do this in a weird way like store in a dictionary and rebind etc. etc,, But here the command pattern can be used.