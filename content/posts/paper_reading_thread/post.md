---
author: "Minh T. Nguyen"
title: "Paper-Reading Thread"
date: "2023-05-18"
description: "Notes on (1) papers I read."
tags: ["paper-reading", "long-read"]
categories: ["software engineer", "deep learning", "systems design"]
series: ["Machine Learning"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: true
weight: 3
---
<p style="color: #286EE0"><strong>Status:</strong> [Latest]</p>

In the field of machine learning (ML), staying ahead of the curve involves actively reading papers. Renowned ML researcher Andrew Ng, from Stanford University and founder of Coursera and Landing.AI, provides valuable tips and tricks in his [lecture](https://www.youtube.com/watch?v=733m6qBH-jI&ab_channel=StanfordOnline) for understanding ML domains and effectively reading research papers. According to Ng, reading 50-100 papers is crucial for gaining a deep understanding of the field.

**How to select papers?** To select papers, start by compiling a list that includes research papers, Medium posts, blog posts, GitHub repositories, and conference materials. From this list, choose five papers that you find most intriguing or relevant, and mark your initial understanding percentage while reading them. If a paper has been discredited by other researchers, it's advisable to discard it. Otherwise, reread and strive to fully comprehend it. Continuously add more papers to your reading list to expand your knowledge and understanding of the field.

**How to read one paper?** It's recommended to avoid reading it from start to finish in a single pass. Instead, employ a spaced-repetition approach and read the paper in multiple passes. Here's a suggested approach:
<ul type="1">
    <li><strong>1st pass</strong>: Focus on the title, abstract, and figures, while skimming through the rest of the paper.</li>
    <li><strong>2nd pass</strong>: Concentrate on the introduction, conclusion, key figures, and skim the remaining sections.</li>
    <li><strong>3rd pass</strong>: Revisit the entire paper, skipping parts that you already understand well.</li>
    <li><strong>4th pass</strong>: Dive into the mathematical details and equations, understanding them thoroughly.</li>
</ul>

The total time spent on these four passes may vary from 30 minutes to 2 hours, depending on the complexity and length of the paper. After going through the four reading passes, try to answer the following questions:
<ul type="1">
    <li><strong>Q1</strong>: What were the authors aiming to accomplish with their research?</li>
    <li><strong>Q2</strong>: What were the key elements or approaches used in their work?</li>
    <li><strong>Q3</strong>: What aspects of their research can you utilize or apply in your own work?</li>
    <li><strong>Q4</strong>: Which additional references or sources would you like to explore to deepen your understanding of the topic?</li>
</ul>

<center>
    <img style="width: 70%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/paper_reading_thread/imgs/types_of_scientific_paper.png" />
</center>
<figcaption class="img_footer">
    Fig. 1. Types of scientific paper (Image source: 
    <a href="https://xkcd.com/2456/" class="img_footer">xkcd.com</a>).
</figcaption>
</br>

**Why do I start this paper-reading-and-noting journey?**
Embarking on a journey of reading and taking notes on research papers holds significant value for me. Throughout my undergraduate and graduate studies, I had the privilege of working at a research lab, which provided me with invaluable opportunities to delve into various papers and present my insights in academic forums. Recognizing the potential benefits of open-source note sharing, I aim to contribute to the machine learning community by documenting my findings. As the saying goes, teaching is a powerful way to enhance our own learning. In line with this notion, [Eugene Yan](https://twitter.com/eugeneyan/status/1300954984461156352?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1300954984461156352%7Ctwgr%5Eb55e848832d840c4d87e38f0f075ad552b653cef%7Ctwcon%5Es1_&ref_url=https%3A%2F%2Feugeneyan.com%2Fwriting%2Fwhy-read-papers%2F) emphasizes the importance of paper reading: it broadens our perspective, keeps us up to date, and enhances our efficiency by reducing time and effort.

The following collection of topics and papers draws from the [Applied Deep Learning](https://github.com/maziarraissi/Applied-Deep-Learning) Github repository, serving as a foundation for expanding my repertoire of knowledge. Over time, I will continually augment this list by incorporating additional noteworthy papers.

## Image Classification

### Large Networks
<details>
    <summary>
        <strong>D. Cireşan et al.</strong>
        <a href="Multi-column Deep Neural Networks for Image Classification"> Multi-column Deep Neural Networks for Image Classification</a> (2012).
    </summary>
    <blockquote>
            <summary>
                <img src="https://geps.dev/progress/70">
            </summary>
            <summary>
                ▪ Q1:
            </summary>
            <summary>
                ▪ Q2:
            </summary>
            <summary>
                ▪ Q3:
            </summary>
            <summary>
                ▪ Q4:
            </summary>
            <summary>
                ▪ Additional Resources:
            </summary>
    </blockquote>
</details>

### Small Networks

### AutoML

### Robustness

### Visualizing & Understanding

### Transfer Learning

---
## Image Transformation

### Semantic Segmentation

### Super-Resolution, Denoising, and Colorization

### Pose Estimation

### Optical Flow and Depth Estimation

---
## Object Detection

### Two Stage Detectors

### One Stage Detectors

---
## Face Recognitionn & Detection

---
## Video

---
## 3D

---
## NLP
### Word Representations

### Text Classification

### Neural Machine Translation

### Language Modeling

---
## Multimodal Learning

---
## Generative Networks
### Variational Auto-Encoders

### Unconditional GANs

### Conditional GANs

### Diffusion Models

---
## Advanced Topics
### Domain Adaptation

### Few Shot Learning

### Federated Learning

### Semi-Supervised Learning

---
## Speed & Music

### Recognition

### Synthesis

### Modeling

---
## Reinforcement Learning
### Games

### Simulated Environments

### Real Environments

### Uncertainty Quantification & Multitask Learning

---
## Graph Neural Networks

---
## Recommender Systems

---
## Computational Biology

## Citation
Cited as:

<blockquote>
    <summary>Nguyen, Minh. (May 2023). Paper-Reading Thread.</summary>
    <summary>https://mnguyen0226.github.io/posts/paper_reading_thread/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023paper,
  title   = "Paper-Reading Thread.",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "May",
  url     = "https://mnguyen0226.github.io/posts/paper_reading_thread/post/"
}
```

## References

[1] “Stanford CS230: Deep Learning | autumn 2018 | lecture 8 - career advice / reading research papers,” YouTube, https://www.youtube.com/watch?v=733m6qBH-jI&amp;ab_channel=StanfordOnline (accessed May 19, 2023). 

[2] Maziarraissi, “Maziarraissi/applied-deep-learning: Applied deep learning course,” GitHub, https://github.com/maziarraissi/Applied-Deep-Learning (accessed May 19, 2023). 

[3] D. Cireşan, U. Meier, and J. Schmidhuber, “Multi-column deep neural networks for Image Classification,” arXiv.org, https://arxiv.org/abs/1202.2745 (accessed May 19, 2023). 

[4] E. Yan, “How reading papers helps you be a more effective data scientist,” eugeneyan.com, https://eugeneyan.com/writing/why-read-papers/ (accessed May 19, 2023). 

<center>
    <img style="width: 80%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/paper_reading_thread/imgs/hanoi.png" />
</center>
<figcaption class="img_footer">
    Fig. 2. Coffee next to train-track at Hanoi, Vietnam. </br>
    (Image source: 
    <a href="https://unsplash.com/photos/u-z8Cq8EZgM" class="img_footer">Dave Weatherall @ Unsplash</a>)
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