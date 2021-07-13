# COMP3121 Assignment 2 Question 3

Andrew Xie, z5317337

**A city is attacked by $N$ monsters and is defended by a single hero with initial strength of $S$ units. To kill a monster $i$ the hero must dissipate $a_i$ units of strength; if monster $i$ is killed successfully the hero gains $g_i$ units of strength. Thus, if the hero had strength $c \geq a_i$ before tackling monster $i$ he can kill the monster and he will end up with $c - a_i + g_i$ units of strength. Note that for some monsters $i$ you might have $g_i \geq a_i$ but for some other $j$ you might have $a_j \gt g_j$. You are given $S$ and for each $i$ you are given $a_i$ and $g_i$. Design an algorithm which determines in which order the hero can fight the monsters if he is to kill them all (if there is such an ordering). In case there is no such ordering the algorithm should output "no such ordering". Assume all values are positive integers.**

To try and ensure the hero kills all of the monsters, a greedy approach can be used to order the monsters to be fought such that the hero's strength is maximised for each stage. As such, even if tackling a monster results in a net loss of strength ($a_j \gt g_j$), we want there to hopefully be enough strength gained from the previous stages so that $c \geq a_j$ and the hero is able to kill monster $j$ as well as any subsequent monsters using this strategy. To do this, we can sort the order of monsters to be fought by decreasing net strength gain if a fight were to occur, given by the difference $g_i - a_i$. However, simply sorting by this value does not account for the cases where there is not enough strength to start a battle in the first place. To account for this, we can take the ratio of this net strength gain relative to the dissipated strength $a_i$. Thus, sorting monsters by the value $\frac{g_i - a_i}{a_i}$ from highest to lowest will provide the strongest order of monster battles for the hero, which can be done in $O(N \log N)$ time using merge sort. Now we need to iterate over each of the $N$ monsters in $O(N)$ time to ensure that $c \nless a_j$ at any point in the sorted list, otherwise no such ordering of monsters such that all monsters can be killed is possible. Such an algorithm will provide a solution to the problem in $O(N \log N)$.

<u>Pseudocode:</u>

```pseudocode
strength <- S;
Sort monsters by decreasing strength gain to dissipated strength ratio ((g_i - a_i) / a_i);
FOR monster IN monsters:
	IF strength < monster['a_i'] THEN return "no such ordering";
	ELSE strength <- strength - monster['a_i'] + monster['g_i'];
return sorted order of monsters;
```
