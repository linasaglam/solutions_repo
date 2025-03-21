# Problem 1
## Gravity: Orbital Period and Orbital Radius

### Kepler's Third Law

Kepler’s Third Law states that the square of the orbital period $T^2$ is proportional to the cube of the orbital radius $r^3$:

$$
T^2 \propto r^3 
$$

This relationship can be derived from Newton's law of gravitation and circular motion dynamics. 

Using Newton’s law of universal gravitation:
$$
F = \frac{G M m}{r^2} 
$$

For circular orbits, the centripetal force required to keep a body in orbit is:
$$
 F = \frac{m v^2}{r} 
$$

Equating the gravitational force to the centripetal force:
$$
 \frac{G M m}{r^2} = \frac{m v^2}{r} 
$$

Since the orbital velocity $ v $ is related to the orbital period $ T $ by:
$$
 v = \frac{2 \pi r}{T} 
$$

Substituting $ v $ into the equation:
$$
 \frac{G M m}{r^2} = \frac{m (2 \pi r)^2}{T^2 r} 
$$

Simplifying:
$$
 T^2 = \frac{4 \pi^2}{G M} r^3 
$$

This confirms Kepler's Third Law: $ T^2 \propto r^3 $.

### Python Simulation


import numpy as np
import matplotlib.pyplot as plt
from scipy.constants import G

# Constants
M = 5.972e24  # Mass of Earth (kg)
R_Earth = 6.371e6  # Radius of Earth (m)

# Define function to compute orbital period
def orbital_period(radius, mass=M):
    return 2 * np.pi * np.sqrt(radius**3 / (G * mass))

# Generate orbital radii
radii = np.linspace(R_Earth + 200e3, R_Earth + 1e7, 100)  # 200 km to 10000 km above Earth
periods = orbital_period(radii)

# Plot T^2 vs. r^3
plt.figure(figsize=(8, 6))
plt.plot(radii**3, periods**2, label="$T^2 \propto r^3$", color='b')
plt.xlabel("Orbital Radius Cubed (m^3)")
plt.ylabel("Orbital Period Squared (s^2)")
plt.title("Verification of Kepler's Third Law")
plt.legend()
plt.grid()
plt.show()

### Implications and Applications
- Kepler’s Third Law allows astronomers to determine planetary masses and distances.
- It applies to satellites, exoplanets, and even galaxies, aiding in the measurement of cosmic scales.
- The law extends to elliptical orbits with semi-major axis replacing the circular radius.

### Conclusion
The relationship $T^2 \propto r^3$ is fundamental in celestial mechanics. Our simulation verifies this principle, confirming its role in planetary motion and satellite dynamics.
