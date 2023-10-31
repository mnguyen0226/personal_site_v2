---
author: "Minh T. Nguyen"
title: "System Design Fundamentals Mega-Blog"
date: "2023-01-20"
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
    <img style="width: 35%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/system_design_concepts/imgs/3_latency.png" />
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
 
## [REST API](https://www.youtube.com/watch?v=-mN3VyJuCjM&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf&index=4)
**Representational State Transfer Application Programming Interface (REST API)** is the most popular communication standard between computers over Internet. **API** is a way for two computers to talk to each other. The common API used by mobile and web applications to talk to the servers is called **REST**. For instance, Twilio, Stripe, Google Maps use REST API.

**REST** is not a specification, it is a loose set of rules for building web API since the early 2000s. Those rules are:
- Uniform Interface.
- Client-Server.
- Stateless.
- Cacheable.
- Layered System.
- Code on Demand (Optional).

### Basics of REST API
The REST API organizes resources into a set of unique Uniform Resource Identifiers (URIs). The URIs differentiate types of resources on a server.
```
https://example.com/api/v3/products
https://example.com/api/v3/users
```

A client connects to resources by making a request to the endpoint for the resource over HTTP. The request has a specific format such as `POST/products HTTP/1.1`.

Here are the operations (CRUD)
- `POST`: `CREATE` a new resource.
- `GET`: `READ` the data about an existing resource.
- `PUT`: `UPDATE` an existing resource.
- `DELETE`: `DELETE` an existing resource.

In the body of these request, there could be an optional HTTP request body that contains a custom payload of data, usually encoded in JSON. 
```
POST/produccts HTTP/1.1
Accept: application/json

JSON: {
  "customer": "Minh Nguyen",
  "quantity": 1,
  "price": 19.00
}
```

The server receives a request, processes it and form the result into response.
```
HTTP/1.1 200 OK
```

Some HTTP status codes:
- `200`: Request is successful.
- `400`: Something is wrong with our request, such as wrong syntax.
- `500`: Something is wrong at the server level, such as the server is not available.

### Stateless
A REST implementation should be stateless. This means that the two parties don't need to store any information about each other, and every request and response (cycle) is independent from all others. This attribute leads to the web application that is easy to scale and well behaved.

### Pagination
If the return endpoint returns a huge amount of data, we should use pagination. A common scheme uses `limit` and `offset` as parameters. If they are not specified, the server should assume sensible default values.

```
/products?limit=25&offset=50
```

### Versioning
Versioning allows an implementation to provide backward compatibility, so that if we introduce breaking changes from one version to another, consumers can get enough time to move to the next version.

There are many ways to versioning an API. The most common way is to prefix the version before the resource on the URI.
```
/v1/products
/v2/products
```

RESTful API is sensible if used correctly as it is simple and good enough, and that's why it is so widely used. Other options are `GraphQL` and `gRPC`.
 
## [10 Key Data Structures in System Design](https://www.youtube.com/watch?v=ouipSd_5ivQ&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf&index=5)

