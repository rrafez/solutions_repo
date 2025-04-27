# Gravity: Orbital Period and Orbital Radius

## Motivation
The relationship between the square of the orbital period and the cube of the orbital radius, known as **Kepler's Third Law**, is fundamental to celestial mechanics. It enables the calculation of planetary motions and satellite dynamics, providing essential insights into gravitational interactions in the universe.

## Derivation of the Relationship

For a circular orbit:

1. The gravitational force provides the necessary centripetal force:

   ```
   F_gravity = F_centripetal
   ```

2. Gravitational force:

   ```
   F_gravity = (G * M * m) / r^2
   ```

3. Centripetal force:

   ```
   F_centripetal = (m * v^2) / r
   ```

4. Setting them equal:

   ```
   (G * M * m) / r^2 = (m * v^2) / r
   ```

   Simplify (mass m cancels out):

   ```
   (G * M) / r^2 = v^2 / r
   ```

   Thus:

   ```
   v^2 = (G * M) / r
   ```

5. Orbital period T is the time to complete one circle:

   ```
   T = (2 * π * r) / v
   ```

   Therefore:

   ```
   v = (2 * π * r) / T
   ```

6. Substitute for v in v²:

   ```
   ((2 * π * r) / T)^2 = (G * M) / r
   ```

7. Expanding:

   ```
   (4 * π^2 * r^2) / T^2 = (G * M) / r
   ```

8. Rearranging:

   ```
   T^2 = (4 * π^2 / G * M) * r^3
   ```

Thus, **T² is proportional to r³** for a given central mass M.

---

## Implications for Astronomy

- **Planetary Mass Estimation**: By knowing the period and radius, the mass of planets and stars can be determined.
- **Satellite Engineering**: Used for designing satellite orbits like GPS systems.
- **Exoplanet Detection**: Helps detect exoplanets based on star wobbling.

---

## Real-World Examples

### 1. The Moon's orbit around Earth
- Orbital radius ≈ 384,400 km
- Orbital period ≈ 27.3 days

Verifying \(T^2 \propto r^3\) gives a very close match.

### 2. Planets in the Solar System
- Jupiter's moons
- Saturn's rings
- Distant exoplanets

All obey Kepler's Third Law.

---

## Computational Model

### Python Code

```python
# orbital_simulation.py

import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24     # mass of Earth (kg)

# Function to compute orbital period
def orbital_period(r):
    return 2 * np.pi * np.sqrt(r**3 / (G * M))

# Generate a range of orbital radii (from 7000 km to 50000 km)
radii = np.linspace(7e6, 5e7, 100)  # meters
periods = orbital_period(radii)     # seconds

# Plotting T^2 vs r^3
plt.figure(figsize=(10,6))
plt.plot(radii**3, periods**2, marker='o', linestyle='-')
plt.xlabel('Orbital Radius Cubed ($r^3$) [m³]')
plt.ylabel('Orbital Period Squared ($T^2$) [s²]')
plt.title('Kepler\'s Third Law Verification')
plt.grid(True)
plt.show()

# Plotting actual orbits (for visualization)
theta = np.linspace(0, 2*np.pi, 100)

plt.figure(figsize=(8,8))
for r in np.linspace(7e6, 4e7, 5):
    x = r * np.cos(theta)
    y = r * np.sin(theta)
    plt.plot(x, y, label=f'r = {r/1000:.0f} km')

plt.scatter(0, 0, color='yellow', label='Earth')  # Earth at the center
plt.xlabel('x [m]')
plt.ylabel('y [m]')
plt.legend()
plt.title('Visualization of Circular Orbits')
plt.grid(True)
plt.axis('equal')
plt.show()
```

---

## Graphical Results

### 1. \(T^2\) vs \(r^3\) Plot

- Demonstrates a linear relationship between \(T^2\) and \(r^3\), verifying Kepler’s Third Law.

### 2. Circular Orbits Visualization

- Shows different satellite orbits around Earth.

---

## Extension to Elliptical Orbits

Kepler’s Third Law extends to elliptical orbits if we replace \(r\) with the semi-major axis \(a\):

```
T^2 ∝ a^3
```

In elliptical orbits:
- Speed varies (faster at periapsis, slower at apoapsis).
- Gravitational potential energy and kinetic energy exchange, but total energy remains constant.

---

## Conclusion

We have derived, simulated, and verified Kepler's Third Law for circular orbits through analytical derivation, real-world examples, and computational simulation. This foundational principle remains vital in modern astronomy and space exploration.

---

