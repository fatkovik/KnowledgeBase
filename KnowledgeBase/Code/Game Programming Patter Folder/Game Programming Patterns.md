[[Code Core]]

*This page and its nodes could be used for reference for patterns*

**Introduction**
Author talks about how he started programming when he was a child, the main issue for him was that with large application it always becomes a spaghetti. After landing a job at EA he took a look at code and understood that often all brilliant Code, many people did not go past singleton in terms of architecture and programming patters. 

Sometimes this could be the result of people focusing on the product and not overthinking the architecture, sometimes negligence.

**What is a good software architecture**
For author, good design means that for each change needed for the application, the foundation is already laid and its like the design was done the way to anticipate the change. 
(Davit opinion) Easy of navigation, when design is good, It's not hard to find a right method, check if it already exists, get the needed data where necessary without adding references to weird classes.

**Author suggests testing**
Yeah unit tests and automated tests are good, and in some cases they even saved me multiple times (Davit). But in small scale application where result is important, I don't see a place for tests. Maybe only for some specific part of it. could be.

***What's Decoupling***
When two pieces of code are coupled, it means you cant understand one without understanding the other, If you de-couple them,. you can reason them independently.

Basically
==The goal of software architecture is to minimize the amount of knowledge you need to have in brain before you can make a progress.==

**But good architecture doesn't come free.**
You **HAVE** to maintain it, every piece of new functionality a new code **SHOULD** be integrated gracefully and to rest of program

And Also don't over engineer all the things that you might or might not need later. Interface, abstraction and super decoupling could also harm and introduce lengthy development time and more spaghetti. So it is still about the balance.

There's always pressure to get today's work done today and worry about everything else tomorrow. But if we cram in features as quickly as we can, our codebase will become a mess of hacks, bugs, and inconsistencies that saps our future productivity.

**Few Advices from author.**

- Abstraction and decoupling make evolving your program faster and easier, but don't waste time doing them unless you're confident the code in question needs that flexibility.

- Think about and design for performance throughout your development cycle, but put off the low-level, nitty-gritty optimizations that lock assumptions into your code until as late as possible.

- Move quickly to explore your game's design space, but don't go so fast that you leave a mess behind you. You'll have to live with it, after all.

- If you are going to ditch code, don't waste time making it pretty. Rock stars trash hotel rooms because they know they're going to check out the next day.

- But, most of all, if you want to make something fun, have fun making it.
