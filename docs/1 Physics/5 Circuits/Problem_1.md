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

def combine_parallel(resistances):
    inv_sum = sum(1 / r for r in resistances if r > 0)
    return 1 / inv_sum if inv_sum else float('inf')

def combine_series(resistances):
    return sum(resistances)

def simplify_graph(G, source, target):
    G = G.copy()
    changed = True
    while changed:
        changed = False

        # Simplify series connections
        for node in list(G.nodes()):
            if node in (source, target):
                continue
            neighbors = list(G.neighbors(node))
            if len(neighbors) == 2:
                u, v = neighbors
                if G.has_edge(node, u) and G.has_edge(node, v):
                    r1 = G[node][u]['resistance']
                    r2 = G[node][v]['resistance']
                    G.remove_node(node)
                    if G.has_edge(u, v):
                        existing_r = G[u][v]['resistance']
                        G[u][v]['resistance'] = combine_parallel([existing_r, r1 + r2])
                    else:
                        G.add_edge(u, v, resistance=r1 + r2)
                    changed = True
                    break

        # Simplify parallel connections
        for u, v in list(G.edges()):
            if G.number_of_edges(u, v) > 1:
                resistances = [edata['resistance'] for key, edata in G[u][v].items()]
                eq_res = combine_parallel(resistances)
                G.remove_edges_from([(u, v)] * G.number_of_edges(u, v))
                G.add_edge(u, v, resistance=eq_res)
                changed = True
                break

    if G.has_edge(source, target):
        return G[source][target]['resistance']
    else:
        return float('inf')  # No path found
