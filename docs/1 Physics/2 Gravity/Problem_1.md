# **Problem 1: Investigating the Relationship Between Orbital Period and Orbital Radius**

## **1. Theoretical Foundation**

In orbital mechanics, celestial bodies move under the influence of gravity. One of the most important relationships is **Kepler’s Third Law**, which states:

> The square of the orbital period ($T^2$) is proportional to the cube of the orbital radius ($r^3$).

### **1.1 Derivation of the Formula**

The gravitational force provides the centripetal force necessary for a body to stay in a circular orbit:

$$
F_{\text{gravity}} = \frac{G M m}{r^2}
\quad \text{and} \quad
F_{\text{centripetal}} = \frac{m v^2}{r}
$$

Setting them equal:

$$
\frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Simplifying:

$$
v^2 = \frac{G M}{r}
$$

The orbital period $T$ (time to complete one full orbit) is:

$$
T = \frac{2\pi r}{v}
$$

Substituting $v$:

$$
T = 2\pi r \sqrt{\frac{r}{G M}}
$$

Squaring both sides:

$$
T^2 = \frac{4\pi^2 r^3}{G M}
$$

Thus:

$$
T^2 \propto r^3
$$

---

## **2. Analysis of the Relationship**

- As the orbital radius $r$ increases, the period $T$ increases.
- A heavier central body (larger $M$) results in shorter periods for the same radius.
- This relationship is fundamental for determining distances and masses in astronomy.

---

## **3. Practical Applications**

- **Satellite Deployment:** Calculating correct orbits for satellites (e.g., GPS, weather satellites).
- **Planetary Studies:** Determining planetary masses by studying moons' orbits.
- **Space Missions:** Planning spacecraft trajectories around planets and moons.

---

## **4. Implementation: Python Simulation**

Below is a Python script that simulates the relationship between $T^2$ and $r^3$ for circular orbits.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24     # mass of Earth (kg)

# Function to compute orbital period
def orbital_period(r):
    return 2 * np.pi * np.sqrt(r**3 / (G * M))

# Define a range of orbital radii
radii = np.linspace(7e6, 5e7, 100)  # in meters
periods = orbital_period(radii)     # in seconds

# Plotting T^2 vs r^3
plt.figure(figsize=(8, 5))
plt.plot(radii**3, periods**2, label='T² vs r³')
plt.xlabel("Orbital Radius Cubed ($r^3$) [m³]")
plt.ylabel("Orbital Period Squared ($T^2$) [s²]")
plt.title("Verification of Kepler's Third Law")
plt.legend()
plt.grid()
plt.show()

# Plotting Orbits
theta = np.linspace(0, 2*np.pi, 100)

plt.figure(figsize=(8,8))
for r in np.linspace(7e6, 4e7, 5):
    x = r * np.cos(theta)
    y = r * np.sin(theta)
    plt.plot(x, y, label=f'Radius = {r/1000:.0f} km')

plt.scatter(0, 0, color='yellow', label='Earth')  # Earth at center
plt.xlabel("x position (m)")
plt.ylabel("y position (m)")
plt.title("Circular Orbits Visualization")
plt.legend()
plt.grid()
plt.axis('equal')
plt.show()
```

---

## **5. Explanation of the Graphs**

### **Graph 1: T² vs r³**

- This graph demonstrates a straight-line relationship between $T^2$ and $r^3$.
- As the cube of the orbital radius increases, the square of the period increases linearly.
- This confirms **Kepler’s Third Law** experimentally.

### **Graph 2: Visualization of Circular Orbits**

- Shows several circular orbits with different radii around Earth.
- Larger radii result in larger orbital paths and longer periods.

---

## **6. Extension to Elliptical Orbits**

Kepler's Third Law generalizes for elliptical orbits using the semi-major axis $a$ instead of radius $r$:

$$
T^2 \propto a^3
$$

In elliptical motion:
- The speed is highest at periapsis and lowest at apoapsis.
- The total mechanical energy remains constant.

---

## **7. Frequently Asked Questions (FAQ)**

### **Q1: What does Kepler's Third Law state?**

> $T^2$ is proportional to $r^3$ for bodies in circular orbit.

### **Q2: Does satellite mass affect its orbital period?**

> No. The mass of the orbiting object cancels out.

### **Q3: What happens if the central mass increases?**

> The orbital period $T$ becomes shorter for a given orbital radius $r$.

### **Q4: Can Kepler's Law apply to exoplanets?**

> Yes, it applies universally to any orbiting body.

### **Q5: How is Kepler's Law used in missions?**

> It helps predict satellite orbits, plan trajectories, and study planetary systems.

