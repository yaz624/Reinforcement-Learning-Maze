# $\text{Maze Solver via Markov Decision Processes}$
**$\text{ECE 440 – Reinforcement Learning Project 1}$**
**$\text{Author}: \text{Yankai Zhao}, \text{Lehigh University}$**

---

## $\text{Overview}$
This project implements a deterministic Markov Decision Process (MDP) and solves it using the Value Iteration algorithm to compute an optimal navigation policy in a 2D maze environment.
There are several free resources available to generate mazes in order to test your algorithms. For instance, this free
generator https://keesiemeijer.github.io/maze-generator generates a PNG image for mazes of any custom
size, rows and columns.
Each grid cell represents a state, and actions correspond to four directional movements.
The implementation demonstrates Bellman optimality, convergence properties, and computational scaling of dynamic programming in reinforcement learning.

---

## $\text{Mathematical Formulation}$

$\text{An MDP is defined as:}$

$$
\mathcal{M} = \langle S, A, P, R, \gamma \rangle
$$

$\text{where}$
- $\mathbf{S}$: $\text{Set of valid grid states}$
- $\mathbf{A} = \{\text{up}, \text{down}, \text{left}, \text{right}\}$: $\text{Action space}$
- $\mathbf{P(s'|s,a)}$: $\text{Deterministic transition model}$
- $\mathbf{R(s,a,s')}$: $\text{Reward function}$
- $\mathbf{\gamma \in (0,1)}$: $\text{Discount factor controlling future rewards}$

$\text{The optimal value function satisfies the } \mathbf{Bellman \text{ Optimality Equation}} \text{:}$

$$
\mathcal{V}^{\ast}(s) = \max_a [R(s,a) + \gamma V^{\ast}(s')]
$$

---

## $\text{Algorithm}$

**$\text{Value Iteration Update}$**:

$$
V_{k+1}(s) = \max_a [R(s,a) + \gamma V_k(s')]
$$

**$\text{Convergence Criterion}$**:

$$
|V_{k+1}(s) - V_k(s)| < \varepsilon
$$

**$\text{Optimal Policy Extraction}$**:

$$
\pi^{\ast}(s) = \arg\max_a [R(s,a) + \gamma V^{\ast}(s')]
$$


## $\text{Reward Function}$

$$
R(s,a,s') =
\begin{cases}
+100, & s' = s_{\text{goal}}\\
-5, & s' = s \text{ (invalid move)}\\
-0.1, & \text{otherwise}
\end{cases}
$$

$\text{This structure rewards reaching the goal, penalizes collisions, and discourages oscillatory movements.}$

---

## $\text{Experimental Results}$

| $\text{Maze Size}$ | $\text{Iterations to Converge}$ | $\text{Path Length}$ | $\text{Discount Factor } (\gamma)$ |
|:-------------------|:-------------------------------|:---------------------|:-----------------------------------|
| $10\times 10$ | $538$ | $471$ | $0.995$ |
| $20\times 20$ | $1834$ | $775$ | $0.995$ |

$\text{As maze size increases, the number of states } |S| \propto N^2 \text{, leading to quadratic growth in computational cost.}$
$\text{Despite this, Value Iteration remains numerically stable and yields globally optimal trajectories.}$

---

## $\text{Implementation Structure}$

| $\text{Component}$ | $\text{Description}$ |
|:-------------------|:---------------------|
| $\mathbf{MazeMDP}$ | $\text{Defines environment states, actions, transitions, and rewards.}$ |
| $\mathbf{Value \text{ Iteration}}$ | $\text{Executes Bellman updates until convergence.}$ |
| $\mathbf{Policy \text{ Extraction}}$ | $\text{Derives the optimal action for each state.}$ |
| $\mathbf{Visualization}$ | $\text{Generates static and animated trajectories.}$ |

---

## $\text{Visualization Example}$

- $\mathbf{\text{Left}}$: $\text{Original maze (walls } = \text{ black, paths } = \text{ white)}$
- $\mathbf{\text{Right}}$: $\text{Solved maze (optimal path } = \text{ red, start } = \text{ green, goal } = \text{ blue)}$


$\text{Example output visualization}$:

$\text{}$

---
Example output visualization:

<img width="410" height="410" alt="maze-solved" src="https://github.com/user-attachments/assets/628ecbf4-8842-4070-98d4-0d6e6d204d14" />




---

## Usage  

### 1. Dependencies  
```bash
pip install numpy matplotlib opencv-python pillow
```
### 2. Run

Open the notebook in Jupyter or VSCode:
```python
jupyter notebook project1.ipynb
```

### 3. Replace Input

To test custom mazes, replace maze.png with a binary maze image (black–white).
The agent will automatically detect start/end points and output solvedmaze.png.

