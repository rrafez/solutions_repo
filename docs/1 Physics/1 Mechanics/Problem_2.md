# 🌀 Investigating the Dynamics of a Forced Damped Pendulum

## 🎯 Motivation

The **forced damped pendulum** is a classical nonlinear system that exhibits rich dynamics due to the interaction of damping, restoring forces, and external periodic driving. As system parameters vary, the motion can transition from simple periodic motion to chaotic behavior.

Understanding this system provides insights into:
- Mechanical resonance
- Vibration control in structures
- Electrical analogs (RLC circuits)
- Energy harvesting and biomechanical systems

---

## 🧠 1. Theoretical Foundation

### ⚙️ Governing Equation

The motion of a forced damped pendulum is governed by:

\[
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = A \cos(\omega t)
\]

Where:
- \(\theta(t)\): Angular displacement
- \(\gamma\): Damping coefficient
- \(\omega_0 = \sqrt{\frac{g}{L}}\): Natural frequency
- \(A\): Driving force amplitude
- \(\omega\): Driving frequency

---

### 🧪 Small-Angle Approximation

When \(|\theta|\) is small: \(\sin(\theta) \approx \theta\), giving the linearized form:

\[
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t)
\]

This is the equation of a **driven damped harmonic oscillator**.

---

### 📐 Approximate Solution (Linear Case)

Assuming a solution:

\[
\theta(t) = \theta_0 \cos(\omega t - \phi)
\]

We find:

\[
\theta_0 = \frac{A}{\sqrt{(\omega_0^2 - \omega^2)^2 + (\gamma \omega)^2}}, \quad
\tan(\phi) = \frac{\gamma \omega}{\omega_0^2 - \omega^2}
\]

---

### 🔊 Resonance

Resonance occurs near:

\[
\omega_{\text{res}} \approx \sqrt{\omega_0^2 - \frac{\gamma^2}{2}}
\]

At this frequency, the amplitude reaches a maximum, especially when damping is low.

---

## 💻 2. Python Simulation and Analysis

```python
# 📦 Import required libraries
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# 🔧 Parameters
gamma = 0.2         # Damping coefficient
omega0 = 1.5        # Natural frequency
A = 1.2             # Driving amplitude
omega = 2/3         # Driving frequency

# 🧮 Define the differential equation
def pendulum(t, y):
    theta, omega_theta = y
    dtheta_dt = omega_theta
    domega_dt = -gamma * omega_theta - omega0**2 * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# ⏱️ Time span and initial conditions
t = np.linspace(0, 100, 10000)
y0 = [0.1, 0.0]  # Initial angle and angular velocity

# 🌀 Solve the ODE
sol = solve_ivp(pendulum, [t[0], t[-1]], y0, t_eval=t, method='RK45')

# 📈 Plot θ(t)
plt.figure(figsize=(10,4))
plt.plot(t, sol.y[0])
plt.title("θ(t) - Forced Damped Pendulum")
plt.xlabel("Time")
plt.ylabel("Angle (rad)")
plt.grid()
plt.show()

# 🔁 Phase Space Plot
plt.figure(figsize=(6,6))
plt.plot(sol.y[0], sol.y[1], lw=0.5)
plt.title("Phase Portrait: θ vs ω")
plt.xlabel("θ (rad)")
plt.ylabel("Angular Velocity ω (rad/s)")
plt.grid()
plt.show()

# 📍 Poincaré Section
T = 2 * np.pi / omega
poincare_t = np.arange(0, 100, T)
points = []

for ti in poincare_t:
    idx = np.abs(t - ti).argmin()
    points.append([sol.y[0][idx], sol.y[1][idx]])

points = np.array(points)

plt.figure(figsize=(6,6))
plt.plot(points[:,0], points[:,1], 'o', ms=2)
plt.title("Poincaré Section")
plt.xlabel("θ (rad)")
plt.ylabel("ω (rad/s)")
plt.grid()
plt.show()

# 📉 Bifurcation Diagram
A_vals = np.linspace(1.0, 1.5, 100)
bifurcation = []

for A_val in A_vals:
    def pend(t, y):
        theta, v = y
        return [v, -gamma * v - omega0**2 * np.sin(theta) + A_val * np.cos(omega * t)]
    
    sol = solve_ivp(pend, [0, 300], [0.1, 0.0], t_eval=np.linspace(0, 300, 10000))
    T_drive = 2 * np.pi / omega
    sampled = []

    for ti in np.arange(200, 300, T_drive):
        idx = np.abs(sol.t - ti).argmin()
        sampled.append(sol.y[0][idx] % (2*np.pi))

    bifurcation.append(sampled)

# 📊 Plot Bifurcation Diagram
plt.figure(figsize=(10,6))
for i, sampled in enumerate(bifurcation):
    A_val = A_vals[i]
    plt.plot([A_val]*len(sampled), sampled, 'k.', ms=0.5)

plt.title("Bifurcation Diagram: θ (mod 2π) vs A")
plt.xlabel("Driving Amplitude A")
plt.ylabel("θ (mod 2π)")
plt.grid()
plt.show()
