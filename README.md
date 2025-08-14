# F1TENTH Autonomous Vehicle Projects

This repository integrates four main modules related to F1TENTH autonomous vehicle research: Map Controller Extension, Static Obstacle Avoidance, Opponent Detection & Tracking, and Global Trajectory Planning.

---

## 1. Map Controller Extension
- Based on the `map_control` module from the ForzaETH repository.  
- Extends functionality through `map_controller_obs.py`:
  - When static obstacles are detected, switches to a locally generated path using a spline-based planner for safe avoidance.
- Provides lane visualization via `lane_visualize.py`.
- Supports RViz visualization and sensor TF broadcasting for accurate data alignment.

---

## 2. Static Obstacle Avoidance
- Implements a planner using the **Frenet coordinate system** and **spline interpolation**.  
- Computes trajectories around static obstacles in the F1TENTH simulator and real vehicles.  
- Core modules:
  - `frenet_utils.py`: Converts between Cartesian and Frenet coordinates, builds smooth centerlines using cubic splines.  
  - `static_obs_spline_planner.py`: Subscribes to global path and obstacle topics, computes avoidance paths, publishes waypoints and markers.

---

## 3. Opponent Detection & Tracking
- Detects and tracks obstacles (static and dynamic) on the racetrack.  
- Components:
  - **Opponent Detection**: Segments LiDAR scans, filters objects, applies rectangle fitting for feature extraction.  
  - **Opponent Tracking**: Associates detections, classifies obstacles as static or dynamic, predicts trajectories using averaging (static) or Kalman Filter (dynamic).  
- Dynamic parameters configurable at runtime, including obstacle size, TTL, association distance, and debug modes.  
- Works in head-to-head mode for accurate opponent behavior monitoring.

---

## 4. Global Trajectory Planning
- Determines optimal racing lines for autonomous race cars with multiple objectives:
  - Shortest path
  - Minimum curvature
  - Minimum time
  - Minimum time with powertrain behavior consideration
- Components:
  - `frictionmap`: Handles creation and management of friction maps.  
  - `helper_funcs_glob`: Provides helper functions for trajectory computations.  
  - `inputs`: Stores vehicle dynamics, reference tracks, and friction maps.  
  - `opt_mintime_traj`: Computes minimum-time trajectories considering powertrain losses and thermal behavior.  
  - `params`: Contains parameter files for trajectory optimization and vehicle configurations.
- Supports two trajectory formats:
  - **Race Trajectory**: Detailed global trajectory including positions, headings, curvatures, velocities, and accelerations.  
  - **LTPL Trajectory**: Includes source trajectory data and track bounds for use in local planners.

---

