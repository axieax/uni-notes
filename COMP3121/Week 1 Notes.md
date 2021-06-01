# Algorithm

- Collection of precisely defined steps that are executable using certain specified mechanical methods (not involving any creativity, intuition or even intelligence)
- Sequential deterministic - given as sequence of steps (assuming only one step can be executed at a time), and the action of each step gives the same result whenever the step is executed for the same input
- Mathematical proof that an algorithm designed terminates and returns a solution to the problem at hand - needed when not obvious by inspecting the algorithm using common sense

## Thieves loot splitting problem

Three Thieves:

```pseudocode
T1 makes a pile P1 which he believes is 1/3 of the whole loot;
T1 proceeds to ask T2 if T2 agrees that P1 ≤ 1/3;
If T2 says YES, then T1 asks T3 if T3 agrees that P1 ≤ 1/3;
	If T3 says YES, then T1 takes P1;
		T2 and T3 split the rest as in Problem 1.
	Else if T3 says NO, then T3 takes P1;
		T1 and T2 split the rest as in Problem 1.
Else if T2 says NO, then T2 reduces the size of P1 to P2 < P1 such that T2 thinks P2 = 1/3;
	T2 then proceeds to ask T3 if he agrees that P2 ≤ 1/3;
		If T3 says YES then T2 takes P2;
			T1 and T3 split the rest as in Problem 1.
		Else if T3 says NO then T3 takes P2;
			T1 and T2 split the rest as in Problem 1.
```

n thieves generalisation:

```pseudocode
T1 makes a pile P1 which he believes is 1/n of the whole loot;
T1 proceeds to ask T2 if T2 agrees that P1 <= 1/n;
If T2 says YES, then T1 asks the remaining thieves if they agree that P1 <= 1/n;
Else if T2 says NO, then T2 reduces the size of P1 to P2 < P1 such that T2 thinks P2 = 1/n;
	T2 proceeds to ask the remaining thieves sif they agree that P2 <= 1/n.
```





## Merge sort

```pseudocode
Merge-Sort(A,p,r):
if p < r
	then q <- floor((p + r) / 2)
		MERGE-SORT(A,p,q) // sort first half recursively
		MERGE-SORT(A,q+1,r) // sort second half recursively
		MERGE(A,p,q,r) // merge sorted halves
```





## Stable matching problem











