# Problem 3
# 🛰️ Problem 3: Trajectories of a Freely Released Payload Near Earth

## 🎯 Motivation

In space missions, when a spacecraft releases a payload — such as a satellite or a reentry capsule — near Earth, the object's trajectory is determined by its **initial velocity**, **position**, and the **gravitational pull of Earth**.

Depending on these factors, the payload can:
- Enter a stable orbit (elliptical)
- Reenter Earth's atmosphere (suborbital)
- Escape Earth’s gravity (hyperbolic)
- Follow a parabolic or ballistic trajectory

Understanding these outcomes is critical in designing satellite deployments, reentry paths, and mission abort protocols.

---

## 🌌 Physical Principles

### Newton's Law of Gravitation:
$$
\vec{F} = -\frac{GMm}{r^2} \hat{r}
$$

Where:
- \(G\) is the gravitational constant
- \(M\) is the Earth's mass
- \(m\) is the payload's mass
- \(r\) is the distance from Earth's center
- The force is directed toward the center of Earth

### Equations of Motion:

Using Newton’s second law:
$$
\vec{F} = m \vec{a} \Rightarrow \vec{a} = -\frac{GM}{r^2} \hat{r}
$$

We numerically solve the position and velocity over time using:
- Euler's Method (simple)
- Runge-Kutta or `scipy.integrate.solve_ivp` (more accurate)

---

## 🧮 Python Simulation: Trajectory of a Payload Released Near Earth

import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
G = 6.67430e-11  # gravitational constant (m^3/kg/s^2)
M_earth = 5.972e24  # mass of Earth (kg)
R_earth = 6.371e6  # radius of Earth (m)

# Gravitational acceleration function
def gravity(t, state):
    x, y, vx, vy = state
    r = np.sqrt(x**2 + y**2)
    ax = -G * M_earth * x / r**3
    ay = -G * M_earth * y / r**3
    return [vx, vy, ax, ay]

# Initial conditions
altitude = 300e3  # 300 km above Earth
r0 = R_earth + altitude

# Try different initial velocities to simulate different cases
v_circular = np.sqrt(G * M_earth / r0)
v_escape = np.sqrt(2) * v_circular

initial_states = {
    "Suborbital": [r0, 0, 0, 5000],
    "Circular Orbit": [r0, 0, 0, v_circular],
    "Escape Trajectory": [r0, 0, 0, v_escape],
}

# Time span for simulation
t_span = (0, 10000)  # seconds
t_eval = np.linspace(*t_span, 2000)

# Plotting
plt.figure(figsize=(10, 10))

for label, state0 in initial_states.items():
    sol = solve_ivp(gravity, t_span, state0, t_eval=t_eval, rtol=1e-8)
    x, y = sol.y[0], sol.y[1]
    plt.plot(x / 1000, y / 1000, label=label)

# Plot Earth
theta = np.linspace(0, 2*np.pi, 300)
earth_x = R_earth * np.cos(theta) / 1000
earth_y = R_earth * np.sin(theta) / 1000
plt.fill(earth_x, earth_y, color='lightblue', label='Earth')

plt.title('Payload Trajectories Near Earth')
plt.xlabel('x (km)')
plt.ylabel('y (km)')
plt.axis('equal')
plt.grid(True)
plt.legend()
plt.show()
