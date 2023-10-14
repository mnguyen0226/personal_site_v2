---
author: "Minh T. Nguyen"
title: "Java Fundamentals (Part 3)"
date: "2023-09-25"
description: "A brief introduction on test-driven development (TDD)."
tags: ["java", "tdd"]
categories: ["software engineer"]
series: ["Software Engineering"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (09/25/2023):</strong> Post published!</p>

## Test-Driven Development
### Types Of Tests
In software development, there are different ways to test softwares:
- **Beta testing:** Provides a finished or near-finished application to a group of users and sees what problems they come up with.
- **Performance testing:** Uses profiling tools to measure if we are getting acceptable response time. Is this application running as fast as it should be or it need to be?
- **Stress testing:** A type of performance testing. We want to know how well the application runs under heavy loads.
- **Integration testing:** Test one app's integration-ability to another app.
- **Unit Testing:** Tests individual components to ensure they work as intended.
- **Functional Testing:** Confirms the application operates according to specifications and requirements.
- **System Testing:** Tests a fully integrated system for adherence to specified requirements.
- **Regression Testing:** Verifies that recent changes don't adversely affect existing functionalities.
- **Acceptance Testing:** Determines if the software meets specified requirements. User Acceptance Testing (UAT) is a focused subset where end-users assess real-world application scenarios.
- **Security Testing:** Evaluates the software's defense against threats, pinpointing potential vulnerabilities.
- **Compatibility Testing:** Checks if the software functions across different devices, browsers, and operating systems.
- **Usability Testing:** Assesses the software's user-friendliness and gathers user feedback.
- **Exploratory Testing:** Unscheduled testing where testers actively explore and concurrently design and conduct tests.
- **Smoke Testing:** Initial testing to detect major failures and ascertain the software's stability for more detailed testing.
- **Sanity Testing:** Examines specific functions affected by recent changes, a kind of focused regression testing.
- **Monkey Testing:** Random testing without knowledge of system internals, functionalities, or data.
- **Alpha Testing:** In-house testing done before releasing the software to a select external audience.
- etc...

Here, we focus on testing individual units of our code! We test our code as we write it, and we write code to automate the testing of our code.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_3/imgs/paradox_of_test.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Paradox of (test) choices. Which tests to select to capture bugs?
</figcaption>
<br/>

### TDD In A Nutshell

**TDD is about writing the test prior to writing the application logic.**

Counter-intuitive? Having the need to pass 1 test gives us clarity on what is needed to be done.

**Steps:**
- 1. Write a test.
- 2. Watch the test fail.
- 3. Write application logic - as simple as possible.
- 4. Pass the test.
- 5. Refactor, removing duplication

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_3/imgs/unit_testing.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Unit-test </br>(Image Source: 
    <a href="https://www.monkeyuser.com/2022/unit-tests/" class="img_footer">monkeyuser.com</a>).
</figcaption>
<br/>

### Questions & Answers
Question 1: "Does TDD work for everything?"
- *No. There are problems that having TDD by itself does not guarantee the code is perfect, such as problems related to multi-threading, security, or user interfaces. Unit-testing does not replace other testing methods.*

Question 2: "Am I supposed to write all my tests first?"
- *No. It's an iterative process where you write the test, expect to fail, develop the method, then move on to write the next test.*

## Unit Testing Frameworks
There are some unit-testing frameworks, such as: JUnit (Java), NUnit (.NET), PyUnit (Python), CppUnit (C++) or OCUnit (Objective-C). Although there are different frameworks, they all have the same idea.

### JUnit For Unit Testing & Test-Driven Development
Unit tests are ultimately the best way to capture class-level and method-level requirements. Once the tests match the requirements, code can be developed to pass the tests. Unit tests aren't the only kinds of tests; many other kinds are generally required as well

JUnit is by far the most common way to formally write unit tests for Java code. There are many advantages to the formal approach of JUnit:
- Fully integrated into all major Java IDEs to create and run tests without external tools.
- A robust library supports easily writing tests, to encourage quantity and quality of tests.
- Tests can be run – and evaluated – automatically.
- Coverage can be tracked, to ensure that every line of source code has been tested.

Let's look at the example. Note that the test is written prior to the code.
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class CalculatorTest {

    @Test
    public void testAddition() {
        Calculator calculator = new Calculator();
        int result = calculator.add(5, 3);
        assertEquals(8, result);
    }
}
```

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

JUnit provides several assertion methods to make it easy to specify expected behavior.

### Questions & Answers
Question 1: "Do I test getters and setters?"
- *Depends. Test only if they could meaningfully break.*

Question 2: "Do I test private methods"
- *Generally, no. Typically, just make a test for a public method that proves the private method works.*

Question 3: "Can I combine multiple test classes?"
- *Yes, it is called "Test Suites".*

Question 4: "How do I control the order of tests?"
- *No. Controlling order suggests dependencies - avoid at all costs.*
- *Unit tests are not intended to test the application - only the individual units of code, in isolation.*


## Citation
Cited as:

<blockquote>
    <summary>Nguyen, Minh. (September 2023). Java Fundamentals (Part 3).</summary>
    <summary>https://mnguyen0226.github.io/posts/java_fundamentals_3/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mtl,
  title   = "Java Fundamentals (Part 3).",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "September",
  url     = "https://mnguyen0226.github.io/posts/java_fundamentals_3/post/"
}
```

## References
[1] P. Deitel, Java: How To Program, Early Objects: Pearson, 2017

[2] Horstmann, Cay S. Big Java: Early Objects. John Wiley & Sons, 2020.

[3] S. Allardice, Test-Driven Developement: LinkedIn Learning, 2013.


<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_3/imgs/alabama.png" />
</center>
<figcaption class="img_footer">
    Fig. 3: Orange Beach, Alabama, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/x_wloeGrJGs" class="img_footer">Steven Van Elk @ Unsplash</a>).
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