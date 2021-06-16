# COMP3121 Assignment 1 Question 1

Andrew Xie, z5317337

**You are given an array $A$ of $n$ distinct positive integers.**
**a) Design an algorithm which decides in $O(n^2log n)$ (in the worst case) if there exists four distinct integers $m,s,k,p$ in A such that $m^2+s=k+p^2$.**

Rearranging the condition $m^2 + s = k + p^2$ to $m^2 + s = p^2 + k$ for some distinct positive integers $m,s,p,k$, we find that both sides of the equation have a similar form. This means we can reduce the problem down by iterating through the permutations of element pairs, calculating and storing values of the form $pair[1]^2 + pair[2]$, then finding whether there are any duplicates in the stored values corresponding to four distinct integers. Permutations of element pairs can be obtained by pairing each of the $n$ elements with the other $n-1$ elements. The resulting calculation for each $pair[1]^2 + pair[2]$ can then be stored in an $n(n-1)$ array, with $O(n^2)$ elements. This value should be stored within a tuple as its first element, as well as the two integers $pair[1]$ and $pair[2]$ used in the calculation of this value.

Duplicate elements in the array of values can be easily found after sorting the array. Merge sort has a complexity of $O(N \log N)$, so with $O(n^2)$ elements, the array can be sorted with merge sort in a worst case time complexity of $O(n^2 \log (n^2)) = O(2 n^2 \log n) = O(n^2 \log n)$. Duplicate values can now be found as consecutive elements when traversing the sorted array in $O(n^2)$. Since we stored the integers used in the calculation for the values within the tuple, we can use this to verify whether there exists two pairs of duplicate values which were created from four distinct integers. As a result, this algorithm allows us to find whether there exists four distinct integers $m,s,k,p \in A$ such that $m^2+s=k+p^2$ in $O(n^2 \log n)$.

<u>Pseudocode:</u>

```pseudocode
permutations <- empty list;
FOR index i of A:
    FOR index j of A:
        if i != j:
            Add (A[i], A[j]) to permutations;

values <- empty list;
FOR pair in permutations:
    value <- pair[1] ^ 2 + pair[2];
    Add (value, pair[1], pair[2]) to values;

Sort values with merge sort;
FOR tuple(value, x, y) of values:
    IF value seen before (as a duplicate) and
    (x and y both not used to calculate duplicate values before),
        THEN return True;
return False;
```

**b) Solve the same problem but with an algorithm which runs in the expected time of $O(n^2)$.**

An algorithm running in the expected time of $O(n^2)$ is similar to the one used in part a). Firstly, obtain the permutations similarly to part a), resulting in $O(n^2)$ elements. For each of these permutation pairs, we can calculate the $pair[1] ^ 2 + pair[2]$ value similarly to before. However, instead of storing this to a new array, we can store it in a hash table instead, with the 'key' being the calculated value and the 'value' representing the integers used to calculate this value. Now we don't have to worry about sorting to find duplicate items. Checking whether there exists four distinct integers in at least two pairs that have the same key (calculated value) will allow us to solve the problem in $O(n^2)$. 

<u>Pseudocode:</u>

```pseudocode
permutations <- empty list;
FOR index i of A:
    FOR index j of A:
        if i != j:
            Add (A[i], A[j]) to permutations;
lookup <- empty hash map from calculated_value
          to list of permutation pairs used to calculate it;
FOR pair in permutations:
    calculated_value <- pair[1] ^ 2 + pair[2];
    Add pair to lookup[calculated_value];
FOR key, value in lookup:
    IF length of value array > 1 and there exists 4 distinct integers
    between at least two pairs in value, THEN return True;
return False;
```


