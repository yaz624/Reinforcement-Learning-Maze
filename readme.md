Maze Solver via Markov Decision Processes
Overview

This project implements a deterministic Markov Decision Process (MDP) and solves it using the Value Iteration algorithm to obtain an optimal navigation policy for 2D mazes.
Each maze cell is treated as a state, and actions correspond to four directional movements.
The implementation demonstrates the convergence of the Bellman optimality updates and the scalability of dynamic programming in reinforcement learning.

Formulation

An MDP is defined as:

𝑀
=
⟨
𝑆
,
𝐴
,
𝑃
,
𝑅
,
𝛾
⟩
M=⟨S,A,P,R,γ⟩

where

𝑆
S: set of valid grid states

𝐴
=
{
up
,
down
,
left
,
right
}
A={up,down,left,right}: action space

𝑃
(
𝑠
′
∣
𝑠
,
𝑎
)
P(s
′
∣s,a): deterministic transition model

𝑅
(
𝑠
,
𝑎
,
𝑠
′
)
R(s,a,s
′
): reward function

𝛾
∈
(
0
,
1
)
γ∈(0,1): discount factor

The optimal value function satisfies the Bellman equation:

𝑉
∗
(
𝑠
)
=
max
⁡
𝑎
[
𝑅
(
𝑠
,
𝑎
)
+
𝛾
𝑉
∗
(
𝑠
′
)
]
V
∗
(s)=
a
max
	​

[R(s,a)+γV
∗
(s
′
)]
Algorithm

Value Iteration Update:

𝑉
𝑘
+
1
(
𝑠
)
=
max
⁡
𝑎
[
𝑅
(
𝑠
,
𝑎
)
+
𝛾
𝑉
𝑘
(
𝑠
′
)
]
V
k+1
	​

(s)=
a
max
	​

[R(s,a)+γV
k
	​

(s
′
)]

Convergence Criterion:

∣
𝑉
𝑘
+
1
(
𝑠
)
−
𝑉
𝑘
(
𝑠
)
∣
<
𝜀
∣V
k+1
	​

(s)−V
k
	​

(s)∣<ε

Optimal Policy Extraction:

𝜋
∗
(
𝑠
)
=
arg
⁡
max
⁡
𝑎
[
𝑅
(
𝑠
,
𝑎
)
+
𝛾
𝑉
∗
(
𝑠
′
)
]
π
∗
(s)=arg
a
max
	​

[R(s,a)+γV
∗
(s
′
)]

Computational Complexity:

𝑂
(
𝐾
∣
𝑆
∣
∣
𝐴
∣
)
O(K∣S∣∣A∣)

where 
𝐾
K is the number of iterations until convergence.

Reward Function
𝑅
(
𝑠
,
𝑎
,
𝑠
′
)
=
{
+
100
,
	
𝑠
′
=
𝑠
goal


−
5
,
	
𝑠
′
=
𝑠
 (invalid move)


−
0.1
,
	
otherwise
R(s,a,s
′
)=
⎩
⎨
⎧
	​

+100,
−5,
−0.1,
	​

s
′
=s
goal
	​

s
′
=s (invalid move)
otherwise
	​


This design rewards reaching the goal, penalizes collisions, and discourages idle or oscillatory movement.

Experimental Results
Maze Size	Iterations to Converge	Path Length	Discount Factor (
𝛾
γ)
10×10	538	471	0.995
20×20	1834	775	0.995

The number of states grows quadratically with maze size (
∣
𝑆
∣
∝
𝑁
2
∣S∣∝N
2
), leading to proportional increases in computational cost.
Value Iteration remains numerically stable and produces globally consistent trajectories even in larger environments.

Implementation Structure
Component	Description
MazeMDP	Environment definition (state validity, transitions, reward)
Value Iteration	Iterative Bellman updates and convergence detection
Policy Extraction	Derivation of optimal state–action mapping
Visualization	Static and animated rendering of the optimal trajectory
Visualization Example

Left: Original maze (walls = black, paths = white)

Right: Solved maze (optimal path = red, start = green, goal = blue)

maze1.png           # 10×10 maze input
maze1-solved.png    # 10×10 solution
maze.png            # 20×20 maze input
maze-solved.png     # 20×20 solution

How to Run
Dependencies
pip install numpy matplotlib opencv-python pillow

Execute

Run the notebook in Jupyter or VSCode:

jupyter notebook project1.ipynb


The output includes:

Value function convergence logs

Path length and iteration metrics

Visualized optimal solution (solvedmaze.png)
