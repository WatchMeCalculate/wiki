Modelica
========
- Declarative, statically type language for describing mathematical behaviour
- Encapsulates mathematheical behaviour into composable compoenent models
- Defers manipulation and solution of mathematical equations to the compiler
- Focuses on the problem statement, leaving users free to explore various solution methods


Basic Syntax:
 - models
   - High level "class"
 - partial model
   - "base class"
 - parameters
   - inputs into the model
 - initial equation: describes initial condition of equation
 - equation:
     - describe continuous equation
     - describe discrete equation
  - connector
     - how do components interact
     - no inputs or outputs: connectors describe how componenents "interact" with other componenents

Networks:
 Can compose systems hierarchically

 Under the hood:
 - puts the equations into a dense matrix
 - uses Equation Sorting (find equations where all variables are known except one)
 - becomes Lower triangular matrix
 - Index Reduction
 - State Selection
 - Tearing
 - Clock Partitioning


 Resources:
  - (Modelica book)[https://mbe.modelica.university/]
