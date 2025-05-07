# Problem: Circular Wave Interference from Multiple Sources

## Motivation
Interference on a water surface provides a beautiful, tangible example of how waves interact. By studying these patterns from coherent point sources arranged in a regular polygon, we can observe and analyze wave superposition, constructive interference (bright spots), and destructive interference (dark spots).

## Physical Background

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

## Parameters and Setup

We consider:
- **$N = 6$ sources** arranged at the vertices of a regular hexagon
- Constant amplitude $A = 1.0$
- Wavelength $\lambda = 1.0$
- Frequency $f = 1.0$ Hz
- Time snapshot at $t = 0$

