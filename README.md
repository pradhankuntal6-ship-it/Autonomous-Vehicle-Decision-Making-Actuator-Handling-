# Simplified Autonomous Vehicle Decision Module

This MATLAB project implements **Module 2, Project 4** from the assignment: a basic autonomous vehicle decision module that chooses when to cruise, yield, stop, and turn, then simulates the corresponding throttle, brake, and steering commands.

This is the simplest project in the assignment to build and demonstrate in MATLAB because it uses a small finite-state machine and a lightweight vehicle model. It does not require ROS, Carla, Simulink, external datasets, or add-on toolboxes.

## What it demonstrates

- A pedestrian crossing event that triggers a yield response.
- A stop sign that triggers braking, a full stop, and a 2.5-second dwell.
- A right turn after the stop, followed by a return to cruise.
- Throttle, brake, and steering commands mapped from each decision state.
- A simple bicycle-model path and plots of speed, state, and actuator commands.

## Run it

1. Open `av_decision_module.m` in MATLAB.
2. Select **Run** or enter `av_decision_module` in the Command Window.
3. Read the plain-language summary in the Command Window and the one-page route/timeline figure.

The script uses only base MATLAB functions. The main scenario settings (road event locations, pedestrian timing, speed, and dwell duration) are near the top of the script and can be edited to explore other cases.

## Decision logic

The finite-state machine uses four states:

| State | Behavior | Actuator response |
| --- | --- | --- |
| CRUISE | Drive toward the target speed | Apply throttle as needed |
| YIELD | Slow or stop for the active pedestrian crossing | Apply service braking |
| STOP | Stop at the stop sign and wait | Apply full braking |
| TURN | Complete a right turn after the stop | Apply reduced target speed and steering |

The pedestrian yield check has priority. Once the vehicle comes to a stop at the sign, it waits for the configured dwell time, turns, then returns to cruise.

## Model scope

The vehicle motion is intentionally simplified. Longitudinal acceleration is calculated from throttle and brake commands. A kinematic bicycle model updates position and heading from speed, wheelbase, and steering angle. Road objects are represented as scenario event locations and time windows rather than camera or lidar detections. The output focuses on a labeled route map and a color-coded timeline, with the main actions also printed in everyday language.

This is an educational simulation for demonstrating decision logic and actuator mapping. It is not a validated autonomous-driving controller and must not be used to control a real vehicle.

## Files

- `av_decision_module.m` - complete MATLAB simulation and visualization.
- `README.md` - project overview and run instructions.

## Possible extensions

- Add traffic-light states, speed limits, and more pedestrian scenarios.
- Add hysteresis or sensor uncertainty to prevent rapid state switching.
- Replace scenario flags with detections from a perception model.
- Implement the same state machine in Simulink and compare responses.
