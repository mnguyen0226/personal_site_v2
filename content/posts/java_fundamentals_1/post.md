---
author: "Minh T. Nguyen"
title: "Java Fundamentals (Part 1)"
date: "2023-08-21"
description: "Object-oriented concepts, classes, objects, methods in Java programming."
tags: ["java", "oop"]
categories: ["software engineer"]
series: ["Software Engineering"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 3
---

<p style="color: #286EE0"><strong>[v.1.0] (08/15/2023):</strong> Post published!</p>

## Object-Oriented Concepts

### Terminologies
**Method**: Stores the program statements what perform the task.

**Class**: A proggram unit to store the set of methods that perform the class's tasks.

**Object**: An instance of the class.

**Reuse:** Of existing classes when building new classes and programs saves time and effort. Also, it helps you build more reliable and effective systems, as the existing classes and components often have undergone extensive testing, debugging, and performance tuning.

**Method call:** Each message is implemented as a method call that tells a method of the object to perform its task.

**Encapsulate:** Classes (and their objects) encapsulate their attributes and methods. Objects may communicate with one another, but they are normally not allowed to know how other objects are implemented (details can be hidden within the object themselves). The practice of "information hiding" is crucial to good software engineering.

**Inheritance:** The new class (i.e. subclass) starts with the characteristics of an existing class (i.e. superclass), possibly customizing them and adding unique characteristrics of its own.

**Interfaces**: Collections of related methods that typically enable you to tell objects what to do, but not how to do it. Note, a class "implements" zero or more interfaces, each of which can have one or more methods.

**Unified Modeling Language (UML):** The most widely used graphical scheme for modeling object-oriented systems.

**Java application**: Is a computer program that executes when you use the java command to launch the Java Virtual Machine (JVM).

**Java Programming:** Is simple, safe, platform independent, rich library, designed for internet. Here is the comparison between C/C++ vs Java programming.

</br>
<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_1/imgs/c_program.png" />
      <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_1/imgs/java_program.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: C/C++ vs Java programming.
</figcaption>
</br>

**Downside to JVM:** As you have something in between your bytecode and CPU, the application is slower and less efficient (the disadvantage is mostly not notificable)

### Operating Systems (OS)

**OS:** Are software systems that make using computers more convenient for users, application developers, and systems administrators. They provide services that allow each application to execute safely, efficiently, and concurrently.

**Kernel:** Is the software that contains the core components of the operating system.

## Java Programming

### Types & Variables
**Type:** Defines a set of valeus and the operations that can be carried out on those values. There are 2 types in Java
- Primitive types: simple values. Examples: `int`, `short`, `long`, `float`, `double`, `boolean`, `byte`, `char`.
- Reference types: objects. Examples: `String`, `Interger`, `Array`, `List`, `HashSet`, `Rectangle`, `FileReader`,...

**Variable:** A name for a value that you want to use at a later time.

### Classes, Objects, & Methods

Rectangle is a class in package java.awt. Let's implement a simplified version in a package called simplified.geometry. 

Every public class, field, constructor, and method should be documented with appropriate Javadoc comments and tags.

```java
/**
 * Represents a rectangle defined by a set of x, y coordinates and dimensions (width and height).

 * The class provides basic operations such as translation and resizing, and it also includes
 * methods for querying the rectangle's position and dimensions.
 * 
 * @author Minh Nguyen
 * @version 1.0
 */
package simplified.geometry;

public class Rectangle {

    /** The x-coordinate of the rectangle's top-left corner. */
    private int x;

    /** The y-coordinate of the rectangle's top-left corner. */
    private int y;

    /** The width of the rectangle. */
    private int width;

    /** The height of the rectangle. */
    private int height;

    /**
     * Creates a new rectangle with coordinates (0,0) and dimensions (0,0).
     */
    public Rectangle() {
        this(0, 0, 0, 0);
    }

    /**
     * Creates a new rectangle with specified coordinates and dimensions.
     *
     * @param x The x-coordinate of the rectangle's top-left corner.
     * @param y The y-coordinate of the rectangle's top-left corner.
     * @param width The width of the rectangle.
     * @param height The height of the rectangle.
     */
    public Rectangle(int x, int y, int width, int height){
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }

    /**
     * Returns the x-coordinate of the rectangle's top-left corner.
     * 
     * @return The x-coordinate.
     */
    public int getX(){
        return x;
    }

    /**
     * Returns the y-coordinate of the rectangle's top-left corner.
     * 
     * @return The y-coordinate.
     */
    public int getY(){
        return y;
    }

    /**
     * Returns the width of the rectangle.
     * 
     * @return The width.
     */
    public int getWidth(){
        return width;
    }

    /**
     * Returns the height of the rectangle.
     * 
     * @return The height.
     */
    public int getHeight(){
        return height;
    }

    /**
     * Sets the size of the rectangle to the specified width and height.
     * 
     * @param width The new width of the rectangle.
     * @param height The new height of the rectangle.
     */
    public void setSize(int width, int height){
        this.width = width;
        this.height = height;
    }

    /**
     * Translates the rectangle by the specified amount in the x and y directions.
     * 
     * @param dx The amount to translate in the x-direction.
     * @param dy The amount to translate in the y-direction.
     */
    public void translate(int dx, int dy){
        this.x += dx;
        this.y += dy;
    }

    /**
     * Checks if this rectangle is equal to another rectangle.
     * 
     * @param that The rectangle to compare with.
     * @return true if the two rectangles have the same coordinates and dimensions; false otherwise.
     */
    public boolean equals(Rectangle that){
        return ((this.x == that.x) && 
                (this.y == that.y) && 
                (this.width == that.width) &&
                (this.height == that.height));
    }

    /**
     * Returns a string representation of the rectangle in the format:
     * "Rectangle[x=...,y=...,width=...,height=...]".
     * 
     * @return A string representation of the rectangle.
     */
    @Override
    public String toString() {
        return "Rectangle[x=" + x + 
                        ",y=" + y +
                        ",width=" + width + 
                        ",height=" + height + "]";
    }
}
```

### Design & Language Concepts
**Encapsulation:** Direct access to internal state should always be prohibited (by declaring them as private).

**Constructor:** Defines the initial values of the fields for a newly-created object.

**Accessors:** return artifacts of the current state of the object.

**Mutators:** allows potential modification of the current state, and may return useful values.

**Object Life Cycle:** 
- Objects are constructed (via the `new` operator) as instances of a class.
  - The constructor (a special method with no return type) is called to initialize the fields. The name of the constructor is the name of the class
  - The `new` operator returns the address of the newly-created object. This address acts as a "reference" (a pointer, in other languages) to the object
- Objects can then be accessed and/or mutated by their public methods
  - Method calls are always requests; we ask the object to do something on our behalf. Accessors ask objects to return current state information. Mutators ask objects to make changes (which may be refused or altered)
  - The state fields, and internal operations of each method, are hidden from other objects. Ensures the implementation can change without ripple effects throughout the system
- Objects cannot be deleted explicitly, but they can become unreachable
  - Unreachable: no in-scope variable, nor reachable object's field, references the object
  - Once unreachable, an object becomes immediately eligible for garbage collection. The system eventually reclaims the memory of any unreachable objects. Modern garbage collection is an extremely efficient automatic background service.

## Citation
Cited as:

<blockquote>
    <summary>Nguyen, Minh. (August 2023). Java Fundamentals (Part 1).</summary>
    <summary>https://mnguyen0226.github.io/posts/java_fundamentals_1/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mtl,
  title   = "Java Fundamentals (Part 1).",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "August",
  url     = "https://mnguyen0226.github.io/posts/java_fundamentals_1/post/"
}
```

## References
[1] P.Deitel, Java: How To Program, Early Objects: Pearson, 2017

[2] Horstmann, Cay S. Big Java: Early Objects. John Wiley & Sons, 2020.

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_1/imgs/arizona_grand_canyon.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Grand Canyon National Park, Arizona, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/dS3UnDX6InQ" class="img_footer">Jason Thompson @ Unsplash</a>).
</figcaption>

<!-- CSS Styling -->
<style>
.img_size {
  width: 100%;
}

.img_footer {
    color: #888888;
    text-align: center;
}
</style>