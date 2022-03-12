---
layout: post
title: Data Engineering for Everyone
subtitle: Responsibilities & Big Data
categories: Pipelines
tags: [data, engineering]
mermaid: true
---

## Data Workflow:
<div class="mermaid">
flowchart LR;
    
    A[Data Collection & Storage] --> B[Data Prep.];
    B-->C[Exploration & Visualization];
    C-->D[Experimentation & Prediction];
    

    style A fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
    style B fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    style C fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    style D fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

</div>

#### * Data Engineers deliver the correct data in the right form, to the right people, as efficiently as possible.

## Data Engineer's Responsibilities:
1. Ingest data from different sources.
2. Optimize DBs for analysis.
3. Remove corrupted data.
4. Develop, construct, test, and maintain data architectures.

## Big Data:
#### * **Very large data**
- You have to think about how to deal with its size.
- Traditional methods don't work on it due to its size.

### Big Data is usually categorized by the **5 Vs**:
1. Volume **(how much?)**
2. Variety **(what kind?)**
3. Velocity **(how frequent?)**
4. Veracity **(how accurate?)**
5. Value **(how useful?)**
