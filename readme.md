# Maze Solver via Markov Decision Processes  
**ECE 440 – Reinforcement Learning Project 1**  
**Author:** Yankai Zhao, Lehigh University  

---

## Overview  
This project implements a deterministic **Markov Decision Process (MDP)** and solves it using the **Value Iteration algorithm** to compute an optimal navigation policy in a 2D maze environment.  
Each grid cell represents a state, and actions correspond to four directional movements.  
The implementation demonstrates Bellman optimality, convergence properties, and computational scaling of dynamic programming in reinforcement learning.

---

## Mathematical Formulation  

An MDP is defined as:  

\[
\mathcal{M} = \langle S, A, P, R, \gamma \rangle
\]

where  
- \(S\): Set of valid grid states  
- \(A = \{\text{up}, \text{down}, \text{left}, \text{right}\}\): Action space  
- \(P(s'|s,a)\): Deterministic transition model  
- \(R(s,a,s')\): Reward function  
- \(\gamma \in (0,1)\): Discount factor controlling future rewards  

The optimal value function satisfies the **Bellman Optimality Equation**:  

\[
V^*(s) = \max_a [R(s,a) + \gamma V^*(s')]
\]

---

## Algorithm  

**Value Iteration Update:**  

\[
V_{k+1}(s) = \max_a [R(s,a) + \gamma V_k(s')]
\]

**Convergence Criterion:**  

\[
|V_{k+1}(s) - V_k(s)| < \varepsilon
\]

**Optimal Policy Extraction:**  

\[
\pi^*(s) = \arg\max_a [R(s,a) + \gamma V^*(s')]
\]

**Computational Complexity:**  

\[
O(K|S||A|)
\]

where \(K\) is the number of iterations until convergence.

---

## Reward Function  

\[
R(s,a,s') =
\begin{cases}
+100, & s' = s_{\text{goal}}\\
-5, & s' = s \text{ (invalid move)}\\
-0.1, & \text{otherwise}
\end{cases}
\]

This structure rewards reaching the goal, penalizes collisions, and discourages oscillatory movements.

---

## Experimental Results  

| Maze Size | Iterations to Converge | Path Length | Discount Factor (γ) |
|------------|-----------------------|--------------|----------------------|
| 10×10 | 538 | 471 | 0.995 |
| 20×20 | 1834 | 775 | 0.995 |

As maze size increases, the number of states \( |S| \propto N^2 \), leading to quadratic growth in computational cost.  
Despite this, Value Iteration remains numerically stable and yields globally optimal trajectories.

---

## Implementation Structure  

| Component | Description |
|------------|-------------|
| **MazeMDP** | Defines environment states, actions, transitions, and rewards. |
| **Value Iteration** | Executes Bellman updates until convergence. |
| **Policy Extraction** | Derives the optimal action for each state. |
| **Visualization** | Generates static and animated trajectories. |

---

## Visualization Example  

- **Left:** Original maze (walls = black, paths = white)  
- **Right:** Solved maze (optimal path = red, start = green, goal = blue)  

