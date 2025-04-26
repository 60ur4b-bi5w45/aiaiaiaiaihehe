# aiaiaiaiaihehe

Here’s a worked‐out solution to all five questions:

---

### Q1: How do local search algorithms operate? (2 marks)

Local search methods maintain **a single current state** and repeatedly move to a “neighbor” state in its vicinity, guided by an **evaluation** (or objective) function rather than by building a full search tree.  At each step they:

1. **Generate** one or more successors of the current state (its “neighbors”).  
2. **Evaluate** each neighbor, using a heuristic or objective function.  
3. **Move** to the best neighbor (or sometimes a random neighbor, to escape plateaus/local maxima).  

Examples include **hill‐climbing**, **simulated annealing**, **genetic algorithms**, and **local beam search**.  

---

### Q2: The Vacuum-World as a Standardized Problem (4 marks)

A “standardized” (or **formal**) problem specification in AI consists of:

1. **State space**  
2. **Initial state**  
3. **Actions (successor function)**  
4. **Goal test**  
5. **Path-cost function**

For the simple two-cell vacuum world:

1. **State**  – A triple ⟨Loc, StatusA, StatusB⟩ where  
   - Loc ∈ {A,B} is the agent’s current location.  
   - StatusX ∈ {Clean, Dirty} is the cleanliness of cell X.  
2. **Initial state**  – e.g. ⟨A, Dirty, Dirty⟩ (agent in A, both dirty).  
3. **Actions**  –  
   - **Suck**: if current cell is Dirty, it becomes Clean.  
   - **Left** / **Right**: move between A and B.  
4. **Transition model**  – specifies the result of each action (e.g. sucking in a clean cell leaves it clean, moving flips Loc).  
5. **Goal test**  – both cells are clean: StatusA = Clean ∧ StatusB = Clean.  
6. **Path-cost**  – typically one unit per action (minimize total actions).  

---

### Q3: When do we call an optimization problem “hill-climbing” vs. “gradient descent”? (3 marks)

- **Hill-climbing** is the discrete/local version: you have a finite (or combinatorial) set of states and a **score** f(s) to **maximize**. You move to neighbor states with higher f(s), stopping at a local maximum.  
- **Gradient descent** applies when the domain is **continuous** and f(x) is **differentiable**. One iteratively updates  
\[
x_{t+1} = x_t - \eta\,\nabla f(x_t)
\]  
to **minimize** f(x) (or uses +η∇f for maximization).  

In short:  
- **Discrete, score‐based →** hill-climbing  
- **Continuous, differentiable →** gradient‐descent  

---

### Q4: Explain any two real-world problems (choose two; 3 marks × 2 = 6 marks)

#### (i) The 8-Puzzle  
- **State**: a 3×3 grid with eight numbered tiles and one blank.  
- **Initial/Goal**: two different arrangements of the tiles.  
- **Actions**: slide a tile adjacent to the blank into the blank spot.  
- **Successors**: up to 4 moves from each state.  
- **Goal test**: tiles are in the target order.  
- **Heuristics**: e.g. Manhattan distance or number of misplaced tiles.  
- **Search methods**: A*, IDA*, etc.

#### (ii) Route-Finding Problem  
- **State**: current location (node) in a graph of cities/roads.  
- **Initial**: starting city.  
- **Goal test**: destination city.  
- **Actions**: traverse any outgoing road (edge) to a neighboring city.  
- **Path-cost**: sum of road lengths (or travel times).  
- **Heuristics**: straight‐line (“as‐the‐crow‐flies”) distance for A* search.

*(Other choices:)*  
- **Touring problems (TSP)** – find the shortest cyclic tour through all cities (NP‐hard).  
- **VLSI layout** – assign circuit modules to chip locations to minimize total wire length, subject to no‐overlap constraints.

---

### Q5: CSP and Sudoku as a CSP (1 + 4 marks)

**Constraint‐Satisfaction Problem (CSP):**  
A CSP is defined by the triple \((\mathbf{X},\mathbf{D},\mathbf{C})\):  
- \(\mathbf{X}=\{X_1,\dots,X_n\}\) is a set of **variables**.  
- \(\mathbf{D}=\{D_1,\dots,D_n\}\) gives each \(X_i\) a **domain** \(D_i\) of possible values.  
- \(\mathbf{C}\) is a set of **constraints**, each involving some subset of the variables, specifying which combinations of values are allowed.

---

**Sudoku as a CSP:**  
- **Variables**  
  \[
    X_{i,j}\quad (1\le i,j\le9)
  \]  
  one variable for each cell in the 9×9 grid.  
- **Domains**  
  \[
    D_{i,j} = \{1,2,\dots,9\}
  \]  
  (or a singleton if the cell is pre-filled).  
- **Constraints**  
  1. **Row constraints**: for each row \(i\), all \(\{X_{i,1},…,X_{i,9}\}\) must be all‐different.  
  2. **Column constraints**: for each column \(j\), all \(\{X_{1,j},…,X_{9,j}\}\) must be all‐different.  
  3. **Block constraints**: for each 3×3 block (e.g. cells with \(i∈\{1,2,3\}, j∈\{1,2,3\}\)), the nine variables must be all‐different.  

Solving the Sudoku then reduces to assigning each \(X_{i,j}\) a value from 1–9 so that all constraints are satisfied.  

---

*That completes all parts of the test.*
