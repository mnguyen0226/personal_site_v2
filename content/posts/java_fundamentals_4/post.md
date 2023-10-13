---
author: "Minh T. Nguyen"
title: "Java Fundamentals (Part 4)"
date: "2023-10-02"
description: "Notes on linked lists."
tags: ["java"]
categories: ["software engineer"]
series: ["Software Engineering"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (10/2/2023):</strong> Post started (On-going)!</p>

## Linked Lists

In the [previous post](https://mnguyen0226.github.io/posts/java_fundamentals_2/post/), we learnt that List can be implemented in ArrayLists or LinkedLists and they both behave in the same way. **So why choose one over the other?**

Although the functional behaviours of ArrayLists and LinkedLists are the same, their performance behaviours are different. If we need to access or update a value, ArrayLists is a to-go choice, but if we anticipate to insert or delete value in the middle of the array, we should choose LinkedLists.

<center>
    <img style="width: 80%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_4/imgs/ll_vs_arr.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: LinkedList vs ArrayList.
</figcaption>
<br/>

Let's look at the example of List implemented using ArrayList
```java
/**
 * A dynamic array implementation of the List interface.
 *
 * @param <E> the type of elements in this list
 */
public class ArrayList<E> implements List<E> {
    private E[] elements;
    private int size;
    private int capacity;

    /**
     * Constructs an empty list with an initial capacity of ten.
     */
    public ArrayList(){
        size = 0;
        capacity = 10;
        elements = (E[]) new Object[capacity];
    }

    /**
     * Appends the specified element to the end of this list.
     *
     * @param e element to be appended to this list
     */
    public void add(E e){
        if(size == capacity){
            ensureCapacity();
        }
        elements[size++] = e;
    }

    /**
     * Returns the element at the specified position in this list.
     *
     * @param index index of the element to return
     * @return the element at the specified position
     * @throws IndexOutOfBoundsException if the index is out of range
     */
    public E get(int index){
        if(index < 0 || index >= size){
            throw new IndexOutOfBoundsException();
        }
        return elements[index];
    }

    /**
     * Removes the element at the specified position in this list.
     *
     * @param index the index of the element to be removed
     * @return the element previously at the specified position
     * @throws IndexOutOfBoundsException if the index is out of range
     */
    public E remove(int index){
        if(index < 0 || index >= size){
            throw new IndexOutOfBoundsException();
        }
        E removedElement = elements[index];
        for(int i=index; i<size-1; i++){
            elements[i] = elements[i+1];
        }
        size--;
        return removedElement;
    }

    /**
     * Returns the number of elements in this list.
     *
     * @return the number of elements in this list
     */
    public int size(){
        return size;
    }

    /**
     * Increases the capacity of the array if necessary to ensure that it can hold at least the number of elements specified by the minimum capacity argument.
     */
    private void ensureCapacity(){
        int newCapacity = capacity * 2;
        E[] newElements = (E[]) new Object[newCapacity];
        for(int i=0; i<size; i++){
            newElements[i] = elements[i];
        }
        elements = newElements;
        capacity = newCapacity;
    }
}
```
<br/>

Let's look at the example of List implemented using LinkedList
```java
/**
 * A doubly-linked list implementation.
 *
 * @param <E> the type of elements in this list
 */
public class LinkedList<E>{
    private static class Node<E> {
        E element;
        Node<E> next;
        Node<E> previous;

        Node(E element, Node<E> next, Node<E> previous){
            this.element = element;
            this.next = next;
            this.previous = previous;
        }
    }

    private Node<E> header;
    private int size = 0;

    /**
     * Constructs an empty list.
     */
    public LinkedList(){
        header = new Node<E>(null, null, null);
        header.next = header;
        header.previous = header;
    }

    /**
     * Appends the specified element to the end of this list.
     *
     * @param e element to be appended to this list
     */
    public void add(E e){
        Node<E> newNode = new Node<>(e, header, header.previous);
        header.previous.next = newNode;
        header.previous = newNode;
        size++;
    }

    /**
     * Returns the element at the specified position in this list.
     *
     * @param index index of the element to return
     * @return the element at the specified position
     * @throws IndexOutOfBoundsException if the index is out of range
     */
    public E get(int index){
        if(index < 0 || index >= size){
            throw new IndexOutOfBoundsException();
        }
        Node<E> current = header.next;
        for(int i=0; i<index; i++){
            current = current.next;
        }
        return current.element;
    }

    /**
     * Removes the element at the specified position in this list.
     *
     * @param index the index of the element to be removed
     * @return the element previously at the specified position
     * @throws IndexOutOfBoundsException if the index is out of range
     */
    public E remove(int index){
        if(index < 0 || index >= size){
            throw new IndexOutOfBoundsException();
        }
        Node<E> current = header.next;
        for(int i=0; i<index; i++){
            current = current.next;
        }
        current.previous.next = current.next;
        current.next.previous = current.previous;
        size--;
        return current.element;
    }

    /**
     * Returns the number of elements in this list.
     *
     * @return the number of elements in this list
     */
    public int size(){
        return size;
    }
}
```



## Citation
Cited as:

<blockquote>
    <summary>Nguyen, Minh. (October 2023). Java Fundamentals (Part 4).</summary>
    <summary>https://mnguyen0226.github.io/posts/java_fundamentals_4/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mtl,
  title   = "Java Fundamentals (Part 4).",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "October",
  url     = "https://mnguyen0226.github.io/posts/java_fundamentals_4/post/"
}
```

## References
[1] P. Deitel, Java: How To Program, Early Objects: Pearson, 2017

[2] Horstmann, Cay S. Big Java: Early Objects. John Wiley & Sons, 2020.

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_4/imgs/arkansas.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Pinnacle Mountain State Park, Big Rock Township, Arkansas, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/hET8qSGlQg0" class="img_footer">Joshua J. Cotten @ Unsplash</a>).
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