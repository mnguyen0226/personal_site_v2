---
author: "Minh T. Nguyen"
title: "Fundamentals of Data Engineering: Foundation and Building Blocks"
date: "2024-01-05"
description: ""
tags: ["web development"]
categories: ["data engineer", "systems design"]
series: ["Systems Design"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (01/05/2024):</strong> Post started!</p>

This book is about data engineering lifecycle: data generation, storage, ingestion, transformation, and serving

## 1. Data Engineering Described

### What Is Data Engineering?
- A data engineer gets data, stores it, and prepares it for consumption by data scientists, analysts, and others.
- Data engineering is the development, implementation, and maintenance of systems and processes that take in raw data and produce high-quality, consistent information that supports downstream use cases, such as analysis and machine learning. Data engineering is the intersection of security, data management, DataOps, data architecture, orchestration, and software engineering. A data engineer manages the data engineering lifecycle, beginning with getting data from source systems and ending with serving data for use cases, such as analysis or machine learning.
- Stage of data engineer lifecycle:
  - Generation
  - Storage
  - Ingestion
  - Transformation
  - Serving

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/fundamentals_of_data_engineering_1/imgs/data_science_needs.png" />
</center>
<figcaption class="img_footer">
    Fig. 1. Data Science Hierarchy of Needs </br>
</figcaption>

- 70%-80% o the time doing the bottom 3: gathering data, cleaning data, processing data. Data scientist aren't typically trained to engineer production-grade data system.
- Data from various sources > Data engineering > Data science and analytics

### Data Engineering Skills and Activities
- Skillset of data engineering: security, data management, DataOps, data architecture, and software engineering.
- Data engineer also care about: Cost, Agility, Scalibility, Simplicity, Reuse, Interoperability.
- Data engineer typically does not directly build ML models, create reports or dashboards, perform data analysis, build KPI or develop software application.
- **Data Maturity & the Data Engineer**:
  - The data maturity model has 3 stages: starting with data, scaling with data, and leading with data.
  - **Stage 1**: Starting with data
    - Here, data engineer is a generalist, do everything.
    - Choose the right data architecture.
    - Identify and audit data.
    - Build a solid data foundationn for future data analyst and data scientist to generate reports and models that provide competitive values.
    - Tips:
      - Quick win create technical debts.
      - Get out and talk to people. 
      - Avoid undifferentiate heavy lifetying. Don't box yourself in with unncessary technical complexity. Use off-the-shelf, turnkey solutions wherever possible.
  - **Stage 2**: Scaling with data
    - Data engineer here is a specialist, focusing on data science life cycle.
    - Tips:
      - Establish formal data practices
      - Create scalable and robust data architectures
      - Adopt DevOps and DataOps practices
      - Build systems that support ML.
      - Continue to avoid undifferentiate heavy lifting and customize only when competitive advantage results.
    - Tips:
      - Any tech decisions should be driven by the value they will deliver to your customers.
      - Main bottleneck or scaling is not technology by the data engineering team. Focus on solutions that are simple to deploy and manage to expand your team's throughput.
      - You will be tempted to frame yourself as technologist, a data genuis who deliver magical product. Shift your focus instead to pragmatic leadership and transition to next maturity stage. Make sure to communicate with other teams about the practical utility of data and teach the organization how to consume and leverage data.
  - **Stage 3**: Leading with data
    - The company is data-driven. The automated pipelines and system created by data engineers allow people in the team to self-service analytics and ML. 
    - Data engineer need to be more specialize
      - Create automation for the seamless introduction and usage of new data.
      - Focus on building custom tools and systems that leverage data as a competitive advantage.
      - Focus on the “enterprisey” aspects of data, such as data management (including data governance and quality) and DataOps.
      - Deploy tools that expose and disseminate data throughout the organization, including data catalogs, data lineage tools, and metadata management systems
      - Collaborate efficiently with software engineers, ML engineers, analysts, and others.
      - Create a community and environment where people can collaborate and speak openly, no matter theri role or position.
    - Tips:
      - Once organizations reach stage 3, they must constantly focus on maintenance and improvement or risk falling back to a lower stage.
      - Technology distractions are a more significant danger here than in the other stages. There’s a temptation to pursue expensive hobby projects that don’t deliver value to the business. Utilize custom-built technology only where it provides a competitive advantage.

- **The Background and Skills of Data Engineer**
  - Data engineer must understand both data and technology. Data engineer must also understand the requirements of data consumers (data analysts and data scientists) and the broader implications o data across the org.

- **Business Responsibilities**
  - Know how to communicate with nontechnical and technical people. Pay close attention to organizational hierarchies, who reports to whom, how people interact. Observe!
  - Understand how to scope and gather business and product requirements. Know what to build and ensure that your stakeholders agress with your assessments. Develop a sense of how data and technologuy decisions impact the business.
  - Understand the cultural foundations of Agile, DevOps, and DataOps.
  - Control cost. You will be successful when you can keep the cost low while providing outsized values. Know how to optimize for time to value, the total cost of ownership, and opportunity cost.
  - Learn continuously. People who succeed in data are great at picking up new things while sharpening their fundamental knowledge.They’re also good at filtering, determining which new developments are most relevant to their work, which are still immature, and which are just fads. Stay abreast of the field and learn how to learn.

- **Technical Responsibilities**
  - SQL: The most common interface for databases and data lakes. After briefly being sidelined by the need to write custom MapReduce code for big data processing, SQL (in various forms) has reemerged as the lingua franca of data.
    - We believe that competent data engineers should be
highly proficient in SQL
  - Python: API, Pandas, NumPy, Airflow, Sklearn, Tensorflow, PyTorch, and PySpark.
  - JVM (Java, Scala): Spark, Hive, Druid.
  - Bash

## 2. The Data Engineering Lifecycle

### What Is the Data Engineering Lifecycle?

### Major Undercurrents Across the Data Engineering Lifecycle

## 3. Designing Good Data Architecture

### What is Data Architecture?

### Principles of Good Data Architecutre

### Major Architecture Concepts

### Examples and Types of Data Architecture

### Who's Involved with Designing a Data Architecture?

## 4. Choosing Technologies Across the Data Engineer Life Cycle

### Team Size and Capabilities

### Speed to Market

### Interoperability

### Cost Optimization and Business Value

### Today vs. Future: Immutable Vs. Transitory Technology

### Location

### Build vs Buy

### Monolith Vs. Modular

### Serverless vs. Servers

### Optimization, Performance, and the Benchmark Wars

### Undercurrents and Their Impacts on Choosing Technologies

## Citation
Cited as:

<blockquote>
    <summary>Fundamentals of Data Engineering: Foundation and Building Blocks</summary>
    <summary>https://mnguyen0226.github.io/posts/fundamentals_of_data_engineering_1/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mtl,
  title   = "Fundamentals of Data Engineering: A Summary",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "January",
  url     = "https://mnguyen0226.github.io/posts/fundamentals_of_data_engineering_1/post/"
}
```

## References


<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/fundamentals_of_data_engineering_1/imgs/golden_bridge.png" />
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