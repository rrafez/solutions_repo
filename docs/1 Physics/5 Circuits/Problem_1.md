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