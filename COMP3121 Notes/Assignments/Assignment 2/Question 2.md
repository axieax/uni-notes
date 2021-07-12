# COMP3121 Assignment 2 Question 2

Andrew Xie, z5317337

**At a trade school, there are $N$ workers looking for jobs, each with a skill level $x_i$. There are $P$ entry-level job openings, and the $i^{th}$ opening only accepts workers with a skill level less than or equal to $p_i$. There are also $Q$ senior job openings, the $i$ of which requires a skill level of at least $q_i$. Each worker can take at most one job, and each job opening only accepts a single worker. Your task is to determine the largest number of workers you can to jobs in time $O(N \log N + P \log P + Q \log Q)$.**

A greedy approach can be used to assign entry-level and senior job openings to $N$ workers. The main idea is to assign senior job openings to workers based on decreasing skill level, and then assign entry-level job openings to the remaining unassigned workers based on increasing skill level. Denote the list of workers as $W$, the list of entry-level job openings as $E$ and the list of senior job openings as $S$. Sort list $W$ by increasing skill level, list $E$ by increasing maximum skill level limit and list $S$ by decreasing minimum skill level requirement. With merge sort, each list can be sorted in $O(n \log n)$ time where $n$ is the size of each list. So respectively, sorting $W$ takes $O(N \log N)$, sorting $E$ takes $O(P \log P)$ and sorting $S$ takes $O(Q \log Q)$.

To assign senior job openings to workers, we can iterate over the workers from highest skill level to lowest (traversing the sorted list $W$ in reverse order) and seeing if each worker can be assigned to the next best available senior job opening which they can satisfy. Iterating this way means that if we encounter a worker who cannot satisfy a senior job opening requirement, the next workers will be less skilled and still unable to satisfy this requirement, so we should see if we can assign another job opening with a lower minimum skill requirement to the same worker, and so on. Using two pointers (one for workers and one for senior job openings), we can iterate over both arrays in a worst case time of $O(N + Q)$. Similarly, we can iterate over the sorted lists $W$ and $E$ to try and assign entry-level job openings to workers who have not been assigned a senior job opening yet. If a worker does not meet the maximum skill level limit for a job opening, the following workers with a higher skill level will also not be able to meet the same requirement, so we iterate over the remaining entry-level job openings to try and find an opening with a higher maximum skill level limit which can be satisfied by the worker. This can be computed in $O(N + P)$ time.

Now that the assignment process has been complete, we can iterate over the workers in $O(N)$ time to count how many workers have been assigned a job, providing the solution to the problem in $O(N \log N + P \log P + Q \log Q + 3N + P + Q) = O(N \log N + P \log P + Q \log Q)$ time. 

<u>Pseudocode:</u>

```pseudocode
W <- workers sorted by increasing skill level;
E <- entry-level job openings sorted by increasing maximum skill level limit;
S <- senior job openings sorted by decreasing minimum skill level requirement;

// assign senior job openings to workers first
FOR worker IN W, traversed in reverse order:
	WHILE job openings from S are still available:
		s_i <- next available job opening from S;
    IF worker.skill_level >= s_i.minimum_skill_level_requirement THEN
      assign s_i to worker;
      break;

// assign entry-level job openings to unassigned workers
FOR worker IN W:
	IF worker has already been assigned a senior job opening THEN continue;
	while job openings from E are still available:	
    e_i <- next available job opening from E;
    IF worker.skill_level <= e_i.maximum_skill_level_limit THEN
      assign e_i to worker;
      break;

return number of assigned workers in W;
```

