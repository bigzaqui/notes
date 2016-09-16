# Effective Java 2nd edition
## Chapter 2

* **Item 1**: Instead of using the constructor of an object, create a Factory function that returns the initialized instance, benefits:
   * Give names to the constructor(s)
   * multiple constructors without having to do it in a hackish way 
   * allows to implement the flightway pattern (avoid constructing repeated objects), for example when using casting.
   * allows you to return subtypes of the class, hiding the constructor and allowing you to play with the                  
   
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

## CHapter 14
* **Item 13**:
   * A well-designed module hides all of its implementation details, cleanly separating its API from its implementation.
   * Make each class as innaccesible as possible, just as in security, only allow the necessary privileges for the module to work, this helps you expose only the API of your module, hiding the implementation details.
   * If you have a private package top level class used only by another class, consider making it instead a nested private class inside the class that is using it, this reduces the unnecessary acces from other classes inside this package.
   * the `default` privilege mode means `package-private`, this means accessible from any class inside the package it was declared.
   * be careful of defining final fields as `public` if they reference to a mutable object, this allows access to the internals of the class by modifying the object being referenced.
   * applying these restrictions allow you to modify the internals of the class without worring about compatiblity issues, once of your class members is public, you are forced to maintain it.
* **Item 15**:
   * If possible, try to create inmutable classes, they are easier to design, implement and use than utable classes. 
   * The problem with inmutable classes is that they might create new instances when called a method that makes a change in the instance, this might affect performance.
   * for creating an inmutable class you have to declare it as final or you can use a private consturctor with a static factory
   * Classes should be immutable unless there’s a very good reason to make them mutable
   * having a `reuse` or `reinitialize` method often gains little or no performance benefits to the cost of added complexity. Keep it stateless stupid. 
* **Item 16 & 17**: 
   * Working with inheritance is recommended only when you control the superclass and the subclasses, inter package inheritance is not a good idea.
   * Your subclasses are closely dependent of the superclass of which they inherit, so the versions of the code of the subclass are linked to a specific release of the superclass, even if you dont want it to be.
   * a safer approach when using inheritance is to only add custom methods and avoid overriding.
   * when deciding to use inherintance or not, if B is not an A, but needs some of the methods of A, have an instance of A be part of the private fields of B and use the methods internally instead of inheritance.
   * If you want to have a class that is safe to inherit, be sure to make explicit in the documentation those methods that cannot be overwritten.
* **Item 18**:

#Things learned on the way
* Mixin is a way in Java 8 to allow multiple inheritance via interfaces, this is done by using method implementation on the interface declarations. [link](http://hannesdorfmann.com/android/java-mixins)

   
# Video notes
* **Part 1**:
  * be careful of mutability and sharing: Java is cool due to the explicit type, some frameworks allow you to play with this as long as you know what you are doing (python style) but this could create trouble if the code is gonna be shared with others... Keep focused on having standard code.
  * throwing nullPointException? from the code?, YES! is the same as Exceptions in Python, is just the idiom 
  * You want your methods to completely suceed or completely fail
  * you should do all the checks before starting to do the mutations in your variables
  * Java has evolved in a way of doing the same things in a simpler way and not focusing in offering completely new alternatives/ways of doing the same thing... 
  * if you are gonna go with a builder, go early.