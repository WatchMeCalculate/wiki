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




