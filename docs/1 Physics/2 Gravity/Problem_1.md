# **Problem 1: Investigating the Relationship Between Orbital Period and Orbital Radius**

## **1. Theoretical Foundation**

Orbital mechanics describes how celestial bodies move under the influence of gravitational forces. A key concept is **Kepler's Third Law**, which states that the square of the orbital period ($T^2$) is proportional to the cube of the orbital radius ($r^3$).

### **1.1 Equations of Motion**

In circular orbits, the gravitational force provides the necessary centripetal force:

Gravitational Force:
$$
F_{\text{gravity}} = \frac{G M m}{r^2}
$$

Centripetal Force:
$$
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

The orbital period $T$ is the time taken to complete one orbit:

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

Thus, the square of the orbital period is proportional to the cube of the orbital radius:

$$
T^2 \propto r^3
$$

---

## **2. Analysis of the Relationship**

- The larger the orbital radius, the longer the period of revolution.
- A more massive central body (larger $M$) results in shorter orbital periods for a given radius.
- This relationship is foundational for determining distances and masses in astronomy.

---

## **3. Practical Applications**

- **Satellite Deployment:** Designing satellite orbits around Earth or other planets.
- **Planetary Mass Calculation:** Determining the mass of celestial bodies by observing their moons.
- **Exoplanet Studies:** Finding exoplanets and their orbital characteristics around distant stars.

---

## **4. Implementation: Python Simulation**

The following Python script simulates circular orbits and verifies the relationship between $T^2$ and $r^3$.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24     # mass of Earth (kg)

# Function to compute orbital period
def orbital_period(r):
    return 2 * np.pi * np.sqrt(r**3 / (G * M))

# Range of orbital radii
radii = np.linspace(7e6, 5e7, 100)  # from 7000 km to 50000 km (converted to meters)
periods = orbital_period(radii)

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
plt.title("Circular Orbits around Earth")
plt.legend()
plt.grid()
plt.axis('equal')
plt.show()
```

---

## **5. Explanation of the Graphs**

### **Graph 1: T² vs r³**

This graph demonstrates the linear relationship between the square of the orbital period ($T^2$) and the cube of the orbital radius ($r^3$).

- As $r^3$ increases, $T^2$ also increases linearly.
- This verifies **Kepler's Third Law** for circular orbits.

### **Graph 2: Visualization of Orbits**

- Shows circular orbits for satellites at different radii.
- Earth is placed at the center.
- Larger orbital radius corresponds to a larger orbit and a longer period.

These visualizations help understand how satellites and moons move around their parent bodies.

---

## **6. Frequently Asked Questions (FAQ)**

### **1. What does Kepler's Third Law state for circular orbits?**
- It states that the square of the orbital period ($T^2$) is directly proportional to the cube of the orbital radius ($r^3$).

### **2. Does the mass of the satellite affect the orbital period?**
- No, the satellite's mass cancels out in the equations; only the central mass ($M$) and the orbital radius ($r$) matter.

### **3. How is this law useful in real-world applications?**
- It is used in calculating satellite orbits, determining planetary masses, and studying exoplanets.

### **4. What happens if the central body's mass increases?**
- If $M$ increases, the orbital period for a given radius decreases (i.e., objects orbit faster).

### **5. Does this relationship apply to elliptical orbits?**
- Yes, but $r$ is replaced with the semi-major axis ($a$) of the ellipse in the general form of Kepler's Third Law.

