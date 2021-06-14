# COMP3121 Assignment 1 Question 5

Andrew Xie, z5317337

**Read about the asymptotic notation in the review material and determine if $f(n) = O(g(n))$ or $g(n) = O(f(n)$ or both (i.e., $f(n) = \Theta(g(n)))$ or neither of the two, for the following pairs of functions:**

**a) $f(n) = log_2(n)$;	$g(n) = \sqrt[10]{n}$;**

By definition, $f(n) = O(g(n))$ if there exists positive constants $c$ and $n_0$ such that $0 \leq f(n) \leq c g(n)$ for all $n \geq n_0$. It can be observed that $0 \leq f(n), g(n)$ for all positive integers $n$. If we can show that there exists $c$ such that $\lim_{n \to \infty} f(n) \leq c \lim_{n \to \infty} g(n)$, then $f(n) = O(g(n))$. Substituting in for $f(n)$ and $g(n)$, the inequality $\lim_{n \to \infty} log_2(n) \leq c \lim_{n \to \infty} \sqrt[10]{n}$ can be rearranged to obtain:
$$
\lim_{n \to \infty} \frac{log_2(n)}{\sqrt[10]{n}} \leq c.
$$

L'Hopital's rule can be applied to this left-hand limit since the numerator and denominator both tend towards $\infty$ as $n \to \infty$. Differentiating both sides by $n$, the left-hand limit now becomes:
$$
    \lim_{n \to \infty} \frac{\frac{1}{n \ln 2}}{\frac{1}{10} n ^ {- \frac{9}{10}} }
    = \lim_{n \to \infty} \frac{\frac{10}{\ln 2}}{n ^ \frac{1}{10}} = 0.
$$
There exists a positive integer $c$ which is greater than or equal to the left-hand limit of 0. Thus, $f(n) = O(g(n))$.

Conversely, when trying to see if $g(n) = O(f(n))$, we find that after applying L'Hopital's Rule, the limit
$$
    \lim_{n \to \infty} \frac{\frac{1}{10} n ^ {- \frac{9}{10}} }{\frac{1}{n \ln 2}}
    = \lim_{n \to \infty} \frac{n ^ \frac{1}{10}}{\frac{10}{\ln 2}}
$$
approaches $\infty$ as $n \to \infty$. Since no positive integers exist which are greater than or equal to $\infty$, $g(n) \neq O(f(n))$. Hence, only $f(n) = O(g(n))$.

**b) $f(n) = n^n$;	$g(n) = 2^{n log_2(n^2)}$;**

By definition, $f(n) = O(g(n))$ if there exists positive constants $c$ and $n_0$ such that $0 \leq f(n) \leq c g(n)$ for all $n \geq n_0$. It can be observed that $0 \leq f(n), g(n)$ for all positive integers $n$. Substituting in for $f(n)$ and $g(n)$, we obtain the following inequality:
$$
    n ^ n \leq c 2^{n log_2(n^2)}.
$$
Applying a logarithm of base two to both sides of the inequality, we obtain:
$$
    \log_2 (n^n) \leq log_2 (c 2^{n log_2(n^2)})
$$
$$
    n \log_2 n \leq log_2 c + \log_2 (2^{n log_2(n^2)})
$$
$$
    n \log_2 n \leq log_2 c + 2 n log_2 n.
$$
Since $2 n \log_2 n \geq n \log_2 n$ for all $n \geq n_0$ for some positive constant $n_0$, there must exist a positive constant $c$ to satisfy this inequality. Thus, $f(n) = O(g(n))$.

Conversely, when trying to see if $g(n) = O(f(n))$ using a similar method, we find that:
$$
    2^{n log_2(n^2)} \leq c n ^ n
$$
$$
    2 n log_2 n \leq \log_2 c + n \log_2 n
$$
$$
    n log_2 n \leq \log_2 c.
$$
There does not exist any positive integer $c$ such that this inequality is true for all $n \geq n_0$ for some positive constant $n_0$. Hence, $g(n) \neq O(f(n))$ and only $f(n) = O(g(n))$.

**c) $f(n) = n^{1+sin(\pi n)}$;	$g(n) = n$;**

Note that $1 + \sin(\pi n) = 1$ for all $n$ since $n$ is a positive integer (or natural number) and the function $1 + \sin(\pi n)$ is periodic. Thus $f(n)$ can be simplified to $n^1 = n = g(n)$. Since $f(n) = g(n) = n \geq 0$ for all positive integers $n$, $f(n) = \Theta(g(n))$.
