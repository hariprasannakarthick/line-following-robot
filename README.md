# Arduino Line Following Robot

This project implements an autonomous line-following robot using Arduino and an array of IR sensors. The robot detects a line on the ground and adjusts its movement to stay on the path.

## Components Used
- Arduino Nano / Uno
- IR Sensor Array (5 sensors)
- L298N Motor Driver
- DC Motors
- Chassis with wheels
- Battery pack

## Working Principle
The IR sensors detect the contrast between the line and the floor. The Arduino reads sensor values and decides the robot's movement:

- Move forward when the center sensor detects the line
- Turn left when right sensors lose the line
- Turn right when left sensors lose the line

## Features
- Autonomous navigation
- Real-time line detection
- Simple control logic

## Future Improvements
- PID control for smoother movement
- Speed optimization
- Obstacle detection
