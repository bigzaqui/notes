# Effective Java 2nd edition
## Chapter 2

* **Item 1**: Instead of using the constructor of an object, create a Factory function that returns the initialized instance, benefits:
   * Give names to the constructor(s)
   * multiple constructors without having to declare multiple constructors with the same arguments but in different order (super hack)
   * allows to implement the flightway pattern (avoid constructing repeated objects), for example when using casting.
   * allows you to return subtypes of the class, hiding the constructor and allowing you to play with what the factory returns.
   * Take into consideration, a class declared with no accessible constructor cannot be subtyped, forcing you to use composition [(item 16)](#item16)
   
* **Item 2**: use builders, they simulate named optional parameters, makes a class with multiple variables easier to write, and to read.
   * You can add checkers or semantic logic to the builder setters (e,g: check that the parameters make sense), this way you keep the Class that you are building clean of the logic, easier to read! 
   * `varargs` is Java's response to **kwargs in Python. The notation is `...` in the method signature
   * TIL about `Abstract factory pattern`:  is a pattern that allows you to use Factories without referencing concrete classes but instead using an input like a String to define what class to instanciate, letting you to bend the strongly typed nature of Java. You can do something in similar in python:   
   ```python
		exec("foo= {class}()".format(class="Bar"))
    ```
* **Item 3**: Singletons, a class that can only have one instance.
  * multiple ways of doing this, the simplest is using enum

* **Item 4**: Damn Java and its "A class for everything", if you need a class to be the container of multiple static methods and want to prohibit the instantiation of such class, use a private constructor.
*  **Item 5**: 
   * TIL of the "class constructor", notation `static {}` inside a class. Runs when the Class is loaded in the JVM, useful to initialize costly instances that we will use multiple times, e.g API towards another app.
   * This item makes an argument against lazy initialization.
   * On the topic of creating vs reusing objects: "failing to make defensive copies where required can lead to insidious bugs and security holes; creting objects unnecessarily merely affects style and performance.", so as a general rule, don't feel the need to have smart code that reutilizes instances.
*  **Item 6**: Avoid memory leaks, if you are playing with an Array, remember to nullify the keys that are no longer important
*  **Item 7**: 
	*  Dont use finalizers due to the fact that you cannot guarantee that a finalizer is executed when needed.
	* A good practice is to define a custom terminate() method on the class and call it together with a try&finally block. 
	* Customize the finalize() of your class with a WARNING logging in case this method is executed after the custom terminate() has been called.
	* if you are a class and need to have a finalize(), you can avoid the need of having your subclasses calling your finalize (super().finalize()) using a `finalizer guardian`.
	
## Chapter 3
* **Item 8**: If you want to override the equals() from Object, read this Item.
* **item 9**: follow up of above's Item, dont forget to override hashCode()
* **Item 10**: 
	* Always override the `toString()` method, it will make your class more pleasant to use.
	* the `toString()` method returns by default the class name followed by an “at” sign (@) and the unsigned hexadeci- mal representation of the hash code 
* **Item 11**: implementing `Clone()` is complicated, read this Item for guidance. 
* **Item 12**: if possible, implement the `Comparable` interface on your classes, it will make your class work with plenty of other classes and algorithms that depend on it

## Chapter 14
* **Item 13**:
   * A well-designed module hides all of its implementation details, cleanly separating its API from its implementation.
   * Make each class as innaccesible as possible, just as in security, only allow the necessary privileges for the module to work, this helps you expose only the API of your module, hiding the implementation details.
   * If you have a private package top level class used only by another class, consider making it instead a nested private class inside the class that is using it, this reduces the unnecessary acces from other classes inside this package.
   * the `default` privilege mode means `package-private`, this means accessible from any class inside the package it was declared.
   * be careful of defining final fields as `public` if they reference to a mutable object, this allows access to the internals of the class by modifying the object being referenced.
   * applying these restrictions allow you to modify the internals of the class without worring about compatiblity issues, once of your class members is public, you are forced to maintain it.
* **Item 15**:
   * If possible, try to create inmutable classes, they are easier to design, implement and use than mutable classes. 
   * The problem with inmutable classes is that they might create new instances when called a method that makes a change in the instance, this might affect performance.
   * for creating an inmutable class you have to declare it as final or you can use a private constuctor with a static factory
   * Classes should be immutable unless there’s a very good reason to make them mutable
   * having a `reuse` or `reinitialize` method often gains little or no performance benefits to the cost of added complexity. Keep it stateless stupid. 
* **[Item 16 & 17](id:item16)**: 
   * Working with inheritance is recommended only when you control the superclass and the subclasses, inter package inheritance is not a good idea.
   * Your subclasses are closely dependent of the superclass of which they inherit, so the versions of the code of the subclass are linked to a specific release of the superclass, even if you dont want it to be.
   * a safer approach when using inheritance is to only add custom methods and avoid overriding.
   * when deciding to use inherintance or not, if B is not an A, but needs some of the methods of A, have an instance of A be part of the private fields of B and use the methods internally instead of inheritance.
   * If you want to have a class that is safe to inherit, be sure to make explicit in the documentation those methods that cannot be overwritten.
* **Item 18**:
   * Interfaces are nicer than abstract classes, let's use more of those.
   * Interfaces provide flexibility by allowing you to have multiple interfaces being extended by a class (eg: Singer and SongWriter into SingerAndWriter).
   * Abstract Classes + Interfaces = Abstract Interfaces, by defining an abstract class with a `skeletal implementation` of the interface, you get the best of the two worlds. [nice explanation](https://10kloc.wordpress.com/2012/12/03/abstract-interfaces-the-mystery-revealed/)
   * Once an interface is released and widely implemented, it is almost impossible to change, if you add a new method, previous classes that implement the interface will no longer compile.
* **Item 19**:
  * When a class implements an interface it allows us to know what can we do with the class, that should be the only purpose of the interfaces
  * A bad example of using interfaces is having an interface that only defines constants... bad bad coder. Use `Enum` or a `utility class`
* **Item 20**:
  * `tagged class` is the name of a class that tries to do what could be easily done with inheritance, avoid them, use inheritance instead.
* **Item 21**:
  * The strategy pattern: allows you to change inside behaviour of your instance, [link](http://stackoverflow.com/questions/91932/how-does-the-strategy-pattern-work)
  * Java doesn't allow you to reference methods by pointing to them, thats when strattegy pattern can be useful, eg in Python:

```python
def me():
   pass
x = me
x()
``` 
* **Item 22**: 
  * Defines the 4 kind of sub classes in Java: static, non static, anonymous and local.
  * When defining a inner class, push them to be static if possible, will make life easier by not having a reference to a specific instance of the class.

## Chapter 5
* **Item 23**: 
  * Don't use Raw types without specifying the Class they use (eg: use `Iterator<String>` instead of `Iterator`), this also goes when using Iterator, no need of using casting. remember the reader friendly loop syntax.  

* **Item 24**:
  * Eliminate or Suppress (when you are sure the code is type safe) warnings related to type check, don't ignore them, they will bite you in the ass.  
  * When suppressing warnings, leave a comment mentioning why is it safe to do so.
* **Item 25**:
  * Use Lists instead of Arrays when possible, your code is more flexible, and enforces element types at compile time 
* **Item 26**: Use Generics for all the things!
* **Item 28**:
  * Using bounded wildcard brings you the flexibility that parametrized types don't have (due to the fact of being invariant) by the definition of `producers` and `consumers`
  * `Iterable<? extends E>` and `Collection<? super E>` as examples
  * tl;dr: "PECS" (short for Producer extends and Consumer super) is from the collection's point of view. If you are only pulling items from a generic collection, it is a producer and you should use extends; if you are only stuffing items in, it is a consumer and you should use super. If you do both with the same collection, you shouldn't use either extends or super. ([link](http://stackoverflow.com/questions/2723397/what-is-pecs-producer-extends-consumer-super))
* **Item 29**:
  * Given a class T, I can do T.cast(), the name of this is `dinamically casts`
  * Fun example of using classes as the key of a HashMap.

## Chapter 6
* **Item 31**: Enums are there for a purpose, use them!, also when you need to find the size of an enum, do not use the `ordinal()` method.
* **Item 36**: use annotations when possible, specially the `@override`

## Chapter 7
* **Item 38**:
  * Do validation of parameters ASAP, helps debugging and avoids the execution of lines that will end up in a failure 
  * Validation can be costly, one alternative is to rely in implicit validation (done by the logic of a method) than doing a "manual" validation
  * `exception translation idiom`: see item 61.
* **Item 39**:
  * When dealing with mutable parameters (object references) as parameters for a class method/constructor, make copies of the objects and use those copies instead the original parameters, removing the possiblity of the API's user of playing with the referenced objects later on... same when using getters, return copies, not the reference to the internal object.
  * Order: Make copies, perform a validity check, continue with the code's execution.
* **Item 40**: Rules to follow when creating a method: naming convention, length of parameters, convenience methods..
* **Item 41**:
  * Overloading: multiple methods with the same name but different parameter list, Java decides which one to run at compile time based on the parameter list
  * Overriding: same method defined in a class and in the subclasses that inherit from that class, Java decides which one to run at runtime base on the most specific.
  * Avoid using overloading, it gets confusing.
  * One case where is OK to use overloading is when the 2 methods have the same effect, eg: 

```python
def lookup(id=None):
   .get(id)
def lookup(name=None):
   .search(name=name)
``` 

* **Item 42**:
  * when using `varargs`, use 1 or more parameters 
  * `varargs` should be used with respect, use it only when is clear that the benefits of having are worth the usage.
* **Item 43**:
  * Do not return `null`, forces the client to do extra verifications  
  
## Chapter 8
* **Item 45**: You can do this!
```java 
   for (int i = 0, n = expensiveComputation(); i < n; i++) {       doSomething(i);}
``` 



  
#   QUESTION?
when you have List<?>
  
   
#Things learned on the way
* Mixin is a way in Java 8 to allow multiple inheritance via interfaces, this is done by using method implementation on the interface declarations. [link](http://hannesdorfmann.com/android/java-mixins)
* Generics are confusing, [here's the bible for them](http://www.angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html)
* Use Lists instead of Arrays
* [Steps for optimizing](http://stackoverflow.com/a/716645/1044704):
  * Don't optimize until you have a nice, clean, and working version of your code. Changing to generic types could very well be motivated at this step already.
  * When you have a version that is nice and clean, decide if it is fast enough.
  * If it isn't fast enough, measure its performance. This step is important for two reasons. If you don't measure you won't (1) know the impact of any optimizations you make and (2) know where to optimize.
  * Optimize the hottest part of your code.
  * Measure again. This is just as important as measuring before. If the optimization didn't improve things, revert it. Remember, the code without the optimization was clean, nice, and working. 


##Pending
 * full read the generics FAQ
   
# Video notes
* **Part 1**:
  * be careful of mutability and sharing: Java is cool due to the explicit type, some frameworks allow you to play with this as long as you know what you are doing (python style) but this could create trouble if the code is gonna be shared with others... Keep focused on having standard code.
  * throwing nullPointException? from the code?, YES! is the same as Exceptions in Python, is just the idiom 
  * You want your methods to completely suceed or completely fail
  * you should do all the checks before starting to do the mutations in your variables
  * Java has evolved in a way of doing the same things in a simpler way and not focusing in offering completely new alternatives/ways of doing the same thing... 
  * if you are gonna go with a builder, go early.