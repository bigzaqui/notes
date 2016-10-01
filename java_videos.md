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

