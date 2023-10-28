---
author: "Minh T. Nguyen"
title: "System Design Fundamentals Note"
date: "2023-01-20"
description: "Notes on fundamentals system design concepts, collected from Sahn Lam's lecture series"
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

## [Computer Memory & Storage](https://www.youtube.com/watch?v=lX4CrbXMsNQ&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf&index=1)
- **Storage**
  - **HDD** (hard disk drive): it works by spinning magnetics disk.
  - **SSD** (solid state drive): it uses NAND-based flash memory, providing fast data access, reduces power consumption, and increases durability. It is more expensive.
  - **USB Drive**: is a small plug-and-play device for convenient data transfer between computers.
  - **SD Card** is commonly found in camera and smartphone. There is SD Card, Mini Card, and Micro Card.
- **Memory**
  - **RAM** (random access memory): is a type of memory that store data temperarily while the computer is running. It's fast and flexible. However, all the data is lost after the power is off.
    - **SRAM** (static random access memory): is a fast and expensive DRAM used in high speed application like CPU caches, where quick access time is crucial.
    - **DRAM** (dynamic random access memory): is slower and cheaper than SRAM. It needs to be constantly refreshed to maintain data.
      - **SDRAM**
      - **DDR SDRAM**: with examples like DDR4, DDR5.
      - **GGDDR SDRAM**: is a specialized of DRAM with faster data transfer rates for parallel processing.
  - **ROM** (read only memory): is a type of memory that retains data, even when the memory is off. It is used to store essential information like firmware and BIOS.
    - **Firmware**: is a type of software stored in ROM that determines how hardware devices communicate with each others
    - **BIOS** (basic input-output systems): first run when you booth up the computer. It is responsible for starting your computer, initializes hardware components, and hands over controls to the OS.

## [Domain Name System (DNS)](https://youtu.be/27r4Bzuj5NQ?si=t1Zb0_2fB1yiGKTs)
It is the backbone of the internet. 

***But how does it work?***

DNS is a directory: it translates human-readable domain names (i.e, www.google.com) to machine-readable IP-addresses.

There are different DNS servers with different purposes. The DNS Resolver can be provided by Cloudflare (1.1.1.1) or Google (8.8.8.8). 

***How does the DNS Resolver find the authoritative nameservers?*** 

There are 3 levels of DNS: 
- **Root Nameservers**: stores the IP-addresses of the TLD nameservers. There are 13 logical Root Nameservers. Ex: .com, .org, .edu
- **Top Level Domain (TLD) Nameservers**: stores the IP-addresses of the Authoritative Nameservers. Ex: google.com, wikipedia.org, mit.edu. 
- **Authoritative Nameservers**: stores authoritative answers to queries

Such design above make DNS decentralized and robust.

***How does the workflow look like?***
<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/system_design_concepts/imgs/2_dns.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: DNS workflow (Image source: 
    <a>ByteByteGo.com</a>).
</figcaption>
</br>

- The user types "google.com" to browser.
- The browser first checks its cache, if there is no answer, it makes the OS call to get the answer.
- The OS then reachs out to DNS Resolver.
- The DNS Resolver first checks its cache, if it is not there or if the answer is expired, it will ask the Root Nameservers.
- The Rootname Servers responses with the root name TLD Nameservers. Here, if the RootName Servers found the root name TLD Nameservers (i.e. .com as it is common) in its cache, it will return.
- The DNS Resolver then reachout to the TLD Nameservers, which return the Authoritative Nameservers for "google.com".
- The DNS Resolver then reachout to the Authoritative Nameservers and get the IP-address of "google.com".
- The DNS Resolver then returns the address of the IP system to the OS, and the OS returns it to the browswer.

## [Common Latency Numbers](https://youtu.be/FqR5vESuKe0?si=o4TviuBEP_tAExaY)

<center>
    <img style="width: 35%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/system_design_concepts/imgs/3_latency_.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Latency number hierachy (Image source: 
    <a>ByteByteGo.com</a>).
</figcaption>
</br>

- **1 ns**: Accessing CPU registers, CPU clock cycle.
- **1-10 ns**: L1/L2 cache, Branch mispredict.
- **10-100 ns**: L3 cache.
- **100-1000 ns**: System call, MD5 hash.
- **1-10 µs**: Context switches between threads. 
- **10-100 µs**: Higher level operations such as process a http request, sequential read, read a 8K page.
- **100-1000 µs**: SSD write latency, intra-zone networking round trip, memcache/redis get operation.
- **1-10 ms**: Intra-zone network latency, seek time of HDD.
- **10-100 ms**: Network round-trip from US West-East.
- **100-1000 ms**: Bcrypt a password, TLS handshake, reading sequentially 1GB of SSD.
- **1 s**: Tranfer 1GB over the network within the same cloud region.
 
## Citation
Cited as:

<blockquote>
    <summary>Scale From Zero To Millions Of Users: An Understanding.</summary>
    <summary>https://mnguyen0226.github.io/posts/system_design_concepts/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mtl,
  title   = "System Design Fundamentals Note",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "January",
  url     = "https://mnguyen0226.github.io/posts/system_design_concepts/post/"
}
```

## References
[1] A. Xu, System Design Interview - An Insider’s Guide. Independently Published, 2020.
‌

[2] ByteByteGo, “10+ Key Memory & Storage Systems: Crash Course System Design #5,” YouTube. Mar. 28, 2023. Accessed: Oct. 25, 2023. [YouTube Video]. Available: https://www.youtube.com/watch?v=lX4CrbXMsNQ&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf
‌

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/system_design_concepts/imgs/golden_bridge.png" />
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