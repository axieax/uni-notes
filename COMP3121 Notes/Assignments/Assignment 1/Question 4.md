# COMP3121 Assignment 1 Question 4

Andrew Xie, z5317337

**You are given an array consisting of a sequence of $2^n-1$ consecutive positive integers starting with 1 except that one number was skipped; thus the sequence is of the form $1,2,3,...,k-1,k+1,...2^n$. You have to determine the missing term accessing at most $O(n)$ many elements of $A$.** 

Suppose array $S = s_1, s_2, ..., s_m$ consists of a sequence of $m$ consecutive positive integers without any skipped numbers. Then we find that the middle term will always be the average of the first and last elements of $S$ (expected average value), defining middle term by the following:

​	i) IF $m$ is even, THEN the middle term will be the average of the two middle elements ($s_{\frac{m+1}{2} - 1}$ and $s_{\frac{m+1}{2}}$).
​	ii) ELSE IF $m$ is odd, THEN the middle term is the middle element $s_{\frac{m+1}{2}}$.

This property can be extended to all partitions of $S$ since $S$ consists of consecutive positive integers. We can use this property to determine whether the skipped element $k$ lies in the lower or upper half of any partition of array $A$, which consists of a sequence of the form $1,2,3,...,k-1,k+1,...2^n$. It can be seen that for any partition $P$ of $A$ containing $k$, the last element of $P$ would be 1 greater than it should have been, causing the expected average value of the first and last elements of $P$ to be greater by $0.5$. If the middle term of $P$ is greater than this expected average, this indicates that $k$ is located in the lower half of $P$ since an earlier skipped number would cause the middle term to be 1 greater than it should have been, and thus $0.5$ greater than the expected average value. Similarly, if $k$ was located in the upper half of $P$, the expected average value would be $0.5$ greater than the middle term. Also, the middle term equaling the expected average value of $P$ indicates that the middle term is the missing number $k$.

Recursively splitting each partition into halves and binary searching for $k$ in these partitions (and including the nearest middle element in each new partition), the skipped number $k$ can be located in an average logarithmic computational complexity. For each of the $log(2^n-1) = n$ partitions (at most), only the middle element(s) needs to be accessed to obtain the middle term to be compared with the known lower and highest elements of the partition. Hence, at most $O(n)$ many elements of $A$ need to be accessed in order to find the missing number $k$. 

Here is the pseudocode for the described algorithm. Note that here I use comparisons between the middle term and the expected average value instead of comparing differences of 0.5, which generalises the algorithm for finding the missing number in an ascending sequence of integers spaced evenly apart and not necessarily consecutive (such as a pairwise difference of 2 instead of 1).

```pseudocode
WHILE skipped element not found in a partition P of A:
    middle term <- average of middle elements if P is even or
                   middle element if P is odd;
    expected average <- average of the first and last elements of P;
    IF middle term == expected average, THEN return middle term;
    ELSE IF middle term < expected average, THEN
        search with P <- upper partition of P;
    ELSE IF middle term > expected average, THEN
        search with P <- lower partition of P;
```

