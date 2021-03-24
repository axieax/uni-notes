# Quiz 1 Part 2 Notes

Recall that for two sets A and B, the Cartesian product $A \times B$ is defined by the set $\{(a,b): a \in A, b \in B\}$. Let $A \subseteq \mathbb{R}^2$ be open in $\mathbb{R}^2$, and let $B \subseteq \mathbb{R}^2$ be open in $\mathbb{R}^2$. Prove, using definitions and first principles only, that $A \times B$ is open in $\mathbb{R}^3$. Argue carefully why every step is true.



Let $A \subseteq \mathbb{R}^2$ be open in $\mathbb{R}^2$. This means that for all $a \in A$, there exists a ball $B(a, \epsilon_1) \subseteq A$ for some $\epsilon_1 > 0$ (by definition). 

Similarly, let $B \subseteq \mathbb{R}$ be open in $\mathbb{R}$. This means that for all $b \in B$, there exists a ball $B(b, \epsilon_2) \subseteq B$ for some $\epsilon_2 > 0$ (by definition).

Let $C$ denote the Cartesian product $A \times B = \{(a,b): a \in A, b \in B\} \subseteq \mathbb{R}^2 \times \mathbb{R}$. The bijective subset $M = \{(x,y,z): (x,y) \in A, z \in B\}$ is also a subset of $\mathbb{R}^3$.

$M$ is open in $\mathbb{R}^3$ if for all $m \in M$, there exists a ball $B(m, \epsilon_3) \subseteq M$ for some $\epsilon_3 > 0$ (by definition). 

By letting $\epsilon_3$ be $min\{\epsilon_1, \epsilon_2\}$, this means that:

- $B(a, \epsilon_3) \subseteq A$
- $B(b, \epsilon_3) \subseteq B$
















$$
\mathbb{R}
$$




