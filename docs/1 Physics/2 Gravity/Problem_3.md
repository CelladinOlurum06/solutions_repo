#  Problem 3
# Trajectories of a Freely Released Payload Near Earth

## 🎯 Motivation

When a payload is released from a spacecraft near Earth, its future motion depends entirely on its **initial conditions** — position, velocity, and the local gravitational field. The resulting path may be:

- A **suborbital** fall back to Earth,
- A **stable circular** or **elliptical orbit**,
- A **parabolic** path (exact escape),
- Or a **hyperbolic** trajectory (true escape from Earth's gravity).

Understanding and predicting these trajectories is critical for:

- Designing satellite deployments,
- Planning reentry operations,
- Performing interplanetary injections.

---

## 📐 Physical Background

We assume that the only force acting on the payload is **Earth's gravity**, modeled by **Newton's Law of Universal Gravitation**.

### Newton's Law of Gravitation:

$$
\vec{F} = -\frac{GMm}{r^2} \hat{r}
$$

Where:

- \( G = 6.67430 \times 10^{-11} \, \text{m}^3/\text{kg}/\text{s}^2 \) is the gravitational constant,
- \( M \) is the mass of the Earth,
- \( m \) is the mass of the payload,
- \( r \) is the distance from the Earth's center,
- \( \hat{r} \) is the unit vector pointing from the payload toward the center of Earth.

Using Newton’s Second Law:

$$
\vec{a} = \frac{\vec{F}}{m} = -\frac{GM}{r^2} \hat{r}
$$

Thus, the acceleration depends only on position, not mass — so the trajectory is **independent of the payload's mass**.

---

## 🧠 Theoretical Velocity Thresholds

Let \( R \) be Earth's radius and \( h \) the altitude of release. Then the radial distance is:

$$
r = R + h
$$

We define three key velocity thresholds at altitude \( r \):

### 1. Circular Orbit Velocity:
The velocity needed to maintain a circular orbit at radius \( r \):

$$
v_{\text{circular}} = \sqrt{\frac{GM}{r}}
$$

### 2. Escape Velocity:
The minimum velocity needed to escape Earth’s gravity (assuming no further propulsion):

$$
v_{\text{escape}} = \sqrt{\frac{2GM}{r}} = \sqrt{2} \cdot v_{\text{circular}}
$$

---

## 🧮 Numerical Simulation

Using numerical integration (e.g., Runge-Kutta method via `scipy.integrate.solve_ivp`), we simulate the path of the payload for various initial velocities and directions.

### Initial Conditions:
- Altitude: \( h = 300\,\text{km} \)
- Initial position: \( [r_0, 0] \)
- Initial velocities:
  - **Suborbital**: \( v < v_{\text{circular}} \)
  - **Circular Orbit**: \( v = v_{\text{circular}} \)
  - **Escape**: \( v \geq v_{\text{escape}} \)

---

## 💻 Python Implementation (Sample Code)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
G = 6.67430e-11        # Gravitational constant (m^3/kg/s^2)
M = 5.972e24           # Mass of Earth (kg)
R = 6.371e6            # Radius of Earth (m)

# Gravitational acceleration
def gravity(t, state):
    x, y, vx, vy = state
    r = np.sqrt(x**2 + y**2)
    ax = -G * M * x / r**3
    ay = -G * M * y / r**3
    return [vx, vy, ax, ay]

# Initial altitude
altitude = 300e3
r0 = R + altitude

# Velocity thresholds
v_circular = np.sqrt(G * M / r0)
v_escape = np.sqrt(2) * v_circular

# Scenarios
scenarios = {
    "Suborbital": [r0, 0, 0, 5000],
    "Circular Orbit": [r0, 0, 0, v_circular],
    "Escape Trajectory": [r0, 0, 0, v_escape]
}

# Time and simulation
t_span = (0, 10000)
t_eval = np.linspace(*t_span, 2000)

# Plotting
plt.figure(figsize=(10, 10))

for label, state0 in scenarios.items():
    sol = solve_ivp(gravity, t_span, state0, t_eval=t_eval, rtol=1e-8)
    x, y = sol.y[0], sol.y[1]
    plt.plot(x / 1000, y / 1000, label=label)

# Earth
theta = np.linspace(0, 2*np.pi, 300)
earth_x = R * np.cos(theta) / 1000
earth_y = R * np.sin(theta) / 1000
plt.fill(earth_x, earth_y, 'lightblue', label='Earth')

plt.title("Trajectories of a Freely Released Payload")
plt.xlabel("x (km)")
plt.ylabel("y (km)")
plt.axis('equal')
plt.grid(True)
plt.legend()
plt.show()
