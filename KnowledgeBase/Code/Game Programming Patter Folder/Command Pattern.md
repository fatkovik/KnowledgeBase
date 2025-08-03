[[Game Programming Patterns]]

A Command is a thingified method call.
*Basically a method call wrapped in an object*

##### Concrete examples and pseudo Implementations
One example of command pattern is handling key presses in video game.

Below is a dead simple implementation in a game loop.
![[Pasted image 20250801234151.png]]
This has a lot of issues, s.t. you would not want to press B a lot of time :D
And we lose the possibility to remap the button in game, i mean we can do this in a weird way like store in a dictionary and rebind etc. etc,, But here the command pattern can be used.

To support all the Remapping stuff, we can use the command pattern.
"Swapping out" sound a lot like assigning a variable, so we create an object that we represent a game action with.

**When you have an interface with a single method that doesn’t return anything, there’s a good chance it’s the Command pattern.**

We create class from interface with some command and execute function which handles it.

In ***InputHandler*** class we store references to that commands.

Now in out game loop we just delegate to those commands.
![[ShitInputButNowCommand.png]]

*Notice how we don’t check for NULL here? This assumes each button will have some command wired up to it. If we want to support buttons that do nothing without having to explicitly check for NULL, we can define a command class whose execute() method does nothing. Then, instead of setting a button handler to NULL, we point it to that object. This is a pattern called Null Object.*

For better managing and choosing where and how to execute the command (on what object e.g.)
We can make the Input Handler return a command and handle it inside of the other place where the command is created and once it's executed we can do the action and handle all stuff correctly.

We can even put them all in some sort of list of commands and make an Event Queue which executes all the stuff in sequence.

For more examples of concrete implementation in relation to executing in game commands refer to ***Page 28***

## Undo/Redo

Another great usage of command pattern not only in video games but overall is Undo/Redo 
In the command interface we already created, we can add a new method called Undo or Redo.
So basically how this thing is widely done, each action that can be undone is stored inside of array, and when the time comes, we just call undo command sequentally. This is a very easy explanation of this example.
More on ***Page 32***

It is astonishing when this works, and it look very fkin cool when someone implements it.
I remember Hovo at office did Undo/Redo for out applicaiton and its cool.
There, besically every action done to some let's say dataset is called Unit of Work. Each action is performed through mediatoR it goes to interaction (Interactor is also very cool pattern along with mediator) In Interactor every action is recorded and after that its done, but still saved so even after commiting it we can call the undo action and thats it.


