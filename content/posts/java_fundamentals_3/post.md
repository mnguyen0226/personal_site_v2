---
author: "Minh T. Nguyen"
title: "Java Fundamentals (Part 3)"
date: "2023-09-25"
description: "Notes on test-driven development (TDD)"
tags: ["java, tdd"]
categories: ["software engineer"]
series: ["Software Engineering"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: true
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (09/25/2023):</strong> Post published!</p>

## Test-Driven Development
In software development, there are different ways to test softwares:
- **Beta testing:** Provides a finished or near-finished application to a group of users and sees what problems they come up with.
- **Performance testing:** Uses profiling tools to measure if we are getting acceptable response time. Is this application running as fast as it should be or it need to be?
- **Stress testing:** A type of performance testing. We want to know how well the application runs under heavy loads.
- **Integration testing:** Test one app's integration-ability to another app.

Here, we focus on testing individual units of our code! We test our code as we write it.

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_3/imgs/unit_testing.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Unit-test </br>(Image Source: 
    <a href="https://www.monkeyuser.com/2022/unit-tests/" class="img_footer">monkeyuser.com</a>).
</figcaption>



##

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
[1] P.Deitel, Java: How To Program, Early Objects: Pearson, 2017

[2] Horstmann, Cay S. Big Java: Early Objects. John Wiley & Sons, 2020.

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/java_fundamentals_3/imgs/alabama.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Orange Beach, Alabama, U.S.A </br>(Image Source: 
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