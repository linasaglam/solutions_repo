# Problem 2
# Estimating $ \pi $ Using Monte Carlo Methods

## Motivation:
Monte Carlo simulations are a powerful class of computational techniques that use randomness to solve problems or estimate values. One of the most elegant applications of Monte Carlo methods is estimating the value of $ \pi $ through geometric probability. By randomly generating points and analyzing their positions relative to a geometric shape, we can approximate $ \pi $ in an intuitive and visually engaging way.

This problem connects fundamental concepts of probability, geometry, and numerical computation. It also provides a gateway to understanding how randomness can be harnessed to solve complex problems in physics, finance, and computer science. The Monte Carlo approach to $ \pi $ estimation highlights the versatility and simplicity of this method while offering practical insights into convergence rates and computational efficiency.

## Part 1: Estimating $ \pi $ Using a Circle

### 1. Theoretical Foundation:

The process for estimating $ \pi $ involves a unit circle inscribed in a square. The side length of the square is 2, while the radius of the circle is 1. 

- The equation of the circle is:  
  $
  x^2 + y^2 \leq 1
  $
  This describes the points that lie within or on the boundary of the unit circle.

- The area of the square is:  
  $
  \text{Area of Square} = 2 \times 2 = 4
  $

- The area of the unit circle is given by:  
  $
  \text{Area of Circle} = \pi \times 1^2 = \pi
  $

- The ratio of the area of the circle to the area of the square is:
  $
  \frac{\text{Area of Circle}}{\text{Area of Square}} = \frac{\pi}{4}
  $

- By generating random points within the square and checking how many fall inside the circle, we estimate $ \pi $. The ratio of points inside the circle to the total number of points is:
  $
  \frac{\text{Points Inside Circle}}{\text{Total Points}} \approx \frac{\pi}{4}
  $
  Therefore, we estimate $ \pi $ as:
  $
  \pi \approx 4 \times \frac{\text{Points Inside Circle}}{\text{Total Points}}
  $

### 2. Simulation:

We generate random points $ (x, y) $ within the square $[-1, 1] \times [-1, 1]$ and check if they satisfy the condition $ x^2 + y^2 \leq 1 $, meaning the point is inside the unit circle.

![alt text](image-1.png)

### 3. Python Code for Circle-Based Method:

```python
import numpy as np
import matplotlib.pyplot as plt

# Function to estimate π using Monte Carlo method based on circle
def estimate_pi_circle(n_points):
    # Generate random points (x, y) in the square [-1, 1] x [-1, 1]
    x = np.random.uniform(-1, 1, n_points)
    y = np.random.uniform(-1, 1, n_points)
    
    # Calculate the distance of each point from the origin (x^2 + y^2)
    distance_squared = x**2 + y**2
    
    # Count the points inside the unit circle (x^2 + y^2 <= 1)
    points_inside_circle = np.sum(distance_squared <= 1)
    
    # Estimate π using the ratio of points inside the circle
    # π = 4 * (points inside circle) / (total points)
    pi_estimate = 4 * points_inside_circle / n_points
    
    return pi_estimate, x, y, distance_squared <= 1

# Run the simulation for 10,000 points
n_points = 10000
pi_estimate, x, y, inside_circle = estimate_pi_circle(n_points)

# Visualize the points and the circle
plt.figure(figsize=(6,6))
plt.scatter(x[inside_circle], y[inside_circle], color='green', s=1, label='Inside Circle')
plt.scatter(x[~inside_circle], y[~inside_circle], color='red', s=1, label='Outside Circle')
plt.gca().set_aspect('equal', adjustable='box')
plt.title(f"Monte Carlo Estimation of $\\pi$\nEstimated $\\pi$: {pi_estimate:.4f}")
plt.xlabel('X')
plt.ylabel('Y')
plt.legend()
plt.grid(True)
plt.show()
```

# Function to simulate Buffon's Needle
def estimate_pi_buffon(needle_length, line_distance, n_drops):
    crosses = 0
    for _ in range(n_drops):
        # Randomly generate the distance from the needle's midpoint to the nearest line
        dist_to_line = np.random.uniform(0, line_distance / 2)
        
        # Randomly generate the angle of the needle (uniformly between 0 and π/2)
        angle = np.random.uniform(0, np.pi / 2)
        
        # Check if the needle crosses the line
        if dist_to_line <= (needle_length / 2) * np.sin(angle):
            crosses += 1
    
    # Estimate π using Buffon's Needle formula
    pi_estimate = (2 * needle_length * n_drops) / (line_distance * crosses)
    
    return pi_estimate

# Run the simulation for Buffon's Needle
needle_length = 1  # length of the needle (L)
line_distance = 2  # distance between parallel lines (D)
n_drops = 10000    # number of needle drops (N_drops)

# Estimate π using Buffon's Needle method
pi_estimate_buffon = estimate_pi_buffon(needle_length, line_distance, n_drops)
print(f"Estimated π using Buffon's Needle: {pi_estimate_buffon:.4f}")
