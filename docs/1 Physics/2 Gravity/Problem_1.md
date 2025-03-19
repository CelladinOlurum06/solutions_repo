# Problem 1
# Orbital Period and Orbital Radius

## 1. Theoretical Foundation

### Kepler’s Third Law

Kepler’s Third Law states that for a body orbiting another in a circular orbit, the square of the orbital period \( T \) is proportional to the cube of the orbital radius \( R \):

$$
T^2 = rac{4\pi^2 R^3}{GM}
$$

where:
- \( T \) is the orbital period,
- \( R \) is the orbital radius,
- \( G \) is the gravitational constant,
- \( M \) is the mass of the central body.

Rearranging for \( T \):

$$
T = 2\pi \sqrt{\frac{R^3}{GM}}
$$

This equation shows that the orbital period increases with the radius.

## 2. Real-World Implications

- **Determining planetary masses:** By measuring the period and radius of a moon orbiting a planet, the mass of the planet can be calculated.
- **Satellite Orbits:** Engineers use Kepler’s laws to design stable orbits for communication and GPS satellites.
- **Exoplanet Discovery:** Astronomers use Kepler’s Third Law to estimate the distance and mass of exoplanets by analyzing their orbital periods.

## 3. Implementation in Python

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # Gravitational constant (m^3/kg/s^2)
M = 5.972e24  # Mass of Earth (kg)
R_values = np.linspace(7e6, 4e8, 100)  # Orbital radii from 7,000 km to 400,000 km

# Calculate orbital periods
T_values = 2 * np.pi * np.sqrt(R_values**3 / (G * M))

# Plot T^2 vs R^3
plt.figure(figsize=(8, 5))
plt.plot(R_values**3, T_values**2, label='$T^2 \propto R^3$', color='b')
plt.xlabel('$R^3$ (m^3)')
plt.ylabel('$T^2$ (s^2)')
plt.title('Kepler’s Third Law: $T^2$ vs $R^3$')
plt.legend()
plt.grid()
plt.show()
```

## 4. Discussion on Extensions

- **Elliptical Orbits:** While this derivation assumes circular orbits, Kepler’s Third Law extends to elliptical orbits by using the semi-major axis instead of \( R \).
- **Gravitational Interactions:** Multi-body systems introduce perturbations that modify orbital periods slightly.
- **Relativistic Effects:** At very high masses or velocities, general relativity modifies the gravitational interactions beyond Newtonian predictions.

## 5. Conclusion

This analysis confirms Kepler’s Third Law through theoretical derivation and computational modeling. The relationship between \( T^2 \) and \( R^3 \) is essential in astronomy, satellite mechanics, and astrophysics, providing a fundamental link between motion and gravity.
