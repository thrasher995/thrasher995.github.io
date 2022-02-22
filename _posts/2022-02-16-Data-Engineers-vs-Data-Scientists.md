---
layout: post
title: Data Engineers vs Data Scientists
subtitle: Data Engineers enable Data Scientists
categories: dataengineering datascience
tags: [data, engineering, Scientists]
---

#### * Refering to the Data Workflow:
```mermaid
flowchart LR;
    subgraph Data Engineer
        A[Data Collection & Storage];
    end

    subgraph Data Scientist
        B[Data Prep.] 
        B-->C[Exploration & Visualization];
        C-->D[Experimentation & Prediction];
    end
    A --> B

    style A fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
    style B fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    style C fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    style D fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

```


#### * Comparison of Tasks:

| Data Engineer            | Data Scientist             |
| --- | --- |
| * Ingest data            | * Exploit data             |
| * Set up DBs             | * Access DBs               |
| * Build data pipelines   | * Use pipeline outputs     |
| * Strong SW Skills       | * Strong Analytical Skills |



