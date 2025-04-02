# Problem 1
# Simulating the Effects of the Lorentz Force

## Motivation

The **Lorentz force** governs the motion of charged particles in electromagnetic fields:

\[
\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})
\]

Understanding this force is crucial in many real-world systems:
- **Cyclotrons** accelerate particles using magnetic fields.
- **Mass spectrometers** measure mass-to-charge ratios via curved paths.
- **Plasma confinement** in **tokamaks** uses magnetic fields to control hot ionized gases.

Simulating this numerically reveals how different field configurations affect particle motion — circular orbits, helices, or E×B drift.

---

## Applications of the Lorentz Force

- **Particle Accelerators**: Use strong magnetic fields to bend and focus particles (e.g., LHC).
- **Mass Spectrometry**: Ions are separated by curvature of their path (depends on m/q).
- **Fusion Reactors (Tokamaks)**: Magnetic fields confine hot plasma using helical motion.
- **Auroras**: Charged solar particles spiral along Earth's magnetic field.

Electric fields (\(\vec{E}\)) add linear acceleration, while magnetic fields (\(\vec{B}\)) bend paths into spirals or circles.

---

## Simulation of Particle Motion

We simulate using the **Lorentz force law** and integrate using **Euler's method**.

### Scenarios:

1. Only \(\vec{B}\): Circular or helical motion
2. \(\vec{E}\) and \(\vec{B}\): Complex curves or drifts
3. Crossed \(\vec{E} \perp \vec{B}\): E×B drift

---

## Python Simulation Code

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.0     # Charge (C)
m = 1.0     # Mass (kg)
dt = 0.01   # Time step
steps = 5000

# Fields
E = np.array([0.0, 0.0, 0.0])    # Electric field
B = np.array([0.0, 0.0, 1.0])    # Magnetic field (along z)

# Initial conditions
v = np.array([1.0, 0.0, 0.0])    # Initial velocity
r = np.array([0.0, 0.0, 0.0])    # Initial position

# Lists to store trajectory
trajectory = [r.copy()]

# Euler integration loop
for _ in range(steps):
    F = q * (E + np.cross(v, B))         # Lorentz force
    a = F / m                            # Acceleration
    v = v + a * dt                       # Update velocity
    r = r + v * dt                       # Update position
    trajectory.append(r.copy())

# Convert to array
trajectory = np.array(trajectory)

# Plotting
fig = plt.figure(figsize=(10, 6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(trajectory[:,0], trajectory[:,1], trajectory[:,2], label='Particle Path')
ax.set_title('Charged Particle Trajectory (Lorentz Force)')
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('z')
ax.legend()
plt.tight_layout()
plt.show()
```
