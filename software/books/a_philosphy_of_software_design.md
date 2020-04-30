A Philosphy of Software Design
------------------------------

The most fundamental problem in CS is problem decomposition: How to take a complex problem and break it up in to smaller, more manageable chunks. This book is all about reducing complexity.


*Complexity* defined for this book: Anything related to the structure of a software system that makes it hard to understand and modify the system. It can take many forms, hard to understand the code, hard to implement small changes, hard to understand how different parts of the system interact with each other etc.

Complexity of a system can be defined in a mathematical way: C = E _p_(c _p_ t _p_  ) 
Overall complexity (C) is determined by the complexity of each part *p*  (c _p_) weighted by the fraction of time developers spend working on that part (t _p_).

 If you write a piece of code and it seems simple to you, but others think it is complex, then it is complex.

One of the most important goals of good design is for a system to be obvious.

### Symptoms of complexity

#### Change amplification

- A goal of good design is to reduce the amount of code that is affected by each design decision, so design changes don't require very many code modifications

#### Cognitive load

- How much a developer needs ot know in order to complete a task
- _Sometimes an approach that requires more lines of code is actually simpler, because it reduces cognitive load_

#### Unknowns unknowns

- It is not obvious which pieces of code must be modified to complete a task.


### Causes of complexity

Complexity is caused by two things _dependencies_ and _obscurity_

#### dependency

A dependency exists when a given piece of code cannot be understood and modified in isolation.

Dependencies are a fundamental part of software design and can't be completely eliminated. We intentionally introduce dependencies as a part of software design process. One of the goals of software design is to reduce the number of depencies and to make the dependencies that remain as simple and obvious as possible

#### Obscurity

Obscurity occurs when important information is not obvious.
- variable so generic that it doesn't carry much useful information
- documentation for a variable might not specify units

Obscurity is often associated with dependency where it is not obvious that a dependency exists


*Complexity is incremental* 



### Development mindeset

One of the most important elements of good software design is the mindset you adopt when you approach a programming task. Many orgs focus on getting features working as quickly as possible. If you want good design, you must take a more strategic approach where you invest time to produce clean designs and fix problems.

#### Tactical programming

The main focus is to get something working, sucha s a new feature or a bug fix. However, tactical programming makes it nearly impossible to produce a good system design. The problem with this approach is that it's short sighted. This mindset makes less time for planning for the future. This is how systems become complicated

#### Strategic programming

*First step towards becoming a good software designer is to realize that working code isn't enough* It's not acceptable to introduce unnecessary complexities to complete your task faster. The most important thing is long term structure of a system. Investment mindset.


### Modules should be deep

One of the most important techniques for managing software complexity is to design systems so that developers only need to face a small fraction of the overall complexity at any given time. This is called modular design.

*Modular Design* a software system is decomposed into a collection of modules that are relatively independent. Module scan take many forms, such as classes, subsystems, or services. In an ideal world, each module would be completely independent of the others. A developer could work in any of the modules without knowing anything about any of the other modules. In this world the complexity of a system would be the complexity of its worst module.

Modules must work together by calling each other's functions or methods. As a result, module smust know something about the other. There will be dependencies between modules: if one module changes, other modules may need to change to match. ie a function signature.o

In order to manage dependencies, we think of each module in two parts: an _interface_ and an _implementation_.

The best modules are those whose interfaces are much simpler than their implementations. Such modules have two advantages:
1. A simple interface minimizes the complexity that a module imposes on the rest of the system.
2. If a module is modified in a way that does not change its interfaces, then no other module will be affected by the modification

#### Abstractions

An abstraction is a simplified view of an entity, which omits unimportant details. Abstractions are useful because they make it easier for us to think about and manipulate complex things.

An Abstraction can go wrong in two ways:
1. It can include details that are not really important, this makes it more complicated than necessary, increasing cognitive load on a developer.
2. It can omit details that are really important, this results in obscurity: developers looking at the abstraction won't have all the information they need to use it correctly.

#### Deep Modules

The best modules are those that provide powerful functionality yet have simple interfaces. A deep modules is a good abstraction because only a small fraction of its internal complexity is visible to users. Module depth is a way of thinking about cost versus benefit. *The benefit provided by a module is its functionality. The cost of a module is its interface*

#### Shallow Modules

A shallow module is one that has a relatively complex interface for the functionality it provides.

#### Classitis


Classes should be small approach, which ends up accumulating many classes with many interfaces, increasing cognitive load etc. 

*Interfaces should be designed to make the common case as simple as possible*

### Information Hiding and Leakage

#### Information Hiding

Each module should encapsulate a few pieces of knowledge, which represent design decisions. This reduces complexity in two ways:
1. The interface reflects a simpler, more abstract view of the module's functionality and hides the details. This reduces the cognitive load
2. Information hiding makes it easier to evolve the system

When designing a new module, you should think carefully about what information can be hidden in that module

#### Information Leakage

This occurs when a design decision is reflected in multiple modules. This creates a dependency between modules, any change to that deisgn decision will require changes to all of the involved modules. _If a piece of information is reflected in the interface for a module, then by definition it has been leaked._

Ask yourself: How can I reorganize these classes so that this particular piece of knowledge only affects a single class?"

#### Temporal decomposition

Wehn designing modules, focus on the knowledge that's needed to perform each task, not the order in which tasks occur.

#### Lessons by example

- Information hiding can often be improved by making a class slightly larger
- Avoid exposing internal data structures as much as possible
- Make the common case as simple as possible
- Be careful of *Overexposure*: If the API of a commonly used feature forces users to learn about other features that are rarely used, this increases cog load.
- Information hiding within classes:
  - Try to design the private methods within a class so that each method encapsulates some information or capability and hides it from the rest of the class
  - Try to minimize the number of places where each instance variable is used 
- Information hiding only makes sense when the information being hidden is not needed outside its module. If the information is needed outside the module then you must not hide it.

### General Purpose vs Specialized Module

General purpose seems consistent with investment mindset. However it's hard to predict the future uses of a module so features that were implemented might never be used. Some might argue it's better to specialize it for the present usage, and expand it to be more general if needed. This refactoring would be consistent to incremental development

*Make classes somewhat general purpose* the module should reflect your current needs, but the interface should not. The interface should be easy to use for today's needs but not specifically tied to them. This approach leads to simpler and deeper interfaces.

Given this example for a text editor
```
void delete(Cursor cursor);
void backspace(Cursor cursor);
void deleteSelection(Selection selection);
```

This could be better served as:
```
void insert(Position position, String newText);
void delete(Position start, Position end);
```

#### Questions to ask yourself

1. What is the simplest interface that will cover all my current needs
  - if you reduce the number of methods in an API without reducing its overall capabilities, then you are probably creating  more general-purpose methods.
  - If you have to overcomplicate the interface to achieve the above, you probably aren't helping
2. In how many situations will this method be used
  - If a method is designed for one particular use, that is a red flag that it may be too special purpose. See if you can replace several special-purpose methods with a single general-purpose method
3. Is this API easy to use for my current needs
  - If you have to write a lot of additional code to use a class for your current purpose, that's a red flag that the interface doesn't provide the right functionality.

