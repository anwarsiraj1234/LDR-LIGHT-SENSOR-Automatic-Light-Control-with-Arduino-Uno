# Arduino Robotics Projects
 
**Educator Renaissance Campus**
 
> Made by **Sir Anwar Siraj, DS AI Robotics**
 
## Contents
 
1. [Smart Traffic Control System](#smart-traffic-control-system)
2. [LDR Light Sensor](#ldr-light-sensor)
 
---
 
## Smart Traffic Control System
 
**Arduino Traffic Light Controller**
Educator Renaissance Campus
 
> Made by **Sir Anwar Siraj, DS AI Robotics**
 
---
 
### Project Overview
 
The Smart Automated Traffic Control System is an Arduino-based robotics project that simulates real traffic management. The program switches Red, Yellow and Green LEDs in a fixed timed sequence, showing how timing and automated logic manage vehicle flow.
 
#### Key Features
 
- **Precise timing:** Red 4 seconds, Yellow 2 seconds, Green 4 seconds
- **Clean code:** one helper function, `showLight()`, controls all three lights
- **Modular:** the module plugs straight into the Arduino header and can join a larger Smart City model
 
---
 
### Components Required
 
| # | Component | Quantity |
|---|-----------|----------|
| 1 | Arduino Uno with USB cable | 1 |
| 2 | Traffic light LED module (G, Y, R, GND) | 1 |
| 3 | Jumper wires (only if not plugged directly) | 4 |
 
---
 
### Hardware Setup
 
The module has four pins marked **G, Y, R, GND** from left to right. It plugs directly onto the Arduino Uno header, where these pins line up with pins 11, 12, 13 and GND.
 
<p align="center">
  <img src="module-setup.jpg" alt="Traffic light module plugged into Arduino Uno" width="250">
</p>
 
#### Pin Connections
 
| Module Pin | Arduino Pin | Meaning |
|------------|-------------|---------|
| G | 11 | Green LED (Go) |
| Y | 12 | Yellow LED (Caution) |
| R | 13 | Red LED (Stop) |
| GND | GND | Ground (negative) |
 
---
 
### Circuit Diagram
 
![Circuit diagram](traffic-circuit-diagram.png)
 
> **Note:** If your module has no built-in resistors, add a 220 Ω resistor in series with each of the G, Y and R lines.
 
---
 
### Timing Sequence
 
| Order | Light | Duration | Meaning |
|-------|-------|----------|---------|
| 1st | 🔴 Red | 4 seconds | Stop |
| 2nd | 🟡 Yellow | 2 seconds | Caution |
| 3rd | 🟢 Green | 4 seconds | Go |
 
Total cycle: **10 seconds**, then it repeats.
 
---
 
### Arduino Code
 
```cpp
/*
 * PROJECT: SMART TRAFFIC CONTROL SYSTEM
 * ORGANIZATION: EDUCATOR RENAISSANCE CAMPUS
 * MADE BY SIR ANWAR SIRAJ, DS & AI ROBOTICS
 */
 
const int redLED    = 13;
const int yellowLED = 12;
const int greenLED  = 11;
 
void setup() {
  pinMode(redLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
}
 
// Turn on only the chosen LED; the other two go OFF
void showLight(int pin) {
  digitalWrite(redLED,    pin == redLED    ? HIGH : LOW);
  digitalWrite(yellowLED, pin == yellowLED ? HIGH : LOW);
  digitalWrite(greenLED,  pin == greenLED  ? HIGH : LOW);
}
 
void loop() {
  showLight(redLED);     // RED (STOP) for 4 seconds
  delay(4000);
 
  showLight(yellowLED);  // YELLOW (CAUTION) for 2 seconds
  delay(2000);
 
  showLight(greenLED);   // GREEN (GO) for 4 seconds
  delay(4000);
}
```
 
---
 
### Code Explanation
 
#### Step 1: Pin names
 
```cpp
const int redLED    = 13;
const int yellowLED = 12;
const int greenLED  = 11;
```
 
Each LED pin gets a name. `const` means the value never changes. To change a pin, edit only these three lines.
 
#### Step 2: `setup()` runs once
 
```cpp
void setup() {
  pinMode(redLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
}
```
 
`pinMode(..., OUTPUT)` makes the pins outputs so Arduino can send voltage to the LEDs.
 
#### Step 3: `showLight()` helper function
 
```cpp
void showLight(int pin) {
  digitalWrite(redLED,    pin == redLED    ? HIGH : LOW);
  digitalWrite(yellowLED, pin == yellowLED ? HIGH : LOW);
  digitalWrite(greenLED,  pin == greenLED  ? HIGH : LOW);
}
```
 
This function turns on only the chosen LED. The part `pin == redLED ? HIGH : LOW` means: if `pin` equals `redLED`, send HIGH (ON), otherwise send LOW (OFF). The same check is done for yellow and green, so exactly one light is ON at a time.
 
#### Step 4: `loop()` repeats forever
 
| Code | What it does |
|------|--------------|
| `showLight(redLED);` | Red ON, yellow and green OFF |
| `delay(4000);` | Wait 4 seconds (1000 ms = 1 second) |
| `showLight(yellowLED);` | Yellow ON, red and green OFF |
| `delay(2000);` | Wait 2 seconds |
| `showLight(greenLED);` | Green ON, red and yellow OFF |
| `delay(4000);` | Wait 4 seconds, then `loop()` starts again at red |
 
---
 
### How to Run
 
1. Plug the traffic light module onto the Arduino Uno (G to 11, Y to 12, R to 13, GND to GND).
2. Open the Arduino IDE and paste the code above.
3. Select **Tools > Board > Arduino Uno** and the correct port.
4. Click **Upload**.
 
---
 
### Author
 
**Sir Anwar Siraj, DS AI Robotics**
Educator Renaissance Campus
 
---
 
## LDR Light Sensor
 
**Automatic Light Control with Arduino Uno**
 
> Made by **Sir Anwar Siraj, DS & AI Robotics**
 
---
 
### Project Overview
 
This project uses a Light Dependent Resistor (LDR) to detect light. Arduino reads the light level through pin **A0** and switches an LED **ON when it is dark** and **OFF when it is bright**, like an automatic street light.
 
---
 
### What Is an LDR?
 
An LDR is a passive semiconductor device whose resistance **decreases as light intensity increases**. It works on the principle of **photoconductivity**.
 
| Step | What happens |
|------|--------------|
| 1. No light (dark) | Very few electrons are free, so current cannot flow easily. Resistance is very high and current is low. |
| 2. Light falls on the LDR | Photons strike the semiconductor material. Electrons gain energy and more free electrons are created. |
| 3. Conductivity increases | More free electrons are available, so current flows more easily and resistance decreases rapidly. |
| 4. Arduino reads the voltage | The LDR and the 10 kΩ resistor form a voltage divider. Arduino reads the voltage at A0, compares it with the threshold and controls the LED. |
 
#### Voltage Divider Result
 
| Condition | LDR resistance | Value at A0 | LED (pin 13) |
|-----------|----------------|-------------|--------------|
| Dark | High | Low (70 or below) | ON |
| Bright | Low | High (above 70) | OFF |
 
> **Note:** This result is for this circuit, where the LDR is on the 5V side and the 10 kΩ resistor is on the GND side. If you swap their positions, the readings are reversed.
 
---
 
### Components Required
 
| # | Component | Quantity |
|---|-----------|----------|
| 1 | Arduino Uno with USB cable | 1 |
| 2 | LDR (photoresistor) | 1 |
| 3 | 10 kΩ resistor | 1 |
| 4 | LED (any color) | 1 |
| 5 | 220 Ω resistor | 1 |
| 6 | Breadboard and jumper wires | 1 set |
 
---
 
### Circuit Diagram
 
![LDR circuit diagram](ldr-circuit-diagram.png)
 
#### Connections
 
| Component / leg | Arduino connection | Role |
|-----------------|--------------------|------|
| LDR leg 1 | 5V (positive) | Supply side of the voltage divider |
| LDR leg 2 | Junction with 10 kΩ resistor and pin **A0** | Signal point read by `analogRead()` |
| 10 kΩ resistor leg 1 | Same junction as LDR leg 2 and A0 | Pull-down resistor |
| 10 kΩ resistor leg 2 | GND (negative) | Completes the divider |
| LED long leg (+) | Pin **D13** through a 220 Ω resistor | Output indicator |
| LED short leg (−) | GND (negative) | Return path |
 
**Important points**
 
- The LDR has **no polarity**. One leg goes to 5V and the other goes to the A0 junction.
- A0 connects at the point **between the LDR and the 10 kΩ resistor**.
- The 10 kΩ resistor goes from the A0 junction to **GND**.
 
---
 
### Arduino Code
 
```cpp
// MADE BY SIR ANWAR SIRAJ DS & AI ROBOTICS
 
int ldrPin = A0;
int led = 13;
int threshold = 70;
 
void setup()
{
  Serial.begin(9600);
  pinMode(led, OUTPUT);
}
 
void loop()
{
  int data = analogRead(ldrPin);
  Serial.println("");
  Serial.print("Light Sensor ");
  Serial.print("Value = ");
  Serial.print(data);
  if(data <= threshold)
  {
    digitalWrite(led, HIGH);
  }
  else
  {
    digitalWrite(led, LOW);
  }
}
```
 
---
 
### Code Explanation
 
#### Step A: Variables
 
```cpp
int ldrPin = A0;
int led = 13;
int threshold = 70;
```
 
- `ldrPin` stores analog pin A0, where the LDR voltage divider is connected.
- `led` stores pin 13, where the LED is connected through a 220 Ω resistor.
- `threshold` is the limit value. Readings of 70 or below mean it is dark. Change it to adjust sensitivity.
 
#### Step B: `setup()` runs once
 
```cpp
void setup()
{
  Serial.begin(9600);
  pinMode(led, OUTPUT);
}
```
 
- `Serial.begin(9600);` starts serial communication so values can be shown on the Serial Monitor.
- `pinMode(led, OUTPUT);` sets pin 13 as an output so Arduino can switch the LED on and off. (A0 is an input by default.)
 
#### Step C: Read the sensor
 
```cpp
int data = analogRead(ldrPin);
```
 
Reads the voltage at A0 and converts it to a number from 0 to 1023. The number is saved in `data`.
 
#### Step D: Show the value on the Serial Monitor
 
```cpp
Serial.println("");
Serial.print("Light Sensor ");
Serial.print("Value = ");
Serial.print(data);
```
 
Prints one line like `Light Sensor Value = 45`. The first line prints an empty line so each new reading starts on a new line.
 
#### Step E: Decision, control the LED
 
```cpp
if(data <= threshold)
{
  digitalWrite(led, HIGH);
}
else
{
  digitalWrite(led, LOW);
}
```
 
- If `data` is **70 or below** (dark), `HIGH` sends 5V to pin 13 and the LED turns **ON**.
- Otherwise (bright), `LOW` sends 0V and the LED turns **OFF**.
- Then `loop()` starts again, so this repeats continuously.
 
---
 
### Tips
 
- Open the Serial Monitor (9600 baud) and cover the LDR to see the values drop. Change `threshold` to match your room.
- Optional: add `delay(200);` at the end of `loop()` to make the Serial Monitor easier to read.
 
---
 
### Author
 
**Sir Anwar Siraj, DS & AI Robotics**
 
