#Videos

###[Effective java, still effective](https://www.youtube.com/watch?v=V1vQf4qyMXg)
* Least astonishment principle: code should not impress you when you read it, if it generates a "ohhhh right" you are probably doing it wrong.
*  When comparing primitive types, be careful not to be comparing the Object references of those things by using `==`, is better to use `.equals()`
*  The wildcards are confusing, remember Swatcheneger PECS, Producer Extends, Consumer Super...
* Don't use wildcards in the return type of a method. It makes it harder to understand what the method returns.
* Explicit type parameter: ugly thing to tell the compiler what's the return type of a method when the compiler cannot figure it out itself.
* Pursue your code to blow up ASAP, better to fail while you are coding than 1 yearl later.
* Really smart people write things like `ConcurrentHashMap` so I don't have to worry about it.
* You should almost always check the return value of putIfAbsent when dealing with concurrency

###[Java puzzles, Google IO](https://www.youtube.com/watch?v=wbp-3BJWsU8)
* Do not use `double` or `float` when exact answer is needed, use BigDecimal instead

###[Dagger 2](https://www.youtube.com/watch?v=oK_XtfXPkqw)

* A class `C` needs instances of X,Y...Z to do its work, and the usual way of doing this is creating those instances in the constructor of `C`. Dependency injection (DI) consists of taking out this task from the constructor and instead pass the instances differently
* The problem with DI is that you need to create code that is aware of the order of which those dependencies are loaded, a bunch of boring work.
* Spring was the first attempt at using DI, it worked pretty well, but it was XML.
* Dagger 2 simply tries to replicate the original solution code written by a human. Plenty of benefits including traceability and Compile time dependency check.

##[Lambdas in Java 8](https://www.youtube.com/watch?v=1OpAgZvYXLQ)

* Lambdas in Java 8 where implemented using the feature invokedynamic, the result of this is no need of creating a .class files per each of the lambdas
* Lambda implementation helps removing unnecessary code (using the :: notation you can create a lambda function that simply passes the argument to a function X), e.g:

		List<Integers> numbers = Array.asList(1,2,3,4,5);
		for (Integer i : numbers) {
			System.out.println(i);
		}
		//
		numbers.forEach(System.out::println);
* Method references are only useful when you are just passing the argument, you cannot do any kind of logic.
* You can use N arguments, and use one of the arguments as a `target` (if the argument is an instance you can call methods from the instance to the rest of the arguments).

		(a,b) -> a.myMethod(b)
		// same as
		SuperclassOfA::myMethod

* lambdas and stream() allows you to use pipelines instead of imperative code (for loops
* write your line in a way that is simple, does one thing only, easy to read.
* You can use `parallelStream()` to paralellize the composite function, OMG.
* Be careful though, use parallelStream() only when you can say "I dont mind spending a lot/all of resources just to get the results faster"... remember the searching for phone analogy.
* The pipeline is built in a lazy way, so what it does it nests the set of functions that you want to perform and applies them to each one of the elements in order, it does not do this to all of the elements in the input.
* The laziness is smart enough to not execute the pipeline if theres no "final pipeline" function
* inmutability brings no side effect, which brings laziness, which brings infinite streams
* I love streams

##[Core Design Principles for Software Developers by Venkat Subramaniam](https://www.youtube.com/watch?v=llGgO74uXMI#t=21.768723)

* A design is good when is easy to change. A good way to test it is to try to apply changes along the way and see the how it feels
* A good design is almost impossible to have the first time we design it, it goes against the way we as humans create good stuff (paints, )
* Good quality software requires time and iterations.
* let go of the ego, be unemotional. You have to be attached to solving the problem, not the solution.
* "Im glad i didnt give you the answer, what you have done is way better than what I have in mind "
* the definition of simplicity, kind of tricky:
	* if something is simple, it keeps your focus 	* it solves the problem we know about, if you don't know about a problem, wait for it to appear to spend time writing code for it.
	* fails less/fails fast
*kind of complexities:
	*inherent: comes from the problem itself
	*accidental: we made it up while trying to solve the problem
*when making a design think about this:
	* is my solution really worth it (where the cost is the amount of accidental complexity added), or can I find a better solution that has a lower cost?... e,g: concurrency.
	*What problem am I really trying to solve
* Simple != Familiar:
	* Easier to understand
	* Familiar you have seen it a lot, e.g: your parents in law :-).
* We have to go beyond the solutions we are familiar with, other solutions might unknown to us but easier to understand.
* "You Are Not Gonna Need it Yet": 
	* don't solve a problem that you don't have at the moment.
	* dont't solve something until you really get value from doing it.
* When should I implement something:
	* How much do you know (you know more tomorrow than today)
	* Cost of implementing it now: if cost(now) > cost(later), then do it later!
	* if cost(now) < cost(later), how probable is that you need it?
* When implementing a solution, aim for an MVP, it helps you get knowledge that you can use later for making a better version, continue this iteration process until the solution is good enough.
* Don't rush into writing more code!
* The example of the Ikea table, You have to aim in putting multiple loose things together instead of having a perfect section (tight) code (that later on you cannot change easily when needed.)
* Anecdote of using SQLite3 as DB while the application was developed, and decided which DB to use just before delivery. Since the application had growth and change during the development, knowledge about the tool was later used to decide what DB to use.
* Postpone is good, but it depends on good automated test 
* Making decisions way to early (not taking advantage of the learning curve) will come back to bite your ass.
* cohesion: things that feel should go together, would go together.
* decoupling classes means no dependencies, which means need to do mocking... go for decoupling!
* types of coupling:
	* tight: depends on a class
	* loose: depends on a interface
* going together with the microservices idea, if you have a class that "does this AND ...", you should consider splitting.
* at [this time](https://youtu.be/llGgO74uXMI?t=3918) it creates a nice list on why long methods are bad.
* The question is not how many lines does a method has, is about what is the level of abstraction of the method. Single Level of Abstraction Principle (SLAP).
* A good practice is to not name methods on creating, use instead the name of the function as a comment that describes its behavior.
* Comments inline are used to cover up bad code, in those cases refactoring is needed.
* Don't comment what, comment why, why is this code necessary?
* Sometimes we don't even want to open file with our existing code, so aim for an application that allows you to add features by creating new modules without modifying the existing ones.
* Inheritance should be used only for subtitutions, Overuse of inheritance is a thing, key concepts:
	* if an object of B should be use anywhere an object of A is used the use inheritance 
	* if an object of B should use an object of A, the use composition/delegation.
* Don't try to bring inheritance where it doesn't belong!!
* A derived class should not ask for more than the base class, and it should offer no less than the base class.
* Collection of derived does not extends from collection of base, example of Book extends TechBook.
* Dependency Inversion principle: Do not make classes depend on each other, use an interface instead, eg: the clock and the alarm anecdote.

##[Time series databases](https://www.youtube.com/watch?v=SgD3RD2Shg4)

* 

