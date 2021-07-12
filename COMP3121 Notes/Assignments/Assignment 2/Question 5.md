# COMP3121 Assignment 2 Question 5

Andrew Xie, z5317337

**You are given $n$ jobs where each job takes one unit of time to finish. Job $i$ will provide a profit of $g_i$ dollars $(g_i \gt 0)$ if finished at or before time $t_i$, where $t_i$ is an arbitrary integer larger or equal to 1. Only one job can be done at any instant of time and jobs have to be done continuously from start to finish. (Note: if a job $i$ is not finished by $t_i$ then there is no benefit in scheduling it at all. All jobs can start as early as time 0). Give the most efficient algorithm you can to find a schedule that maximises the total profit.**

This question can be solved using a greedy strategy. Since all jobs take the same duration of one unit of time, total profit can be maximised by trying to schedule the jobs which would provide the highest profit of $g_i$ dollars if completed before $t_i$. To do this, we can place such jobs in the latest available time slot before $t_i$, since this leaves open more time slots to be filled earlier in the schedule. Firstly, sorting the jobs by their profit return $g_i$ from highest to lowest can be achieved in $O(n \log n)$ using merge sort. Iterating over each of the $n$ jobs sorted by decreasing profits, finding the first available time slot before $t_i$ can be completed in $O(\log \max\{t_i\})$ using a binary search over the increasing monotonic range of positive integer end times from 1 to $\max\{t_i\}$ (we can simply consider end times since start_time is just end_time - 1). Since all profits $g_i$ are non-negative, total profit would be maximised if we can schedule as many jobs as possible up to the latest end time of $\max \{t_i\}$. If the job was able to be scheduled in, remove its scheduled time slot from the remaining available time slots, and add $g_i$ to the total profit. Continue trying to schedule the remaining jobs until all jobs have been iterated over, or there are no remaining time slots available in the schedule. This algorithm has a worst case time complexity of $O(n (\log n + \log \max\{t_i\}))$. 

<u>Pseudocode:</u>

```pseudocode
total_profit <- 0;
unscheduled_end_times = list(1, 2, ..., max(t_i));
Sort jobs by decreasing profit g_i;
FOR job IN sorted_jobs:
	t_i <- deadline for completing job and receiving a profit;
	g_i <- profit for completing job before t_i;
	Binary search to find first available unscheduled_end_time before t_i;
	IF found THEN
		Remove unscheduled_end_time from unscheduled_end_times;
		total_profit <- total_profit + g_i;
return total_profit;
```

