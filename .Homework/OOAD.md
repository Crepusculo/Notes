<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [L01](#l01)   
- [L02 UML](#l02-uml)   
- [Chapter 5. Evolutionary Requirements](#chapter-5-evolutionary-requirements)   
- [User Case](#user-case)   
- [Iteration](#iteration)   
- [Domain Models](#domain-models)   

<!-- /MDTOC -->
# L01
+ What is Analysis and Design
    + **Analysis** emphasizes an investigation of the problem rather than how a solution is defined
        + What
        + Not solution
        + investigation of problem
    + **Design** emphasizes a logical solution, how the system fulfils the requirements
        + How
        + logic solution about requirements
+ Division between A\&D is fuzzy
+ What is OOAD
    + Essence: to consider a problem domain and logic solution from the perspective objects
    + OOA: emphasizes finding and describing the objects -or concepts-- in the problem domain
    + OOD: emphasizes defining logical software objects (things, concepts, or entities) that have attributes and methods
+ OOA
    + Domain expert is always right to ...
+ OOA identifies
    + Concepts in the problem domain
    + Relationships among those concepts
    + Attribute of those concepts
+ OOD solution
    + Solution is defined based on findings of OOA phase
    + It includes definition of class methods that represent a logical software solution
    + New concepts or attr, relation among concepts are often discovered design phase.

```doc
 - Requirements - Concepts   - Collaborations -Code/Test
    analysis        model        Diagrams
 - Use case     - System      - Class Design
                  behavior       Diagrams
<------------------------------------------------------->
  Requirements | OO Analysis | OO Design | Construction
     Study     |             |           |
```

Define Usecase
---> Define domain model
---> Define interaction diagrams
    + sequence diagrams
    + communication diagram
---> Define design class diagrams

# L02 UML
+ UML
    + not a methodology
    + not a process
+ UML is
    + UML as sketch
        + Informal and incomplete diagram
        + create to explore difficult parts of the problem or solution space
    + UML as blue print
        + Relatively detailed design diagrams used either for
            1. reverse engineering to visualize and better understanding existing code
            2. code generation
    + UML as programming language
        + Complete executable specification of a software system in UML
        + Executable code will be automatically generated, but is not normally seen or modified by developers;
+ Iterative, Evolutionary, and Agile
+ What is Iterative
    + pass
+ What is Agile model
    + Adopting an agile method does not mean avoiding any modeling
    + The purpose of modeling and models is primarily to support understanding and communication, not documentation.
    + Do not model or apply the UML to all or moset of the software design.
    + Use the simplest tool possible.
# Chapter 5. Evolutionary Requirements
Requirements are capabilities and conditions to which the systems-and more broadly, the project must conform
> 需求是项目的功能和条件
- Challenges
    - Find
    - Communicate
    - Remeber
- Why effective management is critical
    - Requirement changes are inevitable
- FURPS+
-   - Functional
-   - Usability
-   - Reliablity
-   - Performance
-   - Supportabily
    - Packaging
    - Legal
    - Implementation
    - Interface
    - Operation
- How are Requirements organized in UP artifacts
    - UC model
    - Supplementray Specification
    - Glossary
    - Vision
    - Business Rules

# User Case
- A User Case
    - Brief
    - Casual
    - Fully-Dressed
<div class="html">
Name : start with a verb

+ Scope: The system under design
+ Level: "User Goal" or "subfunction"
+ Primary Actor
+ Stakeholders and interests
+ Preconditions
+ Postconditions
+ Main Success Scenario
+ Extensions
+ Special Requirements
</div>

+ How to find Use Cases
1. Choose the system boundary
2. Identify the primary actors
3. Identify goals for each actor
4. Difine use case that satisfy goals

+ Three ways to Find a useful UC
    - Boss
    - EBP
    - Size

# Iteration
# Domain Models
+ Domain model
    + illustrates meaningful conceptual classes in the problem domain
    + is a source of inspiration for design software objects
+ A domain model can be illustrated by a set of UML calss Diagrams
    + Domain objects or conceptual calsses
    + associations between conceptual classes
    + attributes of conceptual classes
>A domain model is the most important – and classic model in OOA

+ __Key idea:__ Domain model - A Visual Dictionary of Abstractions
    + only the noteworthy concepts are included
    + a simplified representation of the domain

+ What are the Sections of aa Contract
    + Operation
    + Cross Reference
    + Preconditions
    + Postconditions
+ System Operations
    + MSC SDL
    +
