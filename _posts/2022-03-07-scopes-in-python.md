---
layout: post
title: Scopes
subtitle: Global, Local, and Built-in
categories: python, scope
tags: [python, scope]
mermaid: true

---

# What does scope mean?
- The scope of an identifier name binding – an association of a name to an entity, such as a variable – is the region of a computer program where the binding is valid – the name can be used to refer to the entity. Such a region is referred to as a "scope block". 
- In other parts of the program, the name may refer to a different entity (it may have a different binding), or to nothing at all (it may be unbound).

# Types of scopes:

1. **Built-in scope:** names in pre-defined built-ins module (such as print and sum).
2. **Global scope:** binding is done in the main body of a Python script. 
3. **Enclosing scope (encloses a Nested Function).** 
4. **Local scope:** binding is done inside a Python function. **(can't be used outside the function block)**

## LEGB Rule:

<div class=mermaid>

flowchart LR;
    local["(1) Local Scope"] --> enc["(2) Enclosing Scope"]
    enc --> global["(3) Global Scope"]
    global --> builtin["(4) Built-in Scope"]

    style local fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
    style enc fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
    style global fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
    style builtin fill:#8fffd4,stroke:#000,stroke-width:2px,color:#000
</div>

- The order **L**ocal, **E**nclosing, **G**lobal, **B**uilt-in is the order of precedence for scope resolution. 
- This means that Python searches for the value of an identifier name in each of these namespaces in turn.


### Some notes on the LEGB rule:
- Identifier names defined in a **local scope** are given a priority over ones defined in the **global scope** by **default** in **Python** (if the same name exists in both local & global scopes).
- Identifier names defined in the **global scope** are given a priority over ones defined in the **built-in scope** by **default** in **Python** (if the same name exists in both global & built-in scopes).
- To use identifier names defined in the global scope inside a local scope, the **global** keyword is used before the identifier name.
- The **global** keyword is also used inside functions to define a global identifier name.
- The **nonlocal** keyword is used inside nested functions to access and define a identifier names in the **enclosing scope**.



