# SDLC Design: Software Complexity

Essential - complexity that is inherent to the problem - fundamentally can't be removed, but can be managed with good software design

Accidental - complexity that is not inherent to the problem (e.g. generating/parsing data in specific formats) - can be somewhat mitigated by engineering decisions (e.g. smart use of libraries, standards etc) - hard to remove entirely

Coupling - a measure of how closely connected different software components are - 'loose' or 'tight', e.g. web applications tend to have a frontend that is loosely coupled from the backend (big reliance on each other)

Cohesion - degree to which elements of a module belong together - elements belong together if they're somehow related - 'low' or 'high', e.g. other.py from project

Cyclomatic complexity - a measure of the branching complexity of functions - computed by counting the number of linearly-independent paths through a function

- To compute, convert function into a control flow graph and calculate the value of the formula `V(G) = e - n + 2` (e = #edges, n = #nodes)

Examples:















