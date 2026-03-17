# Arduino Line Following Robot

This project implements an autonomous line-following robot using an Arduino microcontroller and a 5-channel IR sensor array. The robot detects the position of a line and adjusts motor speeds in real time to maintain alignment with the path.

---

## Components Used

- Arduino Nano / Uno  
- IR Sensor Array (5 sensors)  
- L298N Motor Driver  
- DC Motors  
- Robot Chassis with Wheels  
- Battery Pack  

---

## Working Principle

The IR sensor array detects the contrast between the line and the surface. Each sensor outputs a digital signal indicating the presence of the line beneath it.

The Arduino continuously reads these inputs and applies rule-based logic to control the motors:

- When the center sensor detects the line, the robot moves straight  
- When the line shifts to the left sensors, the robot turns left  
- When the line shifts to the right sensors, the robot turns right  
- If no sensors detect the line, the robot stops (line lost condition)  

Motor speed and direction are controlled using PWM signals through the L298N motor driver.

---

## Features

- Autonomous line tracking  
- Real-time sensor-based decision making  
- Differential motor speed control  
- Simple and efficient rule-based navigation  

---

## Limitations

- No PID control (movement is not smooth at higher speeds)  
- Performance drops on sharp curves or noisy surfaces  
- No line recovery mechanism when the path is lost  

---

## Future Improvements

- Implement PID control for smooth and stable tracking  
- Add adaptive speed control based on curvature  
- Integrate line recovery algorithm  
- Add obstacle detection using ultrasonic sensors  

---
