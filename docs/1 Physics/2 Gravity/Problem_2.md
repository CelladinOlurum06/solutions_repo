 # Problem 2
 # 🚀 Problem 2: Escape Velocities and Cosmic Velocities

## 🎯 Motivation

Space travel depends critically on understanding the gravitational forces of celestial bodies and the energy required to overcome them. Concepts such as **escape velocity** and **cosmic velocities** define the speed thresholds necessary for different types of motion — from stable orbiting to escaping a planet, or even a solar system entirely.

These are not just theoretical physics concepts, but real-world tools used in designing missions, launching satellites, planning interplanetary trips, and one day — perhaps — achieving interstellar travel.

---

## 🌍 Definitions of Cosmic Velocities

In classical mechanics and astrodynamics, three main types of "cosmic velocities" are defined, each corresponding to a specific threshold in orbital mechanics:

---

### 1. 🛰️ First Cosmic Velocity (\(v_1\)) – Orbital Velocity

- **Definition:**  
  The minimum horizontal velocity needed for an object to enter a stable circular orbit just above the surface of a celestial body (ignoring atmosphere).

- **Physical Interpretation:**  
  If a spacecraft reaches this velocity tangential to the surface, it will fall around the planet instead of onto it — achieving orbit.

- **Formula:**  
  $$
  v_1 = \sqrt{\frac{GM}{R}}
  $$
  where:
  - \(G\) is the gravitational constant: \(6.67430 \times 10^{-11} \, \text{m}^3 \cdot \text{kg}^{-1} \cdot \text{s}^{-2}\)
  - \(M\) is the mass of the celestial body (kg)
  - \(R\) is the radius of the celestial body (m)

---

### 2. 🚀 Second Cosmic Velocity (\(v_2\)) – Escape Velocity

- **Definition:**  
  The minimum velocity required to completely escape the gravitational pull of a celestial body without further propulsion.

- **Physical Interpretation:**  
  At this velocity, the total mechanical energy (kinetic + potential) of the spacecraft becomes zero — it can reach infinity with zero velocity.

- **Formula:**  
  $$
  v_2 = \sqrt{\frac{2GM}{R}} = \sqrt{2} \cdot v_1
  $$

---

### 3. 🌌 Third Cosmic Velocity (\(v_3\)) – Interstellar Escape Velocity

- **Definition:**  
  The speed needed to escape both the planet’s gravity and the gravity of its parent star (e.g., the Sun), and leave the solar system.

- **Physical Interpretation:**  
  A spacecraft launched from Earth would need additional energy to escape not only Earth’s gravity but also the Sun’s gravitational influence.

- **Note:**  
  \(v_3\) depends on the orbital velocity of the planet around the star and the relative direction of launch (same or opposite to orbital motion). It's generally derived from the total energy needed to reach the star system’s edge.

---

## 📐 Mathematical Background

### Gravitational Potential Energy:
$$
U = -\frac{GMm}{r}
$$

### Kinetic Energy:
$$
K = \frac{1}{2}mv^2
$$

Setting total mechanical energy \(E = K + U = 0\) gives the escape condition:
$$
\frac{1}{2}mv^2 - \frac{GMm}{r} = 0 \Rightarrow v = \sqrt{\frac{2GM}{r}}
$$

This is the essence of escape velocity (\(v_2\)). For orbital motion, we only need to balance centripetal and gravitational forces:
$$
\frac{mv^2}{r} = \frac{GMm}{r^2} \Rightarrow v = \sqrt{\frac{GM}{r}} = v_1
$$

---

## 🧮 Python Code: Calculate and Visualize Cosmic Velocities

import numpy as np
import matplotlib.pyplot as plt

# Gravitational constant
G = 6.67430e-11  # in m^3 kg^-1 s^-2

# Celestial bodies: name, mass (kg), radius (m)
bodies = {
    'Earth': (5.972e24, 6.371e6),
    'Mars': (6.417e23, 3.3895e6),
    'Jupiter': (1.898e27, 6.9911e7)
}

# Compute v1 and v2 for each body
results = {}
for body, (mass, radius) in bodies.items():
    v1 = np.sqrt(G * mass / radius)  # v1 = sqrt(GM / R)
    v2 = np.sqrt(2) * v1             # v2 = sqrt(2) * v1
    results[body] = (v1, v2)

# Prepare data for visualization
labels = list(results.keys())
v1_vals = [results[body][0] for body in labels]
v2_vals = [results[body][1] for body in labels]

x = np.arange(len(labels))
width = 0.35

# Plotting
plt.figure(figsize=(10, 6))
plt.bar(x - width/2, v1_vals, width, label='First Cosmic Velocity ($v_1$)')
plt.bar(x + width/2, v2_vals, width, label='Second Cosmic Velocity ($v_2$)')
plt.xticks(x, labels)
plt.ylabel('Velocity (m/s)')
plt.title('Cosmic Velocities for Different Celestial Bodies')
plt.legend()
plt.grid(True, linestyle='--', alpha=0.5)
plt.tight_layout()
plt.show()
