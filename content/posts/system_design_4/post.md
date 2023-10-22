---
author: "Minh T. Nguyen"
title: "Design A Rate Limiter: An Understanding"
date: "2023-03-08"
description: "Learning notes on chapter 1 of 'System Design Interview' - Alex Xu."
tags: ["web development", "long-read"]
categories: ["software engineer", "systems design"]
series: ["Systems Design"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: true
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (01/20/2023):</strong> Post started!</p>

We will start by building a system that supports a single user and graduatelly scale it up to serve millions of users.

## Single server setup

## Database

## Vertical scaling vs horizontal scaling

## Load balancer

## Database replication

## Cache

## CDN

## Stateless web tier

## Data center

## Message queue

## Logging, metrics, automation

## Citation
Cited as:

<blockquote>
    <summary>Scale From Zero To Millions Of Users: An Understanding.</summary>
    <summary>https://mnguyen0226.github.io/posts/scale_from_zero_to_millions_of_users/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mtl,
  title   = "Scale From Zero To Millions Of Users: An Understanding.",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "January",
  url     = "https://mnguyen0226.github.io/posts/scale_from_zero_to_millions_of_users/post/"
}
```

## References
[1] Xu, Alex, and Sahn Lam. System Design Interview: An Insider's Guide. Vol. 1. Byte Code LLC, 2020.

[2] Hypertext Transfer Protocol: https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol

[3] Should you go Beyond Relational Databases?: https://blog.teamtreehouse.com/should-you-go-beyond-relational-databases

[4] Replication: https://en.wikipedia.org/wiki/Replication_(computing)

[5] Multi-master replication: https://en.wikipedia.org/wiki/Multi-master_replication

[6] NDB Cluster Replication: Multi-Master and Circular Replication: https://dev.mysql.com/doc/refman/5.7/en/mysql-cluster-replication-multimaster.html

[7] Caching Strategies and How to Choose the Right One: https://codeahoy.com/2017/08/11/caching-strategies-and-how-to-choosethe-right-one/

[8] R. Nishtala, "Facebook, Scaling Memcache at," 10th USENIX Symposium on Networked Systems Design and Implementation (NSDI’13).

[9] Single point of failure: https://en.wikipedia.org/wiki/Single_point_of_failure

[10] Amazon CloudFront Dynamic Content Delivery: https://aws.amazon.com/cloudfront/dynamic-content/

[11] Configure Sticky Sessions for Your Classic Load Balancer: https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-stickysessions.html

[12] Active-Active for Multi-Regional Resiliency: https://netflixtechblog.com/active-active-for-multi-regional-resiliencyc47719f6685b

[13] Amazon EC2 High Memory Instances: https://aws.amazon.com/ec2/instance-types/high-memory/

[14] What it takes to run Stack Overflow: http://nickcraver.com/blog/2013/11/22/what-it-takes-to-run-stack-overflow

[15] What The Heck Are You Actually Using NoSQL For: http://highscalability.com/blog/2010/12/6/what-the-heck-are-you-actuallyusing-nosql-for.html

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/scale_from_zero_to_millions_of_users/imgs/golden_bridge.png" />
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