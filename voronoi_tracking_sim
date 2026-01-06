import numpy as np
import matplotlib.pyplot as plt
from scipy.spatial import Voronoi, voronoi_plot_2d
import matplotlib.animation as animation
from matplotlib.path import Path

# Step 1: Define the dimensions of the square and generate 15 random points (drones)
square_size = 10
num_points = 15
drone_positions = np.random.rand(num_points, 2) * square_size

# Step 2: Compute the Voronoi diagram
vor = Voronoi(drone_positions)

# Step 3: Initialize the moving target (red point)
target_position = np.random.rand(2) * square_size  # Random initial position within the square
tracking_drone_index = None  # Initialize tracking drone index

# Step 4: Set up the plot
fig, ax = plt.subplots(figsize=(8, 8))

# Plot the Voronoi diagram
voronoi_plot_2d(vor, ax=ax, show_vertices=False, line_colors='black', line_width=1)

# Customize the plot
ax.set_xlim(0, square_size)
ax.set_ylim(0, square_size)
ax.set_aspect('equal')
ax.set_title('Voronoi Diagram with Moving Target and Tracking Drone')

# Plot the drones (blue points)
drones, = ax.plot(drone_positions[:, 0], drone_positions[:, 1], 'bo', label='Drones')

# Initialize the red moving target
target, = ax.plot([target_position[0]], [target_position[1]], 'ro', label='Moving Target', markersize=8)

# Add legend
ax.legend()

# Step 5: Define a function to handle mouse clicks
def on_click(event):
    global target_position
    if event.inaxes is not None:  # Ensure the click is within the plot's axes
        target_position = np.array([event.xdata, event.ydata])  # Set the target's position
        target.set_data([target_position[0]], [target_position[1]])  # Update the target position on the plot
        fig.canvas.draw()  # Redraw the plot

# Connect the on_click function to mouse clicks
fig.canvas.mpl_connect('button_press_event', on_click)

# Step 6: Define the update function for animation
def update(frame):
    global drone_positions, tracking_drone_index
    
    # Move the target randomly within the square (after click, it continues to move randomly)
    step_size = 0.5
    target_position[0] += (np.random.rand() - 0.5) * step_size
    target_position[1] += (np.random.rand() - 0.5) * step_size
    
    # Ensure the target stays within the bounds of the square
    target_position[0] = np.clip(target_position[0], 0, square_size)
    target_position[1] = np.clip(target_position[1], 0, square_size)
    
    # Update the position of the target
    target.set_data([target_position[0]], [target_position[1]])

    # Step 7: Identify which drone's Voronoi cell contains the target
    for i, region_index in enumerate(vor.point_region):
        vertices = [vor.vertices[v] for v in vor.regions[region_index] if v >= 0]
        if vertices:
            cell_path = Path(vertices)
            if cell_path.contains_point(target_position):
                tracking_drone_index = i
                break

    # Move each drone towards the target but keep it within its own Voronoi cell
    for i in range(num_points):
        # If this is the tracking drone, move it towards the target
        direction = target_position - drone_positions[i]
        distance_to_target = np.linalg.norm(direction)
        
        # Normalize the direction vector and scale it by a step size
        step_size = 0.1
        if distance_to_target < 0.2:  # Threshold for very close drones
            step = direction  # Move full step toward the target
        else:
            step = (direction / distance_to_target) * step_size  # Normalized movement direction

        # Calculate the proposed new position
        new_position = drone_positions[i] + step

        # Check if this drone is the tracking drone
        if i == tracking_drone_index:
            # If the tracking drone is within its cell, update it
            vertices = [vor.vertices[v] for v in vor.regions[vor.point_region[i]] if v >= 0]
            if vertices:
                cell_path = Path(vertices)
                if cell_path.contains_point(new_position):
                    drone_positions[i] = new_position  # Update tracking drone's position
                else:
                    # If the new position is out of bounds, move it within the cell
                    # Try a smaller step to avoid boundary violation
                    small_step = step * 0.5
                    small_position = drone_positions[i] + small_step
                    if cell_path.contains_point(small_position):
                        drone_positions[i] = small_position
        else:
            # For other drones (boundary or not), try to move them towards the target
            vertices = [vor.vertices[v] for v in vor.regions[vor.point_region[i]] if v >= 0]
            if vertices:
                cell_path = Path(vertices)
                # If the calculated step leads out of the cell, scale the movement
                if cell_path.contains_point(new_position):
                    drone_positions[i] = new_position
                else:
                    # If out of bounds, try to take a smaller step
                    small_step = step * 0.5
                    small_position = drone_positions[i] + small_step
                    if cell_path.contains_point(small_position):
                        drone_positions[i] = small_position

    # Update drone positions on the plot
    drones.set_data(drone_positions[:, 0], drone_positions[:, 1])

    return target, drones

# Step 8: Animate the movement
ani = animation.FuncAnimation(fig, update, frames=200, interval=100, blit=True)

plt.show()
