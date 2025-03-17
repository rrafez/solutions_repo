# **Problem 1: Investigating the Range as a Function of the Angle of Projection**

## **1. Theoretical Foundation**
Projectile motion is a type of two-dimensional motion where an object is launched into the air with an initial velocity $v_0$ at an angle $\theta$ relative to the horizontal. The motion can be analyzed by breaking it into horizontal (x) and vertical (y) components.

### **1.1 Equations of Motion**
The horizontal and vertical components of the initial velocity are:
$$v_{0x} = v_0 \cos(\theta)$$
$$v_{0y} = v_0 \sin(\theta)$$

Using the kinematic equations, the motion in each direction is governed by:
- **Horizontal motion (constant velocity, no acceleration in the ideal case):**
  $$x = v_{0x} t = v_0 \cos(\theta) t$$
- **Vertical motion (accelerated due to gravity):**
  $$ y = v_{0y} t - \frac{1}{2} g t^2 $$

where:
- $g$ is the acceleration due to gravity $(9.81 \text{ m/s}^2)$
- $t$ is the time of flight.

### **1.2 Time of Flight**
The time of flight is determined by solving for when the projectile returns to the ground $(y = 0)$:
$$ t = \frac{2 v_0 \sin(\theta)}{g} $$

### **1.3 Range Equation**
The range $R$ is the horizontal distance traveled when the projectile lands:
$$ R = v_{0x} \cdot t = v_0 \cos(\theta) \cdot \frac{2 v_0 \sin(\theta)}{g} $$

Using the identity $2 \sin(\theta) \cos(\theta) = \sin(2\theta)$, we get:
$$ R = \frac{v_0^2 \sin(2\theta)}{g} $$

## **2. Analysis of the Range**
- The range is maximized when $\sin(2\theta) = 1$, which occurs at $2\theta = 90^\circ$, or $\theta = 45^\circ$.
- If the initial velocity $v_0$ increases, the range increases quadratically.
- If gravity $g$ increases (e.g., on another planet), the range decreases.

## **3. Practical Applications**
- **Sports:** Understanding projectile motion is crucial in games like soccer, basketball, and golf.
- **Engineering:** Used in ballistics, rocketry, and artillery targeting systems.
- **Real-World Effects:** Air resistance, wind, and uneven terrain can significantly alter the theoretical range.

## **4. Implementation: Python Simulation**
The following Python script simulates projectile motion and plots the range as a function of the angle of projection.

```python
import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, g=9.81):
    angles = np.linspace(0, 90, 100)  # Angle range from 0 to 90 degrees
    angles_rad = np.radians(angles)  # Convert degrees to radians
    ranges = (v0**2 * np.sin(2 * angles_rad)) / g  # Compute range
    
    plt.figure(figsize=(8, 5))
    plt.plot(angles, ranges, label=f'v0 = {v0} m/s')
    plt.xlabel("Angle (degrees)")
    plt.ylabel("Range (m)")
    plt.title("Projectile Range vs. Launch Angle")
    plt.legend()
    plt.grid()
    plt.show()

# Example usage
projectile_range(v0=20)  # Change v0 to analyze different scenario