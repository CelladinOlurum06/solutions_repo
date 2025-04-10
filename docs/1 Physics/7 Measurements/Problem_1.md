# Problem 1
# Measuring Earth's Gravitational Acceleration Using a Pendulum

## Motivation

The acceleration due to gravity $$g$$ is a cornerstone of physics. A **simple pendulum** allows us to estimate $$g$$ experimentally by analyzing the time it takes to complete oscillations.

This experiment emphasizes:
- Accurate measurement techniques
- Uncertainty analysis
- Comparing experimental results with accepted values

---

## Materials

- String: 1.0–1.5 m long  
- Weight: key, coins, sugar, etc.  
- Stopwatch or smartphone  
- Measuring tape or ruler (with known resolution)

---

## Experimental Setup

- Attach weight to the string and suspend from a stable point.
- Measure total length $$L$$ from the suspension point to the **center of mass** of the weight.
- Let the pendulum swing with an angle <15°.
- Measure time $$T_{10}$$ for **10 full oscillations**, **repeat 10 times**.
- Record all values and compute uncertainties.

---

## Data Table

| Trial | $$T_{10}$$ (s) | $$T$$ (s) = $$\frac{T_{10}}{10}$$ |
|-------|----------------|----------------------------------|
| 1     |                |                                  |
| 2     |                |                                  |
| 3     |                |                                  |
| 4     |                |                                  |
| 5     |                |                                  |
| 6     |                |                                  |
| 7     |                |                                  |
| 8     |                |                                  |
| 9     |                |                                  |
| 10    |                |                                  |

### Summary Statistics

-import numpy as np
``markdown
# Ölçülen 10 salınım süreleri (örnek değerler)
T_10_list = [12.3, 12.5, 12.4, 12.6, 12.3]  # Buraya kendi verilerini gir

# Hesaplamalar
n = len(T_10_list)
T_10_bar = np.mean(T_10_list)
T_bar = T_10_bar / 10
sigma = np.std(T_10_list, ddof=1)
delta_T_10 = sigma / np.sqrt(n)
delta_T = delta_T_10 / 10

# Markdown (LaTeX $$ $$ formatında) çıktısı
print("### Ölçüm Sonuçları (LaTeX Formatında)\n")

print(f"$$\\bar{{T}}_{{10}} = {T_10_bar:.4f}\\ \\text{{s}}$$")
print(f"$$\\bar{{T}} = \\frac{{\\bar{{T}}_{{10}}}}{{10}} = {T_bar:.4f}\\ \\text{{s}}$$")
print(f"$$\\sigma = {sigma:.4f}\\ \\text{{s}}$$")
print(f"$$\\delta \\bar{{T}}_{{10}} = \\frac{{\\sigma}}{{\\sqrt{{n}}}} = {delta_T_10:.4f}\\ \\text{{s}}$$")
print(f"$$\\delta \\bar{{T}} = \\frac{{\\delta \\bar{{T}}_{{10}}}}{{10}} = {delta_T:.4f}\\ \\text{{s}}$$")
```
---

## Calculations

### 1. Gravitational Acceleration

Using the simple pendulum equation:

$$
T = 2\pi \sqrt{\frac{L}{g}} \Rightarrow g = \frac{4\pi^2 L}{T^2}
$$

### 2. Propagation of Uncertainty

Let:
- $$\delta L$$: uncertainty in length (typically half the ruler resolution)
- $$\delta T$$: uncertainty in mean period

Then:
$$
\delta g = g \cdot \sqrt{ \left( \frac{\delta L}{L} \right)^2 + \left( 2 \cdot \frac{\delta T}{T} \right)^2 }
$$

---

##  Python Code for Calculation

```python
import numpy as np

# --- Input your data here ---
T10 = np.array([  # Time for 10 oscillations, in seconds
    20.1, 19.9, 20.0, 20.2, 20.0,
    20.1, 20.0, 20.1, 19.8, 20.2
])

L = 1.000  # Pendulum length in meters
delta_L = 0.005  # Uncertainty in L (e.g., half the resolution of a 1 cm tape)

# --- Calculations ---
T_single = T10 / 10
T_mean = np.mean(T_single)
sigma = np.std(T10, ddof=1)
delta_T10 = sigma / np.sqrt(len(T10))
delta_T = delta_T10 / 10

# Gravity calculation
g = 4 * np.pi**2 * L / T_mean**2

# Uncertainty in g
delta_g = g * np.sqrt((delta_L / L)**2 + (2 * delta_T / T_mean)**2)

# Output
print(f"Mean T = {T_mean:.4f} s")
print(f"g = {g:.4f} m/s² ± {delta_g:.4f}")
```
