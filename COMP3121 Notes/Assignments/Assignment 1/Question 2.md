# COMP3121 Assignment 1 Question 2

Andrew Xie, z5317337

**You are given a set of $n$ fractions of the form $\frac{x_i}{y_i}$ $(1 \leq i \leq n)$, where $x_i$ and $y_i$ are positive integers. Unfortunately, all values $y_i$ are incorrect; they are all of the form $y_i = c_i + E$ where numbers $c_i \geq 1$ are the correct values and $E$ is a positive integer (equal for all $y_i$). Fortunately, you are also given a number $S$ which is equal to the correct sum $S = \sum_{i=1}^n \frac{x_i}{c_i}$. Design an algorithm which finds all the correct values of fractions $\frac{x_i}{c_i}$ and which runs in time $O(n \log \min\{y_i: 1\leq i \leq n\})$.**

Given fractions of the form $\frac{x_i}{y_i}$, in order to find all the correct values of fractions $\frac{x_i}{c_i}$, we need to find the value of constant $E \geq 1$ such that $\sum_{i=1}^n \frac{x_i}{c_i} = \sum_{i=1}^n \frac{x_i}{y_i - E} = S$ since $y_i = c_i + E$. $E$ is also bounded by $\min\{y_i : 1 \leq i \leq n\}$ since we want $c_i = y_i - E$ to be a positive integer for all $c_i, y_i$. Hence, $1 \leq E \leq \min\{y_i : 1 \leq i \leq n\}$. 

We can more efficiently find the correct value for $E$ in this range with a binary search, using the sum of the fractions with $E$ subtracted from the denominators $y_i$ as an indication of whether we are closer to our goal $S$, which is the sum of the fractions with the correct $E$ subtracted from the denominators. Subtracting $E$ from the denominators will make each fraction larger, causing the overall sum of the positive fractions to increase. Binary search has a logarithmic worst case time complexity, so there is a worst case time complexity of $O(\log \min\{y_i : 1 \leq i \leq n\})$. Calculating the sum of the $n$ fractions in each step of the binary search takes $O(n)$. Hence, the overall complexity of the algorithm is $O(n \log \min\{y_i: 1 \leq i \leq n\})$.

<u>Pseudocode:</u>

```pseudocode
left <- 1;
right <- min(y_i) - 1;
WHILE left <= right:
    E <- (left + right) / 2;
    guess_sum = sum of fractions x_i / (y_i - E);
    IF S == guess_sum, THEN return E;
    ELSE IF S < guess_sum, THEN lower guess for E with right <- E - 1;
    ELSE IF S > guess_sum, THEN increase guess for E with left <- E + 1;
return False;
```

