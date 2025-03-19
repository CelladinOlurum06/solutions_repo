# Problem 1
# Investigating the Range as a Function of the Angle of Projection

## 1. Theoretical Foundation

### Governing Equations of Projectile Motion

Projectile motion follows Newton's laws under constant acceleration due to gravity. The basic equations for a projectile launched with an initial velocity \( v_0 \) at an angle \( \theta \) from the horizontal are:

#### **Equations of Motion**
- **Horizontal motion** (constant velocity):

  $$
  x(t) = v_0 \cos(\theta) t
  $$

- **Vertical motion** (accelerated motion under gravity):

  $$
  y(t) = v_0 \sin(\theta) t - \frac{1}{2} g t^2
  $$

#### **Time of Flight**
The total time of flight can be found by setting \( y(t) = 0 \) (when the projectile returns to the ground):

  $$
  t_f = \frac{2 v_0 \sin(\theta)}{g}
  $$

#### **Range of the Projectile**
The horizontal range is given by:

  $$
  R = v_0 \cos(\theta) \cdot t_f
  $$

Substituting \( t_f \):

  $$
  R = \frac{v_0^2 \sin(2\theta)}{g}
  $$

This equation shows that the range depends on both the initial velocity and the launch angle.

## 2. Analysis of the Range

- The maximum range occurs when \( \sin(2\theta) = 1 \), i.e., at \( \theta = 45^\circ \).
- Increasing \( v_0 \) increases the range quadratically.
- Increasing \( g \) (e.g., on planets with stronger gravity) decreases the range.

## 3. Practical Applications

- **Sports**: Optimization of throwing angles in javelin, shot put, and soccer.
- **Engineering**: Ballistics and missile trajectory predictions.
- **Astrophysics**: Calculations for planetary landings, where gravity varies.

## 4. Implementation in Python

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # gravitational acceleration (m/s^2)
v0 = 20   # initial velocity (m/s)
angles = np.linspace(0, 90, 100)  # angles from 0 to 90 degrees

# Compute range for each angle
ranges = (v0**2 * np.sin(2 * np.radians(angles))) / g

# Find the angle with the maximum range
optimal_angle = angles[np.argmax(ranges)]
max_range = max(ranges)

# Plot
plt.figure(figsize=(8, 5))
plt.plot(angles, ranges, label="Projectile Range")
plt.axvline(x=optimal_angle, color='r', linestyle="--", label=f"Max Range at {optimal_angle:.1f}°")
plt.xlabel("Angle of Projection (degrees)")
plt.ylabel("Range (m)")
plt.title("Projectile Range vs. Angle of Projection")
plt.legend()
plt.grid()
plt.show()

print(f"Maximum range of {max_range:.2f} meters occurs at {optimal_angle:.1f} degrees.")
