# Multiple 1-0 knapsack problem

**Please note that the .ipynb file is valid and will open correctly once downloaded. Thank you for understanding!**

The core idea and design of the solution were developed by author. AI tools were used to assit with the code optimization, refactoring and improving readability, but all conceptual ideas and problem-solving approches, including many experiments, are original.

## Algorithm Overview

### 0. Initialize the first solution
Filling knapsacks with the most valuable items without exceeding weight limits

- Initialize empty knapsacks and a set of used items.
- For each knapsack:
  - Track remaining capacity.
  - Place items in descending order of value if they fit and haven't been used.
- Return the filled knapsack solution matrix.

### 1. Generate a neighbor solution
A neighbor solution is generated using one of the following tweaks:

1. **Invert an item** – change the presence of one item in a knapsack (0 → 1 or 1 → 0).  
2. **Move an item** – move an item from one knapsack to another.  
3. **Swap items** – exchange two items between different knapsacks.  

### 2. Evaluate the New Solution
- Compute `new_cost` (total value of items in the solution).  
- Compare `new_cost` with `current_cost`.
- Accept new solution if  `new_cost` >= `current_cost`

### 3. Simulated Annealing Decision
- Compute the difference:  
$$
\Delta = \text{new_cost} - \text{current_cost}
$$

- Compute temperature:
$$
T = \max(0.1, T_0 - \text{cooling_rate} \times \text{step})
$$

- Draw a random number `r` from `[0, 1]`.  
- **Accept new solution** if:
$$
r < P
$$


This allows accepting worse solutions to escape local optima.

### 4. Fallback Heuristic
With probability
$$
random(0, 1) < 0.5
$$
Check, if the new solution is rejected **and** no remaining items can be added to any knapsack:
- Remove the **least valuable item** from the current solution to free space.  
- Continue the algorithm with the updated solution.
