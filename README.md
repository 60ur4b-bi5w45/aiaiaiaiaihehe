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

# Travelling Problem with A* Heuristic Search

**Question:**  
Solve the following travelling problem using any heuristic search technique. Mark the steps to the solution.  
**Start:** `A`  
**Destination:** `E`  
*(Solution must be both cost- and time-effective.)*

```
       (6)        (1)        (3)
   A ——————— B ——————— D ——————— F
    \         |  \         |      /
   (7)\     (2)|   \  (8)  |(7) / (5)
        \      |      \    |    /
           C ———————— E
                (7)
```

Edges (with costs in parentheses):
- **A–B:** 6  **A–C:** 7  **B–C:** 2  
- **B–D:** 1  **C–D:** 8  
- **C–E:** 7  **D–E:** 7  
- **D–F:** 3  **E–F:** 5  

---

# Answer

## 1. Heuristic Choice

We choose an **admissible** & **consistent** heuristic  
$$
h(n) = \min\{\text{single‐edge cost from }n\text{ to }E\}.
$$

| Node | Edges from $n$ to $E$             | $h(n)$ |
|:----:|:----------------------------------|:------:|
| E    | —                                 | 0      |
| C    | C–E = 7                           | 7      |
| D    | D–E = 7                           | 7      |
| F    | F–E = 5                           | 5      |
| B    | B–D–E = 1+7 = 8                   | 8      |
| A    | min(A–C–E = 7+7, A–B–D–E = 6+1+7) | 14     |

This $h(n)$ never overestimates the true cost and satisfies $h(n)\le c(n,n')+h(n')$.

---

## 2. A* Search Trace

We maintain a **frontier** (min‐heap) ordered by  
$$
f(n)=g(n)+h(n),
$$  
where $g(n)$ is the cost from `A` to $n$.

| Step | Frontier (node: $g,h,f$)         | Action                                 |
|:----:|:---------------------------------|:---------------------------------------|
| 0    | { A: (0,14,$14$) }               | start                                  |
| 1    | { B: (6,8,$14$),  C: (7,7,$14$) } | expand A → generate B, C               |
| 2    | { C: (7,7,$14$),  B: (6,8,$14$) } | tie‐break on lower $h$ → expand **C**  |
|      | { B: (6,8,$14$),  D: (15,7,$22$),  E: (14,0,$14$) } | C → generate D, E |
| 3    | { E: (14,0,$14$),  B: (6,8,$14$),  D: (15,7,$22$) } | **E** has lowest $f$ → goal reached     |

- **Nodes expanded:** `A`, `C` (only 2 expansions)  
- **Goal found** when `E` is popped with $f(E)=14$.

---

## 3. Solution Path & Costs

```
A → C → E
```

- **Total cost:**  
  $g(E) = g(C) + \text{cost}(C,E) = 7 + 7 = \mathbf{14}$  
- **Cost‐optimal:** Yes (no cheaper path exists)  
- **Time‐efficient:** Yes (only 2 node expansions)  
```

