![Unit Tests](https://github.com/siegelzero/satisfier/workflows/Unit%20Tests/badge.svg)


# Satisfier
Satisfier is a package for finding solutions to Constraint Satisfaction Problems (CSPs), supporting variables over finite domains with a rich and flexible set of constraints and combination methods.
The package includes enumerative methods that explore the entire search space of a problem, as well as a variety of heuristic methods to search for solutions to larger problem instances.

Satisfier can be used for a variety of mathematical tasks.
* Enumerating solutions to equations or systems of equations
* Searching for solutions to CSPs, or proving that no solutions exist
* Constructing combinatorial structures
* Graph coloring
* Many more!

### Installation

```bash
pip install satisfier
```

### Example Usage

Below is a system that has a small Pythagorean triple as a solution.

```python
from satisfier.system import ConstraintSystem
from satisfier.enumerative import search

C = ConstraintSystem()
x = C.variable_set

C.add_constraints([
    x[0] < x[1],
    x[0]**2 + x[1]**2 == x[2]**2
])

for variable in C.variables:
    C.set_domain(variable, range(1, 6))

search(C)
```

Satisfier can be used to enumerate combinatorial structures.
A *derangement* is a permutation that has no fixed points.
We can count the derangements of the `n` symbols `0, 1, ..., n - 1` with `n = 10` as follows.
```python
from satisfier.system import ConstraintSystem
from satisfier.enumerative import solutions

C = ConstraintSystem()
position = C.variable_set

n = 10
for i in range(n):
    C.set_domain(position[i], range(n))

for i in range(n):
    C.add_constraint(position[i] != i)

C.all_different(C.variables)

sum(1 for _ in solutions(C))
```
