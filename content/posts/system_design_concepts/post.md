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

## Computer Memory & Storage
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

## Citation
Cited as:

<blockquote>
    <summary>Scale From Zero To Millions Of Users: An Understanding.</summary>
    <summary>https://mnguyen0226.github.io/posts/scale_from_zero_to_millions_of_users/post/.</summary>
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