The choice of correct data structures based on the specification and constraints of the projects is important. To refresh the fundamentals of these data structures, please visit [https://neetcode.io/](https://neetcode.io/).

### Linked List
Linked list (or list) is a versatile and essential data structure in software development. It is great for storing and manipulating ordered data. They are useful in various applications such as *task-management*, *social media feeds*, and *shopping carts*.

For *task-management application*, a list can be used to store and organize tasks for each user. Tasks can be added, removed, or reordered easily, and users can mark them as complete or incomplete.

In *social media application*, e.g. Twitter (X), where they can store and display a users' feeds in real-time, ensuring the order is correct in real-time.

### Array 
Array provdes a fixed-size, ordered collection of elements. They are suitable for situation where the size of the collections is known or isn't changed frequently. Arrays are commonly used in mathematical operations, storing large datasets, or when there is a need for random access to elements.

For instance, in the *weather application*, an array can store temperature readings for a specific location over a defined period. This allows for easy calculations like average temperature or trends analysis.

Arrays are also used in *image-processing*, where each pixel's color data can be represented in a 2D array. It enables efficient manipulation and transformation of the image.

### Stack
Stacks follow the LIFO principle, and they are perfect for supporting undo/redo operations in *text editors* or maintaining *browsing history in web browsers*.

In the *text editors*, a stack can be used to store each change made to the text, making it simple to revert to a previous state when the user triggers an undo operation.

### Queue
Queues operate on the FIFO principle, and they are good for managing *printer jobs*, sending actions in *games*, or handling messages in *chat applications*. Specifically, in *chat applications*, a queue can be used to store incoming messages in the order they are received. It ensures that they are displayed to the recipient in the correct sequence.

### Heap
Heaps are used for *task scheduling* and *memory management*. They are helpful in implementing priority queues where we need to access the highest or lowest priority item efficiently.

### Tree
Trees organize data hierarchically. They are useful for representing data with natural hierarchies or relationships. Trees are used in *database indexing*, *file systems*, or *AI decision tree*.

For *database indexing*, tree helps speed up search, insert, or delete operations. For example, B-trees and B+ trees are commonly used in relational databases to efficiently manage and index large amount of data.

### Hash Table
Hash table (or hashmap) allows for efficent data lookup, insertion, and deletion. They use a hash function to map keys to their corresponding storage locations. It enables constant-time access to the stored values. Hash tables are widely used in various applications, such as *search engines*, *caching systems*, and *programming language interpreters* or *compilers*.

In *search engine*, hash table allows to store and quickly retrieve indexed data based on keywords. This provides fast and relevant search results.

*Caching systems* may use hash tables to store and manage cached data. It allows for eapid access to frequently requested resources and improves overall system performance.

### Suffix Tree
Suffix trees (or tries) are specialized for searching strings in documents. This makes them perfect for *text editors* and *search algorithms*. In a *search engine*, a suffix tree can be used to efficiently locate all occurrences of a search term within a larger corpus of text.

### Graph
Graphs are all about tracking relationships or finding paths. This makes them invaluable in *social networks*, *recommendation engines*, and *pathfinding algorithms*.

In a *social network*, a graph can be used to represent a connections between users. It enables features like friend suggestion or analyzing network trends.

### R-tree
R-trees are good at finding nearest neighbors. They are crucial for *mapping apps* and *geolocation services*. In a *mapping applications*, R-trees can be used to store spatial data, such as points of interest. This enables efficient queries to find the nearest locations based on the user's current position.

### Cache Friendliness Relations to Data Structures
CPU cache is a small, fast memory between the main memory (RAM) and the CPU. It stores recently accessed data and instructions, so the CPU can access them quickly without fetching them from the slower main memory.

Different data structures have different levels of cache friendliness based on how their elements are stored in memory. Contiguous memory storage (arrays) allows for better cache locality and fewer cache misses, resulting in improved performance. When an array element is accessed, the cache can be prefetch and store nearby elements, anticipating that they might be accessed soon. While data structures with non-contiguous memory storage (linked-list) can experience more cache misses and reduce performance. In a linked list, elements are stored in nodes scattered throughout the memory and each node contains a pointer to the next node in the sequence. This makes it difficult for the CPU to predict and load the next node before it's needed.

Other data structures have varying degrees of cache friendliness based on their implementation and use case. This disparity in access times can lead to performance issues in modern computing, particularly in situations where cache misses occur frequently.

## [Cache Systems](https://www.youtube.com/watch?v=dGAgxozNWFE&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf&index=6)
Caching is a common technique in modern computing to system performance and reduce response time. From the front-end to back-end, caching plays a crucial role in improving the efficiency of various applications and systems.

A typical system architecture involves several layers of caching. At each layer, there are multiple strategies and mechanisms for caching data, depending on the requirements and constraints of the specific application.

### Computer Caching Mechanism
The most common hardware cache are *L1*, *L2*, and *L3* caches. 
- *L1 cache* (KBs) is the smallest and fastest cache, typically integrated into the CPU itself. It stores frequently accessed data and instructions, allowing the CPU to quickly access them without having to fetch them from slower memory.
- *L2 cache* (MBs) is larger but slower than L1. It is typically located on the CPU die or on a separate chip.
- *L3 cache* is larger but slower than L2. It is typically shared between multiple CPU cores.

Another common hardware cache is the *translation lookaside buffer (TLB)*. It stores recently used virtual-to-physical address translations. It is used by the CPU to quickly translate virtual memory addresses to physical memory addresses, reducing the time needed to access data from memory

At the OS level, there are *page cache* and other *file system caches*. *Page cache* is managed by the OS and resides in the main memory. It is used to store recently used disk blocks in memory. When a program requests data from the disk, the OS can quickly retrieve the data from memory instead of reading it from disk. There are other caches managed by the OS, such as *inode cache*. These caches are used to speed up file system operations by reducing the number of disk accesses required to access files and directories.

### Cache in System Architecture

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/system_design_concepts/imgs/6_cache.png" />
</center>
<figcaption class="img_footer">
    Fig. 3: Cache in System Architecture (Image source: 
    <a>ByteByteGo.com</a>).
</figcaption>
</br>

**Front-end**: web browsers can cache HTTP response to enable faster retrieval of data. When we request data over HTTP for the first time and it returned with an expiration policy in the HTTP header; we request thee same data again, and the broweser returns the data from its cache if available.

**CDNs**: are used to improve the delivery of static contents (images, videos, web assets). When a user requests a content from a CDN, the CDN network looks for the requested content in its cache. If the content is not already in the cache, the CDN fetches it from the origin server and caches it on its edge servers. When another user requests the same content, the CDN can deliever the content directly from its cache, eliminating the need to fetch it from the origin server again.

**Load-balancers**: implement cache resources to reduce the load on back-end servers. When a user requests content from a server behind a load balancer, the load balancer can cache the response and server it directly to future users who request the same content. This can improve response times and reduce the load on back-end servers.

**Messeging infrastructure**, **message brokers** such as Kafka can cache a massive amount of messages on disk. This allows consumers to retrieve the message at their own pace. The messages can be cached for a long period of time based onthe retention policy.

**Distributed caches** such as Redis can store key-value pairs in memory, providing high read/write performance compared to traditional databases.

**Full-text search engines** like Elastic Search can index data for document search and log search, providing quick and efficient access to specific data.

**Relational database**: has multiple levels of caching:
- *Data* is typicaly written to WAL (write-ahead-log), before indexed in a B-tree.
- *Buggerpool* is a memory area used to cache query results.
- *Materialized-view* can precompute query results for faster performance.
- *Transaction-log* records all transactions and updates to the database.
- *Replication-log* tracks the replication state in the database cluster.

## Citation
Cited as:

<blockquote>
    <summary>System Design Fundamentals Mega-Blog</summary>
    <summary>https://mnguyen0226.github.io/posts/system_design_concepts/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023sdmega,
  title   = "System Design Fundamentals Mega-Blog",
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

[3] ByteByteGo, “Latency Numbers Programmer Should Know: Crash Course System Design #1,” YouTube. Oct. 04, 2022. Accessed: Oct. 31, 2023. [YouTube Video]. Available: https://www.youtube.com/watch?v=FqR5vESuKe0&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf&index=3
‌

[4] ByteByteGo, “What Is REST API? Examples And How To Use It: Crash Course System Design #3,” YouTube. Aug. 24, 2022. Accessed: Oct. 31, 2023. [YouTube Video]. Available: https://www.youtube.com/watch?v=-mN3VyJuCjM&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf&index=4
‌

[5] ByteByteGo, “10 Key Data Structures We Use Every Day,” YouTube. May 01, 2023. Accessed: Oct. 31, 2023. [YouTube Video]. Available: https://www.youtube.com/watch?v=ouipSd_5ivQ&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf&index=5
‌

[6] ByteByteGo, “Cache Systems Every Developer Should Know,” YouTube. Apr. 04, 2023. Accessed: Oct. 31, 2023. [YouTube Video]. Available: https://www.youtube.com/watch?v=dGAgxozNWFE&list=PLCRMIe5FDPsd0gVs500xeOewfySTsmEjf&index=6
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