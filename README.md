# Multi-Armed-Bandits

The multi-armed bandit problem is a fundamental reinforcement learning setting that highlights the
exploration-exploitation tradeoff. An agent is faced with a set of arms, each with an unknown
reward distribution. The agent’s goal is to maximize its total reward over a horizon of trials by
strategically choosing which arms to pull. This requires balancing the exploitation of known high-
value arms with the exploration of uncertain arms. This report presents the implementation and
evaluation of two widely used bandit algorithms: Epsilon-Greedy and Upper Confidence Bound
(UCB). The experiments were conducted in a simulated 10-armed Bernoulli bandit environment.
The performance of these algorithms is compared based on mean reward, percentage of optimal
actions, and cumulative regret.
