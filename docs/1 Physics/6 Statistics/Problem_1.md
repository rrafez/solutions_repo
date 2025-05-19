#  Statistics — Problem 1  
# Central Limit Theorem Through Simulations

##  Motivation

The **Central Limit Theorem (CLT)** is one of the most important results in probability theory and statistics. It states:

> Given a sufficiently large sample size $n$, the sampling distribution of the sample mean $\bar{x}$ will tend to follow a **normal distribution**, regardless of the shape of the population distribution.

This is powerful because it allows us to make inferences about population means using normal probability methods — even when the population distribution is not normal.

In this notebook, we explore the CLT **empirically** by simulating data from different types of distributions and analyzing the distribution of sample means for varying sample sizes.

---

##  Mathematical Framework

### Central Limit Theorem Formal Statement

Let $X_1, X_2, \dots, X_n$ be a random sample of size $n$ drawn from any population with:

- Finite mean $\mu$
- Finite variance $\sigma^2$

Then, the distribution of the standardized sample mean:

$$
Z = \frac{\bar{X} - \mu}{\sigma / \sqrt{n}}
$$

approaches the standard normal distribution $N(0,1)$ as $n \to \infty$.

---

##  Simulation Plan

We will:

- Generate large populations from three different distributions:
  - **Uniform**
  - **Exponential**
  - **Binomial**
- Draw repeated samples of different sizes ($n = 5, 10, 30, 50$)
- Calculate the mean of each sample
- Plot the distribution of these sample means
- Observe how the distribution evolves as $n$ increases

---

```python
# 🔬 Central Limit Theorem Simulation with English Labels

import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set style and seed
sns.set(style="whitegrid")
np.random.seed(42)

# Generate population based on distribution type
def generate_population(dist_type, size=100000):
    if dist_type == "uniform":
        return np.random.uniform(0, 1, size)
    elif dist_type == "exponential":
        return np.random.exponential(scale=1.0, size=size)
    elif dist_type == "binomial":
        return np.random.binomial(n=10, p=0.5, size=size)
    else:
        raise ValueError("Unsupported distribution type")

# Compute sample means
def get_sample_means(population, sample_size, n_samples=1000):
    means = []
    for _ in range(n_samples):
        sample = np.random.choice(population, size=sample_size, replace=False)
        means.append(np.mean(sample))
    return means

# Plot histograms of sample means
def plot_sampling_distributions(population, dist_name, sample_sizes):
    fig, axes = plt.subplots(len(sample_sizes), 1, figsize=(8, 4 * len(sample_sizes)))
    fig.suptitle(f"{dist_name.title()} Distribution - Sample Mean Distributions", fontsize=16)

    for i, n in enumerate(sample_sizes):
        means = get_sample_means(population, sample_size=n)
        sns.histplot(means, kde=True, ax=axes[i], bins=30, color="skyblue")
        axes[i].set_title(f"Sample Size = {n}")
        axes[i].set_xlabel("Sample Mean")
        axes[i].set_ylabel("Frequency")

    plt.tight_layout(rect=[0, 0, 1, 0.95])
    plt.show()

# Run simulation
distributions = ['uniform', 'exponential', 'binomial']
sample_sizes = [5, 10, 30, 50]

for dist in distributions:
    population = generate_population(dist)
    plot_sampling_distributions(population, dist, sample_sizes)


