# Problem 1
# Interference Patterns on a Water Surface

## Motivation

Interference occurs when waves from different sources overlap, creating new patterns. On a water surface, this can be observed when circular ripples from different points meet, forming regions of amplification (constructive interference) and cancellation (destructive interference).

Understanding such patterns deepens our grasp of wave behavior, coherence, and phase relationships. In this study, we place point sources at the vertices of a regular polygon to explore interference using wave superposition.

---

## Problem Setup

We simulate wave interference from **5 coherent point sources** placed at the vertices of a **regular pentagon**. Each source emits circular waves with the same amplitude, frequency, and wavelength.

### Wave Equation

A circular wave from a point source at \((x_i, y_i)\) is:

\[
\psi_i(x, y, t) = A \cdot \cos(k r_i - \omega t)
\]

Where:
- \( A \): amplitude
- \( k = \frac{2\pi}{\lambda} \): wave number
- \( \omega = 2\pi f \): angular frequency
- \( r_i = \sqrt{(x - x_i)^2 + (y - y_i)^2} \): distance from source \(i\)

The total wave displacement is:

\[
\Psi(x, y, t) = \sum_{i=1}^{N} \psi_i(x, y, t)
\]

---

## Assumptions

- Amplitude \(A = 1.0\)
- Wavelength \(\lambda = 1.0\)
- Frequency \(f = 1.0\)
- All waves are coherent (same phase)
- Regular pentagon centered at the origin

---

## Python Simulation Code

```python
import numpy as np
import matplotlib.pyplot as plt

# Simulation parameters
A = 1.0                      # Amplitude
wavelength = 1.0             # Wavelength
frequency = 1.0              # Frequency
k = 2 * np.pi / wavelength   # Wave number
omega = 2 * np.pi * frequency
t = 0                        # Time (snapshot)

# Polygon settings
N = 5  # Number of sources (regular pentagon)
radius = 3.0  # Distance from center to each vertex

# Generate source positions (vertices of regular polygon)
angles = np.linspace(0, 2 * np.pi, N, endpoint=False)
source_positions = [(radius * np.cos(a), radius * np.sin(a)) for a in angles]

# Grid for simulation
x = np.linspace(-10, 10, 500)
y = np.linspace(-10, 10, 500)
X, Y = np.meshgrid(x, y)

# Calculate total wave displacement
Psi = np.zeros_like(X)

for xi, yi in source_positions:
    r = np.sqrt((X - xi)**2 + (Y - yi)**2)
    Psi += A * np.cos(k * r - omega * t)

# Plotting the interference pattern
plt.figure(figsize=(10, 8))
plt.contourf(X, Y, Psi, levels=100, cmap='viridis')
plt.colorbar(label='Wave Displacement')
plt.scatter(*zip(*source_positions), color='red', label='Wave Sources')
plt.title("Interference Pattern from 5 Point Sources (Pentagon)")
plt.xlabel("x")
plt.ylabel("y")
plt.legend()
plt.axis("equal")
plt.grid(True)
plt.show()
```
