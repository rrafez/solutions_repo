# Problem: Circular Wave Interference from Multiple Sources

## 🎯 Objective

To **simulate and visualize** the **interference pattern** produced by multiple point sources generating circular waves on a water surface. We'll mathematically model the superposition of these waves and analyze the resulting pattern using **formulas**, **Python simulation**, and **graphical plots**.

---

## 🌊 Physical Background

When multiple point sources emit circular waves in phase, the overlapping of these waves leads to **constructive** and **destructive** interference. The wave pattern on the water surface can be predicted by summing the displacements from each source using the **principle of superposition**.

Each point source at location $(x_i, y_i)$ produces a wave:

$$
\eta_i(x, y, t) = \frac{A}{\sqrt{r_i}} \cos(k r_i - \omega t + \phi)
$$

Where:
- $A$ is the amplitude of the wave
- $r_i = \sqrt{(x - x_i)^2 + (y - y_i)^2}$ is the distance to the observation point
- $k = \frac{2\pi}{\lambda}$ is the wavenumber
- $\omega = 2\pi f$ is the angular frequency
- $\phi$ is the initial phase (assumed to be zero unless otherwise specified)

The total wave at point $(x, y)$ and time $t$ is:

$$
\eta(x, y, t) = \sum_{i=1}^{N} \eta_i(x, y, t)
$$

---

## 🧠 Parameters and Setup

We consider:
- **$N = 6$ sources** arranged at the vertices of a regular hexagon
- Constant amplitude $A = 1.0$
- Wavelength $\lambda = 1.0$
- Frequency $f = 1.0$ Hz
- Time snapshot at $t = 0$

---

## 🐍 Full Python Code (Simulation + Visualization)

```python
import numpy as np
import matplotlib.pyplot as plt

# --- Constants ---
A = 1.0                      # Amplitude
λ = 1.0                      # Wavelength
f = 1.0                      # Frequency (Hz)
ω = 2 * np.pi * f            # Angular frequency
k = 2 * np.pi / λ            # Wavenumber
φ = 0                        # Phase
t = 0                        # Time (snapshot)

# --- Grid setup ---
x = np.linspace(-6, 6, 800)
y = np.linspace(-6, 6, 800)
X, Y = np.meshgrid(x, y)

# --- Source setup (Regular Hexagon) ---
N = 6
radius = 3.0
angles = np.linspace(0, 2 * np.pi, N, endpoint=False)
sources = [(radius * np.cos(θ), radius * np.sin(θ)) for θ in angles]

# --- Compute total wave ---
η_total = np.zeros_like(X)
for (x0, y0) in sources:
    R = np.sqrt((X - x0)**2 + (Y - y0)**2)
    R[R == 0] = 1e-6  # Avoid division by zero
    η = A / np.sqrt(R) * np.cos(k * R - ω * t + φ)
    η_total += η

# --- Plot interference pattern ---
plt.figure(figsize=(10, 8))
plt.pcolormesh(X, Y, η_total, shading='auto', cmap='RdBu')
plt.colorbar(label='Wave Displacement')
plt.title('Circular Wave Interference Pattern (t = 0)', fontsize=14)
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.axis('equal')
plt.grid(True, which='both', linestyle='--', linewidth=0.5)
plt.tight_layout()
plt.show()
