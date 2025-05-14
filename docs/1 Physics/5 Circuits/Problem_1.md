#  Circuits — Problem 1  
#  Equivalent Resistance Using Graph Theory

## 📘 Motivation

Calculating the **equivalent resistance** of a circuit is essential in understanding current flow, power distribution, and network behavior. For simple circuits, we can use well-known rules:

- Series: $R_{\text{eq}} = R_1 + R_2 + \dots + R_n$
- Parallel: $\displaystyle \frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n}$

However, as circuits grow complex, identifying these combinations becomes harder.

###  Graph Theory Approach

- Treat each **node** (junction) as a **vertex**
- Treat each **resistor** as an **edge** with a weight equal to its resistance
- Use **graph simplification algorithms** to reduce the graph

This approach allows automatic, programmable simplification of circuits, even with **nested** and **cyclical** resistor networks.

---

##  Mathematical Basis

Given a graph $G = (V, E)$:
- $V$ is the set of nodes
- $E$ is the set of edges, each with a weight $R_i$ (resistance)

We compute **equivalent resistance** between two nodes $a$ and $b$ using **Y-Δ transforms**, **series/parallel reduction**, or **Kirchhoff's laws** formulated in matrix form.

We model the circuit as a **weighted undirected graph** and systematically reduce it using basic rules:

### 🔧 Series Rule
If two resistors $R_1$ and $R_2$ connect in series:

$$
R_{\text{eq}} = R_1 + R_2
$$

### 🔌 Parallel Rule
If they connect in parallel:

$$
\frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2}
\Rightarrow
R_{\text{eq}} = \left( \frac{1}{R_1} + \frac{1}{R_2} \right)^{-1}
$$

---

##  Full Python Implementation (Graph Reduction)

We will build a Python implementation that:

- Represents circuits as graphs
- Identifies series and parallel nodes
- Simplifies the graph until one equivalent resistance remains

```python
import networkx as nx

def combine_parallel(resistors):
    inv_sum = sum(1 / r for r in resistors)
    return 1 / inv_sum if inv_sum else float('inf')

def combine_series(resistors):
    return sum(resistors)

def simplify_graph(G, source, target):
    changed = True
    while changed:
        changed = False
        # Series simplification
        for node in list(G.nodes()):
            if node in (source, target):
                continue
            neighbors = list(G.neighbors(node))
            if len(neighbors) == 2:
                u, v = neighbors
                if G.number_of_edges(node, u) == 1 and G.number_of_edges(node, v) == 1:
                    r1 = G.edges[node, u]['resistance']
                    r2 = G.edges[node, v]['resistance']
                    G.remove_node(node)
                    G.add_edge(u, v, resistance=r1 + r2)
                    changed = True
                    break
        # Parallel simplification
        for u, v in list(G.edges()):
            all_edges = list(G.get_edge_data(u, v).values())
            if len(all_edges) > 1:
                resistances = [edata['resistance'] for edata in all_edges]
                eq_res = combine_parallel(resistances)
                G.remove_edges_from([(u, v)] * len(all_edges))
                G.add_edge(u, v, resistance=eq_res)
                changed = True
                break
    return G.edges[source, target]['resistance']
