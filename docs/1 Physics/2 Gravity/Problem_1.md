# Gravity: Orbital Period and Orbital Radius

## Motivation

The relationship between the square of the orbital period (T) and the cube of the orbital radius (r), known as **Kepler's Third Law**, is a fundamental principle in celestial mechanics. Understanding this connection allows us to analyze satellite motions, planetary systems, and broader gravitational phenomena.

---

## Derivation of the Relationship

**Newton's Law of Gravitation:**
\[ F = \frac{G M m}{r^2} \]

**Centripetal Force for Circular Motion:**
\[ F = m \frac{v^2}{r} \]

Equating gravitational force to centripetal force:
\[ \frac{G M m}{r^2} = m \frac{v^2}{r} \]

Simplifying:
\[ v^2 = \frac{G M}{r} \]

Orbital period \(T\) is the time to complete one full circle:
\[ T = \frac{2 \pi r}{v} \quad \Rightarrow \quad v = \frac{2 \pi r}{T} \]

Substitute into the velocity equation:
\[ \left(\frac{2 \pi r}{T}\right)^2 = \frac{G M}{r} \]

Expand:
\[ \frac{4 \pi^2 r^2}{T^2} = \frac{G M}{r} \]

Rearrange:
\[ T^2 = \frac{4 \pi^2}{G M} r^3 \]

**Thus, we derive:**
\[ T^2 \propto r^3 \]

This is **Kepler's Third Law** for circular orbits.

---

## Implications for Astronomy

- **Calculating Masses:** Knowing a satellite's orbital radius and period allows astronomers to calculate the mass of the central body (e.g., Earth, Sun).
- **Determining Distances:** For distant planets and moons, measuring the period gives an estimate of their distance from the central mass.
- **Comparative Analysis:** Planets farther from the Sun have much longer periods, as seen in our Solar System.

---

## Real-World Examples

**The Moon's orbit around Earth:**
- Radius \( r \approx 3.84 \times 10^8 \) m
- Period \( T \approx 27.3 \) days

**Earth's orbit around the Sun:**
- Radius \( r \approx 1.496 \times 10^{11} \) m
- Period \( T \approx 365.25 \) days

They both obey the \( T^2 \propto r^3 \) relation.

---

# Computational Model: Circular Orbit Simulation

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)
M_earth = 5.972e24  # Mass of the Earth (kg)

# Orbital radii (in meters)
radii = np.linspace(7e6, 4e8, 100)  # from 7000 km to 400,000 km

# Calculate periods using Kepler's Third Law
periods = 2 * np.pi * np.sqrt(radii**3 / (G * M_earth))

# Plot Period^2 vs Radius^3
plt.figure()
plt.plot(radii**3, periods**2, 'o')
plt.xlabel("Radius^3 (m^3)")
plt.ylabel("Period^2 (s^2)")
plt.title("Kepler's Third Law Verification")
plt.grid(True)
plt.show()

# Plot Orbit Trajectories
fig, ax = plt.subplots()
for r in np.linspace(7e6, 4e8, 5):
    theta = np.linspace(0, 2*np.pi, 100)
    x = r * np.cos(theta)
    y = r * np.sin(theta)
    ax.plot(x, y, label=f"r = {r/1e3:.0f} km")

ax.set_xlabel("x (m)")
ax.set_ylabel("y (m)")
ax.set_aspect('equal')
ax.set_title("Circular Orbits Around Earth")
ax.legend()
plt.grid(True)
plt.show()
```

---

# Graphical Representations

- **First Graph:** Linear relation between \( T^2 \) and \( r^3 \), confirming Kepler's Law.
- **Second Graph:** Multiple circular orbits of different radii around the Earth.

---

# Extension to Elliptical Orbits

Kepler's Third Law extends to elliptical orbits by replacing the radius with the semi-major axis \( a \):

\[ T^2 \propto a^3 \]

Where \( a \) is the average distance from the focus (not the exact radius).

- Elliptical orbits are common for most celestial bodies.
- Planets sweep out equal areas in equal times (Kepler's Second Law).

Thus, while circular orbits are a special case, the general law remains valid for all orbital shapes.

---

# Conclusion

Through derivation, simulation, and real-world examples, we've shown that the square of the orbital period is proportional to the cube of the orbital radius. This fundamental relationship continues to guide our understanding of gravitational systems across the universe.

---

# References

- Isaac Newton, *Principia Mathematica*, 1687
- Johannes Kepler, *Astronomia Nova*, 1609
- NASA Planetary Fact Sheets
# Problem 1