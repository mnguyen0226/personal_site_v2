---
author: "Minh T. Nguyen"
title: "Java Fundamentals (Part 2)"
date: "2023-09-11"
description: "Dive into the distinctions and practical uses of static and final modifiers in Java. Discover the intricacies of arrays versus lists, and understand the fundamental differences between interfaces and their implementations."
tags: ["java"]
categories: ["software engineer"]
series: ["Software Engineering"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 8
---

<p style="color: #286EE0"><strong>[v.1.0] (09/11/2023):</strong> Post published!</p>

## Static & Final Modifiers
### Static Members
**Static members** Are shared among all objects of the class (and available without any objects)

**Static Methods:** Are stateless utility operations, intended to be used without any instances. For example, `Math.abs()`, `Character.isDigit()`, `Double.parseDouble()`.

**Static Fields:** As a best practice, these are always decleared in conjection with `final` for storing constant. For example, `Math.PI`, `Integer.MAX_VALUE`, `Integer.MIN_VALUE`.However, some `final` values are not actually constant.

### Final Members
**Final Methods:** Are methods that cannot be inherited.

**Final Fields:** Are fields that are assiged a value exactly once. A static final field is only "constant" if its type is a primitive or an immutable class.

## Array vs. List
### Array
Here are some of the properties of `Array`:
- Provides random access to elements.
- An array is an object.
- Once length is fixed it can't be changed.
- Elements can be objects or primitives.
- Special syntax for access, length.
- Java arrays' lengths are immutable but their contents are mutable.

Let's look at an example of `Array`
```java
String[] arr = new String[10]; // null x 10
String[] arr = {"hello", "world"};
myMethod(new String[]{"hello", "world"});
```

Let's look at an example of `Array` class
```java
String[] arr2 = Arrays.copyOf(arr, arr.length);
String[] arr3 = Arrays.copyOf(arr, arr.length * 2);
Arrays.fill(arr, "");
Arrays.sort(arr);
Arrays.toString(arr);
Arrays.equals(arr1, arr2);
```

### List
Here are some properties of `List`:
- Provides random access to elements.
- A list is an object.
- Can add elements.
- Elements can only be objects.
- No special syntax
- `List` is an interface: this means that we can implement `List` via `ArrayList` or `LinkedList`.

Let's look at an example of `List`:
```java
List<String> s1 = new ArrayList<>();
List<String> s2 = new LinkedList<>();
List<String> s3 = new Arrays.asList("abc", "def"); # not recommend as you cannot add or remove element, you can update values though.
s1.add("abc");
s1.add("abc", 4);
s1.size();
String str = s1.get(4);
String str = s2.remove(4);
```

## Interface vs. Implementation
**Interface:** Gives you everything you need to know to use the component (or answering the question "What does the componenet do?").

Let's look at an example of an `interface`:
```java
public interface List<E> {
    /**
     * Appends the specified element
     * to the end of this list.
     * @param element element to be added
     */
    public void add(E element);

    /**
     * Inserts the specified element
     * at the specified position
     * in this list.
     * @param index location to insert element
     * @param element element to be inserted
     */
    public void add(int index, E element);

    /**
     * Removes all of the elements
     * from this list.
     */
    public void clear();

    /* Others functions for a complete List interface */
    public boolean contains(E element);
    public boolean equals(List<E> that);
    public E get(int index);
    public int indexOf(E element);
    public boolean isEmpty();
    public Iterator<E> iterator();
    public E remove(int index);
    public int size();
}
```

**Implementation:** The behind-the-scenes internal working of the component (or answering the question "How does the component do it?").

To connect with the idea of `List`, a `List` interface can have multiple implementations.

Let's look at an example of an `implements`:
```java
/**
 * A simple generic implementation of an ArrayList.
 * 
 * @param <E> the type of elements in this list
 */
public class ArrayList<E> implements List<E> {

    /**
     * The array buffer into which the elements of the ArrayList are stored.
     */
    private E[] elements;

    /**
     * The current number of elements in the ArrayList.
     */
    private int size;

    /**
     * The total capacity of the ArrayList.
     */
    private int capacity;

    /**
     * Constructs an empty ArrayList with an initial capacity of ten.
     */
    public ArrayList() {
        size = 0;
        capacity = 10;
        elements = (E[]) new Object[capacity];
    }

    /**
     * Inserts the specified element at the specified position in this list. 
     * Shifts the element currently at that position (if any) and any subsequent elements to the right.
     * 
     * @param index index at which the specified element is to be inserted
     * @param element element to be inserted
     * @throws AssertionError if the element is null
     * @throws AssertionError if the index is out of range (index < 0 || index >= size)
     */
    public void add(int index, E element) {
        assert element != null;
        assert 0 <= index && index < size;
        if (size == capacity) {
            capacity *= 2;
            elements = Arrays.copyOf(elements, capacity);
        }
        for (int i = size; i > index; i--) {
            elements[i] = elements[i-1];
        }
        elements[index] = element;
        size++;
    }
}

```

## Citation
Cited as:

<blockquote>
    <summary>Nguyen, Minh. (September 2023). Java Fundamentals (Part 2)</summary>
    <summary>https://mnguyen0226.github.io/posts/java_fundamentals_2/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023java2,
  title   = "Java Fundamentals (Part 2)",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "September",
  url     = "https://mnguyen0226.github.io/posts/java_fundamentals_2/post/"
}
```

## References
[1] P. Deitel, Java: How To Program, Early Objects: Pearson, 2017

[2] Horstmann, Cay S. Big Java: Early Objects. John Wiley & Sons, 2020.

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_2/imgs/alaska.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Birch Lake, Alaska, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/APhlh308DqU" class="img_footer">Alain Bonnardeaux @ Unsplash</a>).
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