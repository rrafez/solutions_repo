# 📦 Gerekli kütüphaneleri içe aktar
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp
import os

# 🔧 Parametreler
gamma = 0.2         # Sönümleme katsayısı
omega0 = 1.5        # Doğal frekans
A = 1.2             # Sürükleyici kuvvet genliği
omega = 2/3         # Sürükleyici frekans

# 🎯 Diferansiyel denklem
def pendulum(t, y):
    theta, omega_theta = y
    dtheta_dt = omega_theta
    domega_dt = -gamma * omega_theta - omega0**2 * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# ⏱️ Zaman aralığı ve başlangıç koşulları
t = np.linspace(0, 100, 10000)
y0 = [0.1, 0.0]

# 📁 figures klasörü oluştur
os.makedirs("figures", exist_ok=True)

# 🌀 ODE çözümü
sol = solve_ivp(pendulum, [t[0], t[-1]], y0, t_eval=t, method='RK45')

# 📊 Figure 1: θ(t)
plt.figure(figsize=(10,4))
plt.plot(t, sol.y[0], color='darkblue')
plt.title("Figure 1: Angular Displacement θ(t)")
plt.xlabel("Time [s]")
plt.ylabel("Angle [rad]")
plt.grid(True)
plt.tight_layout()
plt.savefig("figures/theta_vs_time.png", dpi=300)
plt.close()

# 🔁 Figure 2: Phase Portrait
plt.figure(figsize=(6,6))
plt.plot(sol.y[0], sol.y[1], lw=0.5, color='darkgreen')
plt.title("Figure 2: Phase Space (θ vs ω)")
plt.xlabel("θ [rad]")
plt.ylabel("Angular Velocity ω [rad/s]")
plt.grid(True)
plt.tight_layout()
plt.savefig("figures/phase_portrait.png", dpi=300)
plt.close()

# 📍 Figure 3: Poincaré Section
T = 2 * np.pi / omega
poincare_t = np.arange(0, 100, T)
points = []

for ti in poincare_t:
    idx = np.abs(t - ti).argmin()
    points.append([sol.y[0][idx], sol.y[1][idx]])

points = np.array(points)

plt.figure(figsize=(6,6))
plt.plot(points[:,0], points[:,1], 'o', ms=2, color='maroon')
plt.title("Figure 3: Poincaré Section")
plt.xlabel("θ [rad]")
plt.ylabel("ω [rad/s]")
plt.grid(True)
plt.tight_layout()
plt.savefig("figures/poincare_section.png", dpi=300)
plt.close()

# 📉 Figure 4: Bifurcation Diagram
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

plt.figure(figsize=(10,6))
for i, sampled in enumerate(bifurcation):
    A_val = A_vals[i]
    plt.plot([A_val]*len(sampled), sampled, 'k.', ms=0.5)

plt.title("Figure 4: Bifurcation Diagram (θ mod 2π vs A)")
plt.xlabel("Driving Amplitude A")
plt.ylabel("θ (mod 2π)")
plt.grid(True)
plt.tight_layout()
plt.savefig("figures/bifurcation_diagram.png", dpi=300)
plt.close()

print("✅ All figures saved in 'figures/' folder.")
