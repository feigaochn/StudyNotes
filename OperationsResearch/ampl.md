- use `node` and `arc` for *pure* network linear programming as possible!

## general experience


### Initial solution

It is *always* valuable for the modeler to supply the algorithm with an initial solution, no matter how obvious it may appear to a human. Such a solution may provide a better starting point than what the algorithm can derive on its one, and algorithmic heuristics may perform better in the presence of an initial solution, regardless of the quality of its objective function value.

Common tactics to find a starting solutions:
- Provide an obvious solution based on specific knowledge of the model.
- Solve a related, auxiliary problem to obtain a solution.
- Use the solution from a previous solve for the next solve when solving a sequence of models.


### Numerical stability

Use indicators eliminates potentially large values (big M) from the matrix coefficients used to approximate an infinite value.
