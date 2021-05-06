# Q Learning

- Q Learning Formula (converges to)
  - $Q(s,a) = r(s,a) + \gamma* V^*(s')$
- Q Learning Algorithm
  - $Q(s,a) = r(s,a) + \gamma * \max_{a'} Q(s', a')$
  - $s', a'$ is after
  - Necessary to force exploration through probabilistic choice of actions in order to ensure convergence to the true Q values

