# COMP3121 Assignment 2 Question 4

Andrew Xie, z5317337

**You are given $n$ stacks of blocks. The $i^{th}$ stack contains $h_i \gt 0$ identical blocks. You are also able to move for any $i \leq n - 1$ any number of blocks from stack $i$ to stack $i+1$. Design an algorithm to find out in $O(n)$ time whether it is possible to make the sizes of stacks strictly increasing. (For example, 1,2,3,4 are strictly increasing but 1,2,2,3 are not). The input for your algorithm is an array $A$ of length $n$ such that $A[i] = h_i$. Note that you are not asked to actually move the blocks, only to determine if such movements exists or not.** 

This question can be solved using a greedy strategy. Since we are allowed to move as many blocks as we want from a stack to the next stack, aiming to create the smallest sequence of strictly increasing number of blocks (1, 2, 3, ..., k) gives the highest chance of rearranging into a sequence of blocks that is strictly increasing. This is because we are maximising the number of "carryover" blocks which can be added to a stack of blocks if it does not have enough blocks to be able to maintain a strictly increasing sequence. Let $0 \leq i \leq n-1$ denote the index of stack $h_i$. Iterating over the list of $n$ stacks of blocks in $O(n)$ time, we aim to make each $h_i$ be of size $i$, carrying any extra blocks from stack to stack and filling in with these carryover blocks when necessary. If at any point we do not have enough blocks to maintain the minimum strictly increasing sequence, then it is not possible to make the sizes of stacks strictly increasing, and thus no possible movements exist. Otherwise, it is possible to create a strictly increasing sequence of stacks by moving blocks.

<u>Pseudocode:</u>

```pseudocode
carryover = 0
FOR i, h_i IN enumerate(A):
	IF h_i + carryover < i THEN return False;
	ELSE carryover <- carryover + h_i - i;
return True;
```

