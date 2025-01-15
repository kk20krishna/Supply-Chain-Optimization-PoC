# Intelligent-Sourcing
# Supply Chain Optimization - PoC
# Problem Statement

A company has multiple factories, multiple warehouses and stores located across different regions. The goal is to determine the optimal distribution plan to minimize the total transportation cost while meeting the demand of each store and respecting the production of each factory.

| Feature | Description |
|---|---|
| **Company Name** |  *Test Company* |
| **Number of Factories** | 2 |
| **Factory Names** | Factory#1, Factory#2 |
| **Number of Warehouses** | 4 |
| **Warehouse Names** | Palakkad, Bengaluru, Chennai, Hyderabad |
| **Number of Stores** | 5 |
| **Store Names** | Store#1, Store#2, Store#3, Store#4, Store#5 |


# Approach

We will use Linear Programming to model and solve this optimization problem. This involves defining decision variables, formulating an objective function, and specifying constraints. The PuLP library in Python will be used to implement and solve the model.

## Cost Function

The objective function is to minimize the total transportation cost. This is calculated as the sum of the products of the quantity transported on each route and the corresponding transportation cost.

**Mathematically:**

Minimize:

$ Sum(vars[f][w] * costs[f][w] for (f, w) in Routes) + Sum(vars[w][s] * costs[w][s] for (w, s) in Routes) $


where:
-   `vars[f][w]` represents the quantity transported from factory `f` to warehouse `w`.
-   `costs[f][w]` represents the cost of transporting one unit from factory `f` to warehouse `w`.
-   `vars[w][s]` represents the quantity transported from warehouse `w` to store `s`.
-   `costs[w][s]` represents the cost of transporting one unit from warehouse `w` to store `s`.
-   `Routes` represents all possible transportation routes.

## Constraints

The optimization problem is subject to the following constraints:

1.  **Supply Constraint:** The total quantity shipped from each factory cannot exceed its production capacity.
2.  **Routing Conttraint:** The total quantity shipped from each warehouse should be equalt to the supply it received from all the factories.
3.  **Demand Constraint:** The total quantity received by each store must meet its demand.
4.  **Non-negativity Constraint:** The quantity transported on each route must be non-negative.

**Mathematically:**

1.  Supply Constraint: `lpSum([vars[w][s] for s in Stores]) <= supply[w]` for each warehouse `w`
2.  Demand Constraint: `lpSum([vars[w][s] for s in Warehouses]) == demand[s]` for each store `s`
3.  Non-negativity Constraint: `vars[w][s] >= 0` for all routes `(w, s)`

# Final Outcomes

The optimization model provides the following outputs:

1.  **Optimal Distribution Plan:** The quantity of goods to be transported from each factory to each warehouse to each store.
2.  **Minimum Transportation Cost:** The total cost associated with the optimal distribution plan.

**Analyzing Results:**
- Review the `Detailed Distribution Report` to observe the specific quantities shipped on each route.
- Examine the `Total Cost of Transportation` to assess the efficiency of the optimized plan.

By implementing this approach, the company can effectively manage its distribution network, minimize transportation costs, and ensure that customer demand is satisfied.
