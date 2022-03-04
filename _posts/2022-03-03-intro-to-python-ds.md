---
layout: post
title: Introduction to Python Data Structures
subtitle: Lists, Tuples, Sets and Dictionaries
categories: dataengineering databases SQL
tags: [data, engineering, databases, SQL]
mermaid: true
---
## What is a data structure?
A **data structure** is a particular way of organizing data in a computer so that it can be used effectively.<br />


## Comparison between common Data Structures in Python:

| | Lists | Tuples | Sets | Dictionaries |
|---|---|---|---|---|
| Definition | ordered collection of data | ordered collection of data | unordered collection of data | unordered collection of data that stores data in key-value pairs |
| Implementation | Lists are declared with square braces. **[]** | Tuples are enclosed within parenthesis. **()** | Sets are represented in curly brackets. **{}** | Dictionaries are enclosed in curly brackets in the form of key-value pairs. **{key:value}** |
| Examples | list1 = [] **(empty List)**<br />list2 = [1,'some string',True] <br />list3 = list((1,'some string',True))**(argument passed to list method as Tuple)** | tup1 = () **(empty Tuple)** <br />tup2 = (1,'some string',True) <br />tup3 = tuple((1,'some string',True))**(argument passed to tuple method as Tuple)** | set1=set() **(empty Set)**<br />set2={1,'some string',True} <br />set3={(1,'some string',True)} | dict1={} **(empty Dictionary)** <br />dict2={"key1":1,"key2":"string","key3":True}<br />dict3=dict({"key1":1,"key2":"string","key3":True}) |
| Characteristics | Lists are mutable. | Tuples are immutable. | Sets are mutable and have no duplicate elements. | Dictionaries are mutable and have no duplicate keys. |





