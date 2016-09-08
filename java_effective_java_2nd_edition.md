# Effective Java 2nd edition
## Chapter 1

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
# Video notes
* **Part 1**:
  * be careful of mutability and sharing: Java is cool due to the explicit type, some frameworks allow you to play with this as long as you know what you are doing (python style) but this could create trouble if the code is gonna be shared with others... Keep focused on having standard code.
  * throwing nullPointException? from the code?, YES! is the same as Exceptions in Python, is just the idiom 
  * You want your methods to completely suceed or completely fail
  * you should do all the checks before starting to do the mutations in your variables
  * Java has evolved in a way of doing the same things in a simpler way and not focusing in offering completely new alternatives/ways of doing the same thing... 
  * if you are gonna go with a builder, go early.