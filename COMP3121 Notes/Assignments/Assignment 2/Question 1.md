# COMP3121 Assignment 2 Question 1

Andrew Xie, z5317337

**You are given a sequence of $n$ songs where the $i^{th}$ song is $l_i$ minutes long. You want to place all of the songs on an ordered series of CDs (e.g. $CD_1, CD_2, CD_3, ... CD_k$) where each CD can hold $m$ minutes. Furthermore,**

**a) The songs must be recorded in the given order, song 1, song 2, ..., song $n$**
**b) All songs must be included**
**c) No song may be split across CDs**

**Your goal is to determine how to place them on the CDs as to minimise the number of CDs needed. Give the most efficient algorithm you can to find an optimal solution for this problem, prove the algorithm is correct and analyse its time complexity.** 

Given the three restrictions, a greedy approach to solving this problem would be to try and place as many songs on each CD as possible, only placing songs on a new CD if the song is unable to be completely fit on the previous CD. Going through the $n$ songs and determining whether to record each song on the previous CD or on a new CD can occur in $O(n)$ time. This algorithm provides an optimal solution to this problem, since it ensures that each CD used is filled up as much as possible, only recording songs on a new CD if including it would otherwise exceed the limit of $m$ minutes on the same CD. 

Suppose we have an optimal solution which differs from the greedy solution. This means that there exists at least one song $s$ which was placed on $CD_{j+1}$ instead of $CD_j$, even though there would have been enough space to fit $s$ on $CD_j$. Following the greedy approach and recording song $s$ on $CD_j$ instead, it is evident that one of the following outcomes may occur:

1. If there are no songs following $s$, then the greedy solution will provide a better solution than the optimal solution.
2. If the songs following $s$ all remain unmoved on the same CD in the same order, then the number of CDs needed in the greedy solution will be the same as from the optimal solution.
3. If the songs following $s$ are also recorded using a similar greedy approach, then the number of CDs needed in the greedy solution will be either better or the same as the optimal solution.

Since the solution produced by the greedy algorithm is no worse than any optimal solution, it is hence optimal and correct. 

<u>Pseudocode:</u>

```pseudocode
CDs <- empty list;
current_CD = new CD();
FOR song IN songs:
	IF current_CD.length + song.length > m THEN
		CDs.append(current_CD);
		current_CD = new CD();
  ELSE
  	current_CD.record(song);
return CDs;
```

