# Effective Java 2nd edition
## Chapter 1

* **Item 1**: Instead of using the constructor of an object, create a Factory function that returns the initialized instance, benefits:
   * Give names to the constructor(s)
   * multiple constructors without having to do it in a hack way 
   * allows to implement the flightway pattern (avoid constructing repeated objects)
   * allows you to return subtypes of the class, hiding the constructor and allowing you to play with the                  
   
* **Item 2**: use builders, they simulate named optional parameters, makes a class with multiple variables easier to write, and to read.
   * You can add checkers or semantic logic to the builder setters (e,g: check that the parameters make sense), this way you keep the Class that you are building clean of the logic, easier to read! 
   * `varargs` is Java's response to **kwargs in Python. The notation is `...` in the method signature
   * TIL about `**Abstract factory pattern**`:  is a pattern that allows you to use Factories without referencing concrete classes, letting you to bend the strongly typed nature of Java. Example in python:   
   ```python
		exec("foo= {class}()".format(class="Bar"))
    ```
# Video notes
* **Part 1**:
  * be careful of mutability and sharing: Java is cool due to the explicit type, some frameworks allow you to play with this as long as you know what you are doing (python style) but this could create trouble if the code is gonna be shared with others... Keep focused on having standard code.
  * throwing nullPointException? from the code?, YES! is the same as Exceptions in Python, is just the idiom 
  * You want your methods to completely suceed or completely fail
  * you should do all the checks before starting to do the mutations in your variables
  * Java has evolved in a way of doing the same things in a simpler way and not focusing in offering completely new alternatives/ways of doing the same thing... 
  * if you are gonna go with a builder, go early.