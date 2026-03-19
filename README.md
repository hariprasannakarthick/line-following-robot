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

## Circuit Diagram
<img width="1536" height="1024" alt="ChatGPT Image Mar 19, 2026, 04_14_44 PM" src="https://github.com/user-attachments/assets/fdac8501-c2c1-4692-818c-da162ad56fcc" />

## Code
```cpp
// Sensor Pins
#define S1 2
#define S2 3
#define S3 4
#define S4 5
#define S5 6

// Motor Driver Pins
#define ENA 9
#define IN1 8
#define IN2 7
#define ENB 10
#define IN3 12
#define IN4 11

int baseSpeed = 150;
int turnSpeed = 200;

void setup() {
  pinMode(S1, INPUT);
  pinMode(S2, INPUT);
  pinMode(S3, INPUT);
  pinMode(S4, INPUT);
  pinMode(S5, INPUT);

  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(ENB, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);

  Serial.begin(9600);
}

// Motor Functions
void forward(int speedA, int speedB) {
  analogWrite(ENA, speedA);
  analogWrite(ENB, speedB);

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void leftTurn() {
  analogWrite(ENA, 100);
  analogWrite(ENB, turnSpeed);

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);

  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void rightTurn() {
  analogWrite(ENA, turnSpeed);
  analogWrite(ENB, 100);

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}

void stopBot() {
  analogWrite(ENA, 0);
  analogWrite(ENB, 0);
}

void loop() {
  int s1 = digitalRead(S1);
  int s2 = digitalRead(S2);
  int s3 = digitalRead(S3);
  int s4 = digitalRead(S4);
  int s5 = digitalRead(S5);

  Serial.print(s1); Serial.print(" ");
  Serial.print(s2); Serial.print(" ");
  Serial.print(s3); Serial.print(" ");
  Serial.print(s4); Serial.print(" ");
  Serial.println(s5);

  // LINE DETECTION LOGIC
  if (s3 == 1 && s2 == 0 && s4 == 0) {
    // Center on line → straight
    forward(baseSpeed, baseSpeed);
  }
  else if (s1 == 1 || s2 == 1) {
    // Line on left
    leftTurn();
  }
  else if (s4 == 1 || s5 == 1) {
    // Line on right
    rightTurn();
  }
  else {
    // Lost line
    stopBot();
  }
}
