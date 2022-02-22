---
layout: post
title: Data Pipelines
subtitle: Automation of Data Flow
categories: dataengineering datapipelines automation
tags: [data, engineering, pipelines, automation, dataflow]
mermaid: true
---

## What is a Data Pipeline?
- It's a series of **data processing steps**
- Each step delivers an **output** that is the **input** to the next step until the pipeline is complete
- The steps are run in **parallel** in some cases.
- If the data is not currently loaded into the data platform, it's ingested at the beginning of the pipeline.

| **Key Elements in a Data Pipeline:**|
| --- | 
| * Data Source(s) |
| * Processing Step(s) |
| * Data Sink (destination) |

## Example of a Data Pipeline:
<div class="mermaid">
flowchart LR;
    A("Data Source") --"Output | Input"--> B("Operation 1");
    B --"Output | Input"--> C("Operation 2");
    C --"Output | Input"--> D("Operation 3");
    D  --"Output" -->  E("Data Sink");  
    style A fill:#d90ba9,stroke:#000,stroke-width:2px,color:#fff
    style B fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    style C fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    style D fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    style E fill:#d90ba9,stroke:#000,stroke-width:2px,color:#fff
</div>
## Why do Data Pipelines exist?
<div class="mermaid">
graph LR;
    P(("Pipeline"));
    A["Automate flow of data <br> from one station to the next"];
    E["Efficient Data Flow"];
    P --- A;
    A--"Resulting in"--> E;
    E--> U;
    E--> Acc;
    E-->Rel;
    subgraph Provides Data <br> Scienties with:
        U["Up-to-Date Data"];
        Acc["Accurate Data"];
        Rel["Relevant Data"];
    end

    classDef greenStlye fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
    classDef orangeStyle fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    classDef pinkStyle fill:#d90ba9,stroke:#000,stroke-width:2px,color:#fff
    
    class Acc,U,Rel greenStlye
    class P pinkStyle
    class A,E orangeStyle

</div>
## Automation

<div class="mermaid">
graph TD;
    classDef pinkStyle fill:#d90ba9,stroke:#000,stroke-width:2px,color:#fff
    classDef orangeStyle fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    classDef greenStlye fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
    
    A --> Ext["Extracting Data"];
    A --> Trs["Transforming Data"];
    A --> Comb["Combining Data"];
    A --> Validating["Validating Data"];
    A --> Loading["Loading Data"];
    
    class A pinkStyle;
    class Ext,Trs,Comb,Validating,Loading orangeStyle;
    A(Automation);
</div>

| Automation Reduces: |
|---|
| - Human Intervention|
| - Errors |
| - Time needed for Data to flow |

## ETL Framework:
<div class="mermaid">
graph LR;
    classDef pinkStyle fill:#d90ba9,stroke:#000,stroke-width:2px,color:#fff
    classDef orangeStyle fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    classDef greenStlye fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
    
    Ext["Extract Data"] --> Trs["Transform Data"];
    Trs --> Load["Load Data"];
    class Ext,Trs,Load greenStlye;   
</div>


## Notes on Data Pipelines:
1. Data Pipelines move data from one system to another.
2. They may follow **ETL**. 
3. Data may not be **T**ransformed.
4. Data may not be **L**oaded directly.

