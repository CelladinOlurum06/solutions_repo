# Problem 2
# Investigating the Dynamics of a Forced Damped Pendulum

## 1. Theoretical Foundation

### Governing Equation
The motion of a forced damped pendulum is governed by the differential equation:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \sin(\theta) = A \cos(\omega_d t)
$$

where:
- \( \theta \) is the angular displacement,
- \( b \) is the damping coefficient,
- \( g \) is gravitational acceleration,
- \( L \) is the length of the pendulum,
- \( A \) is the amplitude of the external forcing,
- \( \omega_d \) is the driving frequency.

For small angles, we approximate \( \sin(\theta) \approx \theta \), leading to a linearized form:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(\omega_d t)
$$

### Resonance and Energy Considerations
- Resonance occurs when the driving frequency matches the system's natural frequency:
  
  $$
  \omega_0 = \sqrt{\frac{g}{L}}
  $$

- The energy in the system fluctuates due to damping and external forcing, leading to phenomena such as periodic, quasiperiodic, and chaotic motion.

## 2. Implementation in Python

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
g = 9.81  # gravitational acceleration (m/s^2)
L = 1.0  # length of pendulum (m)
b = 0.2  # damping coefficient
A = 1.2  # driving amplitude
omega_d = 2.0  # driving frequency

# Differential equation for the forced damped pendulum
def forced_damped_pendulum(t, y, b, A, omega_d):
    theta, omega = y
    dydt = [
        omega,
        -b * omega - (g / L) * np.sin(theta) + A * np.cos(