# Problem 2
## Escape Velocities and Cosmic Velocities

### Introduction

The concept of escape velocity is fundamental in space science, defining the minimum speed needed for an object to break free from a celestial body's gravitational pull. Additionally, the first, second, and third cosmic velocities describe different motion regimes crucial for satellite deployment, interplanetary travel, and interstellar exploration.

### Definitions

1. **First Cosmic Velocity (Orbital Velocity)**
   - The minimum velocity required to maintain a stable circular orbit around a celestial body.
   - Given by:
   
   $$
      v_1 = \sqrt{\frac{G M}{r}} 
$$

2. **Second Cosmic Velocity (Escape Velocity)**
   - The velocity needed to completely escape a celestial body's gravitational field.
   - Derived from energy conservation:
   
   $$
      v_2 = \sqrt{2} v_1 = \sqrt{\frac{2 G M}{r}} 
   $$

3. **Third Cosmic Velocity (Solar System Escape Velocity)**
   - The velocity required to escape the Sun’s gravitational influence from a planet.
   - Given by:

   $$
      v_3 = \sqrt{v_2^2 + v_{esc,sun}^2} 
   $$

### Python Simulation


import numpy as np
import matplotlib.pyplot as plt
from scipy.constants import G

# Constants for celestial bodies (mass in kg, radius in m)

$$
bodies = {
    "Earth": (5.972e24, 6.371e6),
    "Mars": (6.417e23, 3.389e6),
    "Jupiter": (1.898e27, 6.9911e7)
}
$$
# Function to compute velocities

def cosmic_velocities(mass, radius):
    v1 = np.sqrt(G * mass / radius)  # Orbital velocity
    v2 = np.sqrt(2) * v1  # Escape velocity
    return v1, v2


# Compute velocities

$$
velocities = {body: cosmic_velocities(m, r) for body, (m, r) in bodies.items()}
$$

# Plot results

$$
labels = list(velocities.keys())
vel1 = [velocities[b][0] for b in labels]
vel2 = [velocities[b][1] for b in labels]
$$

x = np.arange(len(labels))
width = 0.4

plt.figure(figsize=(8, 6))
plt.bar(x - width/2, vel1, width, label="Orbital Velocity (m/s)", color='b')
plt.bar(x + width/2, vel2, width, label="Escape Velocity (m/s)", color='r')
plt.xlabel("Celestial Body")
plt.ylabel("Velocity (m/s)")
plt.xticks(x, labels)
plt.title("Cosmic Velocities for Different Celestial Bodies")
plt.legend()
plt.grid()
plt.show()


### Importance in Space Exploration
- The first cosmic velocity defines satellite launch speeds.
- The second cosmic velocity determines interplanetary mission requirements.
- The third cosmic velocity is crucial for interstellar travel considerations.

### Conclusion
Understanding cosmic velocities is essential for space missions, satellite technology, and future interplanetary and interstellar exploration. The provided simulation visualizes these velocities for key celestial bodies, demonstrating their role in space science and engineering.
