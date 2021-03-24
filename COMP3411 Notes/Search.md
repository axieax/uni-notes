$$
A*: f(n) = g(n) + h(n)\\
UCS: f(n) = g(n)
$$

UCS is a special case of A\* where h(n) = 0. Heuristic h(n) only needs to underestimate distance, so 0 works.

Objective function $f(n) = (2-w)*g(n) + w*h(n), 0 \le w \le 2$

- w = 0: Uniform cost search
- w = 1: A\* search
- w = 2: Greedy search
- Optimal when $0 \le w \le 1$ -> equivalent to A\* search

