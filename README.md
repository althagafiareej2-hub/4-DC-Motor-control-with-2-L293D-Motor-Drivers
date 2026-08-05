# 4 DC Motors Simulation Project

## Project Overview
This project is a simulation I designed to connect and program **4 DC Motors** using an Arduino Uno board and two L293D Motor Drivers. I set up the schematic circuit diagram in **Tinkercad**, and added my own custom programming code to achieve the required sequential motor movements precisely.

---

##  Work Details & Modifications:
* **Circuit Diagram:** I prepared and wired the complete hardware schematic in Tinkercad, connecting the Arduino, battery, L293D chips, and all four motors in a clean and organized way.
* **Programming Code:** I wrote and modified the code to map correctly with the pins used in the schematic, ensuring it performs the required movements for the specified durations.

---

## Programmed Motion Sequence:
1. **Forward:** All four motors move forward for **30 seconds**.
2. **Backward:** The motors reverse their direction and move backward for **1 full minute (60 seconds)**.
3. **Right & Left Alternately:** The motors simulate turning (by alternating the rotation direction of opposite sides) for **1 full minute**.

---

## Code Explanation

I wrote the following code to handle the movement sequence, motor control, and timing delays:

```cpp
// Define connection pins for Motors A, B, C, D (PWM speed and direction pins)
int enA = 9; int in1 = 8; int in2 = 7; // Motor A connections
int enB = 3; int in3 = 5; int in4 = 4; // Motor B connections
int enC = 10; int in5 = 13; int in6 = 12;// Motor C connections
int enD = 11; int in7 = 2; int in8 = 6; // Motor D connections

void setup() {
  // Set all motor control and driver pins as Outputs
  pinMode(enA, OUTPUT); pinMode(enB, OUTPUT);
  pinMode(enC, OUTPUT); pinMode(enD, OUTPUT);
  pinMode(in1, OUTPUT); pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT); pinMode(in4, OUTPUT);
  pinMode(in5, OUTPUT); pinMode(in6, OUTPUT);
  pinMode(in7, OUTPUT); pinMode(in8, OUTPUT);
  
  stopMotors(); // Initialize motors in a stopped state for safety
}

void loop() {
  // Set maximum speed for all motors (value 255)
  analogWrite(enA, 255); analogWrite(enB, 255);
  analogWrite(enC, 255); analogWrite(enD, 255);

  // 1. Move Forward for 30 seconds
  moveForward();
  delay(30000); 

  // 2. Move Backward for 60 seconds (1 minute)
  moveBackward();
  delay(60000); 

  // 3. Turn Right and Left alternately for 1 minute (switching every 2 seconds)
  for(int i = 0; i < 15; i++) {
    turnRight();
    delay(2000); 
    turnLeft();
    delay(2000); 
  }

  // Stop all motors permanently after the sequence completes
  stopMotors();
  while(true); 
}

// --- Movement Functions ---
void moveForward() {
  digitalWrite(in1, HIGH); digitalWrite(in2, LOW);
  digitalWrite(in3, HIGH); digitalWrite(in4, LOW);
  digitalWrite(in5, HIGH); digitalWrite(in6, LOW);
  digitalWrite(in7, HIGH); digitalWrite(in8, LOW);
}

void moveBackward() {
  digitalWrite(in1, LOW);  digitalWrite(in2, HIGH);
  digitalWrite(in3, LOW);  digitalWrite(in4, HIGH);
  digitalWrite(in5, LOW);  digitalWrite(in6, HIGH);
  digitalWrite(in7, LOW);  digitalWrite(in8, HIGH);
}

void turnRight() {
  digitalWrite(in1, HIGH); digitalWrite(in2, LOW);
  digitalWrite(in3, HIGH); digitalWrite(in4, LOW);
  digitalWrite(in5, LOW);  digitalWrite(in6, HIGH);
  digitalWrite(in7, LOW);  digitalWrite(in8, HIGH);
}

void turnLeft() {
  digitalWrite(in1, LOW);  digitalWrite(in2, HIGH);
  digitalWrite(in3, LOW);  digitalWrite(in4, HIGH);
  digitalWrite(in5, HIGH); digitalWrite(in6, LOW);
  digitalWrite(in7, HIGH); digitalWrite(in8, LOW);
}

void stopMotors() {
  digitalWrite(in1, LOW); digitalWrite(in2, LOW);
  digitalWrite(in3, LOW); digitalWrite(in4, LOW);
  digitalWrite(in5, LOW); digitalWrite(in6, LOW);
  digitalWrite(in7, LOW); digitalWrite(in8, LOW);
}
```
 **Tinkercad Simulation Link:**
[Click here to view and simulate the project in Tinkercad](https://www.tinkercad.com/things/5NnfC2BVMBH-4-dc-motor-control-with-2-l293d-motor-drivers/editel?returnTo=%2Fthings%2F5NnfC2BVMBH-4-dc-motor-control-with-2-l293d-motor-drivers&sharecode=eT_Xd0RYM8JJINVgLJ3mGkN_tA3FSxMiVy78Vb5zOTA)
