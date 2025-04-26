# Q1: How do local search algorithms operate? (2 marks)

Local search methods maintain **one current state** and repeatedly move to a “neighbor” state in its vicinity, guided by an **evaluation function** rather than by building a full search tree. At each step they:

1. **Generate** one or more successors (neighbors) of the current state.  
2. **Evaluate** each neighbor using a heuristic or objective function.  
3. **Move** to the best neighbor (or sometimes to a random neighbor, to escape plateaus or local maxima).

**Examples:** hill-climbing, simulated annealing, genetic algorithms, local beam search.

---

# Q2: The Vacuum-World as a Standardized Problem (4 marks)

A formal problem specification consists of:

1. **State space**  
2. **Initial state**  
3. **Actions (successor function)**  
4. **Goal test**  
5. **Path-cost function**

For the two-cell vacuum world:

1. **State**  
⟨Loc, StatusA, StatusB⟩

- `Loc ∈ {A, B}` is the agent’s position.  
- `StatusX ∈ {Clean, Dirty}` is the cleanliness of cell X.  

2. **Initial state**  
e.g. `⟨A, Dirty, Dirty⟩`.

3. **Actions**  
- `Suck`: if the current cell is Dirty, it becomes Clean.  
- `Left` / `Right`: move between A and B.

4. **Goal test**  
StatusA = Clean ∧ StatusB = Clean


5. **Path-cost**  
Typically 1 per action (minimize total actions).

---

# Q3: Hill-Climbing vs. Gradient Descent (3 marks)

- **Hill-climbing**  
- Discrete (combinatorial) state space.  
- Objective: **maximize** a score function $f(s)$.  
- Move to a neighboring state with higher $f(s)$ until a local maximum is reached.

- **Gradient descent**  
- Continuous, differentiable domain.  
- Objective: **minimize** a function $f(x)$.  
- Iterative update:  
 $$
   x_{t+1} = x_t - \eta \,\nabla f(x_t)
 $$  
- (For maximization, use $x_{t+1} = x_t + \eta \,\nabla f(x_t)$.)

---

# Q4: Explain Two Real-World Problems (3+3 marks)

Choose any two of the following:

## (i) 8-Puzzle  
- **State:** a 3×3 grid with tiles 1–8 and one blank.  
- **Initial/Goal:** two different tile arrangements.  
- **Actions:** slide a tile adjacent to the blank into the blank spot.  
- **Successors:** up to 4 moves per state.  
- **Goal test:** tiles match the target configuration.  
- **Heuristics:** Manhattan distance, number of misplaced tiles.  
- **Search methods:** A\*, IDA\*, etc.

## (ii) Route-Finding Problem  
- **State:** current node in a graph of cities/roads.  
- **Initial:** start city.  
- **Goal test:** destination city.  
- **Actions:** traverse an edge (road) to a neighboring city.  
- **Path-cost:** sum of road lengths or travel times.  
- **Heuristics:** straight-line distance for A\*.

---

# Q5: CSP and Sudoku as a CSP (1+4 marks)

## What is a CSP?  
A **Constraint-Satisfaction Problem** is defined by a triple $(X, D, C)$:

- $X = \{X_1, \dots, X_n\}$: **variables**.  
- $D = \{D_1, \dots, D_n\}$: each $D_i$ is the **domain** of $X_i$.  
- $C$: a set of **constraints** specifying allowed combinations of values for subsets of $X$.

## Sudoku as a CSP  
- **Variables:**  
$X_{i,j}$ for each cell, $1 \le i,j \le 9$.  

- **Domains:**  
$D_{i,j} = \{1,2,\dots,9\}$ (or a singleton if pre-filled).

- **Constraints:**  
1. **Row:** All $X_{i,1},\dots,X_{i,9}$ in row $i$ must be all-different.  
2. **Column:** All $X_{1,j},\dots,X_{9,j}$ in column $j$ must be all-different.  
3. **Block:** Each 3×3 block (e.g.\ $i\in\{1,2,3\}, j\in\{1,2,3\}$) must be all-different.

Solving is assigning each $X_{i,j}\in D_{i,j}$ so all constraints hold.


