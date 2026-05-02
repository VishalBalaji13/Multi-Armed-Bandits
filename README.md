# Multi-Armed-Bandits

The multi-armed bandit problem is a fundamental reinforcement learning setting that highlights the exploration-exploitation tradeoff. An agent is faced with a set of arms, each with an unknown reward distribution. The agent's goal is to maximize its total reward over a horizon of trials by strategically choosing which arms to pull. This requires balancing the exploitation of known high-value arms with the exploration of uncertain arms. 

This repository presents the implementation and evaluation of widely used bandit algorithms, primarily focusing on Epsilon-Greedy, Upper Confidence Bound (UCB), and Thompson Sampling. The experiments were conducted in a simulated 10-armed Bernoulli bandit environment, comparing performance based on mean reward, percentage of optimal actions, and cumulative regret.

##  Algorithms Implemented

### 1. Epsilon-Greedy
A straightforward method for balancing exploration and exploitation. At each time step, with probability $\epsilon$, the agent selects an arm at random (exploration), and with probability $1-\epsilon$, it selects the arm with the highest estimated value (exploitation).
* **Pros:** Simple and efficient to implement.
* **Cons:** Blind exploration; it may over-explore in the long run.

### 2. Upper Confidence Bound (UCB)
Applies the principle of "optimism in the face of uncertainty." It selects the arm with the maximum value of $Q_t(a) + c \cdot \sqrt{\ln(t)/N_t(a)}$, where $Q_t(a)$ is the estimated reward, and $N_t(a)$ is the number of times the arm has been selected. The exploration bonus naturally decreases as more information is collected.
* **Pros:** More directed and calculated exploration than Epsilon-Greedy.
* **Cons:** Sensitive to the choice of the confidence parameter $c$.

### 3. Thompson Sampling
A Bayesian algorithm providing a probabilistic method for balancing exploration and exploitation. For Bernoulli bandits, it maintains a Beta distribution prior for each arm's reward probability. It samples from the posterior and updates $\alpha$ on a success (reward = 1) and $\beta$ on a failure (reward = 0).
* **Pros:** Highly effective, principled Bayesian approach that often outperforms other methods.
* **Cons:** More computationally intensive.

##  Experimental Setup

* **Environment:** 10-armed Bernoulli bandit.
* **Reward Distribution:** Each arm's reward probability was sampled from a Uniform(0,1) distribution.
* **Horizon:** $T = 1000$ steps.
* **Runs:** Results were averaged over 200 independent runs.
* **Non-Stationary Variant:** Explored environments where probabilities drift with a Gaussian random walk ($\sigma = 0.05$).

##  Results & Analysis

### Baseline Algorithm Comparison
| Algorithm | Final Mean Reward | Final % Optimal | Final Cumulative Regret |
| :--- | :--- | :--- | :--- |
| **Epsilon-Greedy** ($\epsilon=0.1$) | 0.82 | 75% | 95.4 |
| **UCB** ($c=1.0$) | 0.88 | 81% | 60.2 |

### Epsilon-Greedy Parameter Sweep
| Epsilon ($\epsilon$) | Final Mean Reward | Final % Optimal | Final Cumulative Regret |
| :--- | :--- | :--- | :--- |
| 0.0 | 0.675 | 16.0% | 260.47 |
| 0.01 | 0.870 | 56.5% | 128.52 |
| **0.05** | **0.885** | **82.5%** | **60.34** |
| 0.1 | 0.880 | 77.5% | 67.93 |
| 0.2 | 0.805 | 67.5% | 97.34 |

### UCB Parameter Sweep
| Confidence ($c$) | Final Mean Reward | Final % Optimal | Final Cumulative Regret |
| :--- | :--- | :--- | :--- |
| **0.5** | **0.910** | **83.0%** | **33.64** |
| 1.0 | 0.890 | 66.5% | 87.16 |
| 2.0 | 0.810 | 45.5% | 179.72 |

The results confirm that UCB generally outperforms Epsilon-Greedy in stationary environments due to its more structured, uncertainty-based exploration. While Epsilon-Greedy performs random exploration, UCB explores optimistically. In non-stationary settings, adaptation mechanisms (like constant step-size updates) become essential, as standard sample-average methods fail to track changing reward distributions effectively.
