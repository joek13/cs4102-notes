## Algorithms studied this unit
...and whether/how they satisfy optimal substructure and greedy choice property
- Knapsack problem (continuous and 0/1 variety)
    - Fractional/continuous satisfies greedy choice property: at every step, take as much as you can of the item with the highest $val / weight$ ratio.
    - 0/1 knapsack doesn't satisfy greedy choice, but it does satisfy optimal substructure: if $S_{n-1}$ is suboptimal, then $S_n$ cannot be optimal because we could construct a $S_n^*$ using the optimal $S_{n-1}^*$.
        - Time complexity $\Theta(n \times c)$ - *pseudopolynomial*
- Activity scheduling
    - Satisfies greedy choice: at every step, select the earliest-ending activity that doesn't conflict
- Weighted activity scheduling
    - Optimal substructure: argument same as knapsack—if a better selection exists for $n-1$ elements, we can extend it to be optimal for $n$ elements.
- Log cutting
    - Optimal substructure: similar argument as before
    - Runtime: $\Theta(n^2)$
- Making change (greedy variety, caveats)
    - While amount outstanding is greater than zero, take one more of the greatest denomination that is less than the amount outstanding
        - Greedy choice: takes the GREATEST locally feasible denomination every time
    - Only works because American coin denominations form a *matroid*
- Levenshtein edit distance
    - Optimal substructure: if the alignment of strings $X_n$ and $Y_n$ is optimal, then necessarily $X_{n-1}$ and $Y_{n-1}$ are optimal.
- Longest common substring

## Greedy algorithms
### Terminology
- **Optimization problem:** finding the best solution among many feasible solutions
- **Feasible solution:** solution that satisfies constraints, may/may not be best
- **Objective function:** "scoring" function for a feasible solution that we want to maximize or minimize
- **Optimal solution:** a (not necessarily unique) solution that minimizes/maximizes your objective function

### Greedy choice property
- Property of a problem where making the locally optimal choice always results in a globally optimal solution
- All greedy choice problems satisfy optimal substructure, but not all optimal substructure problems satisfy greedy choice

### Dijkstra's and Prim's as greedy algorithms
- Dijkstra's: always pursues shortest-dist unknown vertex
- Prim's: always includes lowest-weight edge that joins a vertex to a non-tree vertex

### Proving greedy algorithm correctness
...using an exchange argument

E.g., proving the unweighted interval selection algorithm correct.

Suppose we have $G = \{ g_1, \dots, \g_n \}$, solution picked by our greedy algorithm. And $O = \{ o_1, \dots, o_n \}$ is the hypothetical optimal solution.

Lemma: $\forall i, g_i.f \le o_i.f$—the greedy algorithm "stays ahead" of the optimal solution.

(Why? Suppose in an inductive proof $g_k.f > o_k.f$. Then there must exist some $o_{k-1}$ that satisfies $g_{k-1}.f \le o_{k-1}.f$. We know $o_{k-1}.f \le o_k.s$, so therefore $g_{k-1}.f \le o_k.s$. So $o_k$ is compatible with our schedule. But the algorithm would have then picked it! But it didn't! Contradiction!)

From the lemma, we can prove that the greedy algorithm will always include an interval from the optimal solution when possible. Therefore it always finds an optimal solution.


## Dynamic programming
Works when we can identify some "recursive structure" to our problem: a solution is made up of several subproblem solutions, which may themselves be made up of several subproblem solutions, etc...

- Finds solutions to smallest subproblems, then builds up
