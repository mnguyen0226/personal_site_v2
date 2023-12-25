---
author: "Minh T. Nguyen"
title: "System Design Roadmap"
date: "2023-12-01"
description: "Notes on fundamentals system design concepts, collected from Sahn Lam's lecture series."
tags: ["long-read"]
categories: ["software engineer", "systems design"]
series: ["Systems Design"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (01/20/2023):</strong> Post started!</p>

## 1. Basics

### Horizontal vs. Vertical Scaling
**Scalability**: the ability to buy bigger machine or more machine. Or throwing money to the problem.

**Horizontal Scaling**: buy more machines.
- Required load-balancing.
- Is resilient.
- Network calls (RPC).
- Data consistency is an issue.
- Scale well as the users increase.

**Vertical Scaling**: buy bigger machine.
- No need for load-balancing.
- A single point of failure.
- Inter-process between communication.
- Data consistency is not an issue.
- Hardware limit.

In the real-world, we use both and select the good qualities.

## 2. Load Balancing

## 3. Data Storages

## 4. Consistency vs. Availability

## 5. Message Queues

## 6. DevOps Concepts

## 7. Caching

## 8. Microservices

## 9. API Gateways

## 10. Authenication Mechanisms

## 11. System Design Tradeoffs

## Citation
Cited as:

<blockquote>
    <summary>System Design Roadmap.</summary>
    <summary>https://mnguyen0226.github.io/posts/system_design_roadmap/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023sdr,
  title   = "System Design Roadmap.",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "December",
  url     = "https://mnguyen0226.github.io/posts/system_design_roadmap/post/"
}
```

## References
[1] “[Complete] System Design Roadmap with Videos for SDEs - Interviews,” takeUforward - ~ Strive for Excellence, Sep. 18, 2023. Available: https://takeuforward.org/system-design/complete-system-design-roadmap-with-videos-for-sdes/. [Accessed: Dec. 01, 2023]
‌

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/system_design_roadmap/imgs/golden_bridge.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Golden Gate Bridge, San Francisco, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/gZXx8lKAb7Y" class="img_footer">Maarten van den Heuvel @ Unsplash</a>).
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