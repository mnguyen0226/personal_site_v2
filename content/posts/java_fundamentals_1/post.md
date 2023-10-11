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

<p style="color: #286EE0"><strong>[v.0.1] (08/15/2023):</strong> Post started!</p>

## Object-Oriented Concepts

### Terminologies
**Method**: Stores the program statements what perform the task.

**Class**: A proggram unit to store the set of methods that perform the class's tasks.

**Object**: An instance of the class.

**Reuse:** Of existing classes when building new classes and programs saves time and effort. Also, it helps you build more reliable and effective systems, as the existing classes and components often have undergone extensive testing, debugging, and performance tuning.

**Method call:** Each message is implemented as a method call that tells a method of the object to perform its task.

**Encapsulate:** Classes (and their objects) encapsulate their attributes and methods. Objects may communicate with one another, but they are normally not allowed to know how other objects are implemented (details can be hidden within the object themselves). The practice of "information hiding" is crucial to good software engineering.

**Inherirance:** The new class (i.e. subclass) starts with the characteristics of an existing class (i.e. superclass), possibly customizing them and adding unique characteristrics of its own.

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

## Classes, Objects, & Methods

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
    Fig. X: Grand Canyon National Park, Arizona, U.S.A </br>(Image Source: 
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