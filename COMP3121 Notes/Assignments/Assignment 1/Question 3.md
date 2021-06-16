# COMP3121 Assignment 1 Question 3

Andrew Xie, z5317337

**You are given an array $A$ consisting of $n$ positive integers, not necessarily all distinct. You are also given $n$ pairs of integers $(L_i, U_i)$ and have to determine for all $1 \leq i \leq n$ the number of elements of $A$ which satisfy $L_i \leq A[m] \leq U_i$ by an algorithm which runs in time $O(n log n)$.**

Sorting the integers in an array first allows for more efficient lookups for determining the number of elements which lie within a range (between $L_i$ and $U_i$ for all $1 \leq i \leq n$ query pairs). Sorting the $n$ integers in the array $A$ can be done in $O(n \log n)$ (worst case) with merge sort. In a sorted array, the number of elements between $L_i$ and $U_i$ can be found by finding the differences between the indices for the first element no less than $L_i$ and the first element strictly greater than $U_i$, for all $1 \leq i \leq n$.

Such a lookup for both elements can be efficiently computed with a binary search for each of the $n$ queries, resulting in a worst case time complexity of $O(n \log n)$ since binary search has a logarithmic complexity. The algorithm must ensure $L_i$ is the lowest it can go, and $U_i$ is the highest it can go. For $L_i$, even if $L_i$ is found in the sorted array, the preceding elements will need to be checked to ensure that none of them are also no less than $L_i$ (i.e. duplicates of $L_i$). Similarly, if an element strictly greater than $U_i$ is found, it must also be the first element strictly greater than $U_i$. By doing so, you end up with an element at the beginning of the range and the other just after the end of the range. The difference between the indices of these elements represents the number of elements in the array which lie within the specified range.

<u>Pseudocode:</u>

```pseudocode
Sort A with merge sort;
FOR each of the queries:
    start <- binary search to find index of first element no less than L_i;
    end <- binary search to find index of first element
           strictly greater than U_i;
    num_elements <- end - start;
```

