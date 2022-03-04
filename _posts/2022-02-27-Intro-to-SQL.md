---
layout: post
title: Introduction to SQL
subtitle: Structured Query Language
categories: dataengineering databases SQL
tags: [data, engineering, databases, SQL]
mermaid: true
---
## What is SQL?
- **SQL** stands for **S**tructured **Q**uery **L**anguage.
- SQL is the industry standard Relational Database Management System **(RDBMS)**.
- SQL allows users to access many records at once, group them, filter them, or aggregate them.
- SQL is a **high-level** language: SQL is Easy to write and understand.

## Data Scientists vs. Data Engineers - SQL:

| Data Engineers | Data Scientists |
|---|---|
| Create & Maintain DBs | Query from DB |

## The Basics:

#### Important Notes:
- **Columns** are called **Fields**.
- **Rows** are called **Records**.
- SQL is **not** case-sensitive.
- SQL commands are written in CAPS according to convention.

### Some SQL Commands:
<div class="mermaid">
flowchart LR;
    root["Commands"]
    style root fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000

    
    root --> create["CREATE"]
    style create fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

    subgraph CREATE:
        create --> create1["CREATE DATABASE database_name"]
        create --> create2["CREATE TABLE table_name"]
        create --> create3["CREATE INDEX index_name ON table_name(col1,col2,...)"]
        create --> create4["CREATE UNIQUE INDEX index_name ON table_name(col1,col2,...)"]
    end
    
    style create1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style create2 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style create3 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style create4 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000

    subgraph CREATE example:
        create2-->crEx["CREATE TABLE family(id INT, name VARCHAR[20],birthdate DATE)"]
        crEx--"Creates an empty table with columns"-->crRes["| id | name | birthdate "]
    end
    style crEx fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000

    root--> ins["INSERT INTO"]
    style ins fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

    subgraph INSERT INTO:
        ins --> ins1["INSERT INTO table_name VALUES(val1,...last_val)"]
        ins --> ins2["INSERT INTO table_name(field1,...) VALUES(val1,...)"]
    end

    style ins1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style ins2 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000

    subgraph INSERT INTO example:
        ins1 --"Inserts values for all fields"--> ins1Ex["INSERT INTO family VALUES(1,'Mohammed','1995-03'25')"]
        ins1Ex--adds record to family-->ins1Res["| 1 | 'Mohammed' | '1995-01-01' |"]
        
        ins2 --"Inserts values for specific fields"--> ins2Ex["INSERT INTO family(name) VALUES('Mohammed')"]
        ins2Ex--adds record to family-->ins2Res["| NULL | 'Mohammed' | NULL |"]
    end
    style ins1Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000
    style ins2Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000


    root --> sel["SELECT"]
    style sel fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    
    subgraph SELECT:
        sel --> sel1["SELECT col_name FROM table_name;"]
        sel --> sel2["SELECT col1_name,col2_name FROM table_name;"]
        sel --> sel3["SELECT * FROM table_name;"]
    end

    style sel1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style sel2 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style sel3 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000

    subgraph SELECT example:
        sel1 -- "Selects one field only" --> sel1Ex["SELECT name FROM family;"]
        sel2 -- "Selects multiple fields" --> sel2Ex["SELECT name,birthdate FROM family;"]
        sel3 -- "Selects all fields" --> sel3Ex["SELECT * FROM family;"]
    end
    style sel1Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000
    style sel2Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000
    style sel3Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000


    root-->as["AS"]
    style as fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

    subgraph AS:
        as --> as1["SELECT name AS first_name FROM family;"]
        as --> as2["SELECT name AS first_name,birthdate AS bd FROM family;"]

    end
    style as1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style as2 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    
    subgraph AS Notes:
        as1-->note1["Renames a col or table with an alias"]
        as1-->note2["Only exists for duration of query"]
        
    end
    style note1 fill:#ffccff,stroke:#000,stroke-width:2px,color:#000
    style note2 fill:#ffccff,stroke:#000,stroke-width:2px,color:#000
    

    root-->whr["AS"]
    style whr fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

    subgraph WHERE:
        whr --> whr1["SELECT ... FROM family WHERE condition;"]
    end

    style whr1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    
    
    subgraph WHERE example:
        whr1-->whrEx1["SELECT * FROM family WHERE name = 'Mohammed';"]
        whr1-->whrEx2["SELECT * FROM family WHERE name = 'Mohammed' AND id < 3;"] 
    end

    style whrEx1 fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000
    style whrEx2 fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000
    
    root-->use["USE"]
    style use fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

    use-->useEx["USE db_name; CREATE TABLE table_name"]
    style useEx fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000


    root-->drop["DROP"]
    style drop fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000
    
    subgraph DROP:
        drop --> drop1["DROP DATABASE db_name"]
        drop --> drop2["DROP TABLE table_name"]
        drop --> drop3["DROP INDEX index_name ON table_name"]
    end

    style drop1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style drop2 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style drop3 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    
    subgraph DROP example:
        drop2 -- "Deletes entire table from DB" --> drop2Ex["DROP TABLE family"]
    
    end
    style drop2Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000
    

    root --> upd["UPDATE+SET"]
    style upd fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

    upd-->upd1["UPDATE table_name SET col1=val1,col2=val2,... WHERE condition;"]
    upd1-->upd1Ex["UPDATE family SET birthdate='1995-03-25' WHERE name='Mutasim';"]
    
    style upd1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style upd1Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000


    root --> del["DELETE"]
    style del fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

    subgraph DELETE FROM:
        del--"Removes specific record(s)"-->del1["DELETE FROM table_name WHERE condition;"]
        del--"Removes all records"-->del2["DELETE FROM table_name;"]
        
    end

    subgraph DELETE examples:
        del1-->del1Ex["DELETE FROM family WHERE name = 'Mohammed';"]
        del2-->del2Ex["DELETE FROM family;"]

    end

    style del1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style del2 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style del1Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000
    style del2Ex fill:#e6ccb3,stroke:#000,stroke-width:2px,color:#000

    root --> alt["ALTER"]
    style alt fill:#ffe18f,stroke:#000,stroke-width:2px,color:#000

    alt-->alt1["ALTER DATABASE db_name;"]
    
    style alt1 fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    

    subgraph ALTER TABLE table_name:
        alt--"Add column"-->alt2a["ALTER TABLE table_name ADD col_name <type>;"]
        alt--"Drop column"-->alt2b["ALTER TABLE table_name DROP COLUMN col_name;"]
        alt--"Change datatype of column"-->alt2c["ALTER TABLE table_name ALTER COLUMN col_name <new_type>;"]
    end
    style alt2a fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style alt2b fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000
    style alt2c fill:#d9ffb3,stroke:#000,stroke-width:2px,color:#000

</div>


