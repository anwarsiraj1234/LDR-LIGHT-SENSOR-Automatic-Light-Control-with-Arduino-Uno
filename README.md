ARDUINO ROBOTICS
PROJECT FILE
Circuit Diagrams, Code and Line-by-Line Explanation
Educator Renaissance Campus
Made by Sir Anwar Siraj, DS AI Robotics
Contents
Project 1	Smart Traffic Control System
Red, Yellow and Green LEDs with timed sequence

Project 2	LDR Light Sensor
Automatic LED control using a light sensor on A0

GitHub	README Text (copy and paste)
Ready-made README for both projects, with picture file names

Each project includes: overview, components, circuit diagram, complete code and a line-by-line explanation. The last section holds the GitHub README text.
PROJECT 1
SMART TRAFFIC
CONTROL SYSTEM
Arduino Traffic Light Controller
Educator Renaissance Campus
Made by Sir Anwar Siraj, DS AI Robotics
1. Project Overview
The Smart Automated Traffic Control System is an Arduino-based robotics project that simulates real traffic management. The program switches Red, Yellow and Green LEDs in a fixed timed sequence, showing how timing and automated logic manage vehicle flow.
Key Features
•	Precise timing: Red 4 seconds, Yellow 2 seconds, Green 4 seconds.
•	Clean code: one helper function, showLight(), controls all three lights.
•	Modular: the module plugs straight into the Arduino header and can join a larger Smart City model.
2. Components Required
#	Component	Quantity	Note
1	Arduino Uno with USB cable	1	Controller
2	Traffic light LED module (G, Y, R, GND)	1	3 LEDs on one board
3	Jumper wires (only if not plugged directly)	4	Male to female
3. Traffic Light Module and Pins
The module has four pins, marked G, Y, R and GND from left to right. The photo shows the module plugged directly onto the Arduino Uno header, where these four pins line up with pins 11, 12, 13 and GND.
 
Real setup: module plugged on the Arduino Uno
Connection Table
Module pin	Arduino pin	Meaning
G	Pin 11	Green LED (Go)
Y	Pin 12	Yellow LED (Caution)
R	Pin 13	Red LED (Stop)
GND	GND	Ground (negative) for all three LEDs
4. Circuit Diagram
 
Note: If your module does not have built-in resistors, add a 220 Ω resistor in series with each of the G, Y and R lines to protect the LEDs.
5. Timing Sequence
Order	Light	Duration	Meaning
1st	RED	4 seconds	Stop
2nd	YELLOW	2 seconds	Caution
3rd	GREEN	4 seconds	Go
Total cycle		10 seconds	Then repeats

6. Complete Arduino Code
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
7. Line-by-Line Code Explanation
Line numbers count every line of the code above, including blank lines.
Line	Code	Explanation
Step 1 – Project heading (comment)
1–5	/* ... */	A multi-line comment with the project name, organization and author. The compiler ignores it.
Step 2 – Pin names (constants)
7	const int redLED = 13;	Gives pin 13 the name redLED. const means the value never changes.
8	const int yellowLED = 12;	Gives pin 12 the name yellowLED.
9	const int greenLED = 11;	Gives pin 11 the name greenLED.
Step 3 – setup() runs once
11	void setup() {	Starts the setup function. Arduino runs it one time after power-on or reset.
12	pinMode(redLED, OUTPUT);	Makes pin 13 an output so Arduino can send voltage to the red LED.
13	pinMode(yellowLED, OUTPUT);	Makes pin 12 an output for the yellow LED.
14	pinMode(greenLED, OUTPUT);	Makes pin 11 an output for the green LED.
15	}	Ends the setup function.
Step 4 – showLight() helper function
17	// Turn on only ...	A comment: this function turns on one LED and turns the other two off.
18	void showLight(int pin) {	Creates our own function. The value passed in (pin) tells it which LED to turn on.
19	digitalWrite(redLED, pin == redLED ? HIGH : LOW);	Checks: is pin equal to redLED? If yes, send HIGH (red ON). If no, send LOW (red OFF).
20	digitalWrite(yellowLED, pin == yellowLED ? HIGH : LOW);	Same check for yellow: ON only when yellow was chosen.
21	digitalWrite(greenLED, pin == greenLED ? HIGH : LOW);	Same check for green: ON only when green was chosen.
22	}	Ends the function. Result: exactly one light is ON at a time.
Step 5 – loop() repeats forever
24	void loop() {	Starts the main function. Arduino repeats it again and again.
25	showLight(redLED);	Turns RED on (Stop). Yellow and green go OFF.
26	delay(4000);	Waits 4000 milliseconds = 4 seconds, so red stays on.
28	showLight(yellowLED);	Turns YELLOW on (Caution). Red and green go OFF.
29	delay(2000);	Waits 2 seconds with yellow on.
31	showLight(greenLED);	Turns GREEN on (Go). Red and yellow go OFF.
32	delay(4000);	Waits 4 seconds with green on.
33	}	Ends loop(). Arduino jumps back to line 25 and the cycle starts again with red.

8. How the Program Works
•	Arduino starts and setup() sets pins 13, 12 and 11 as outputs.
•	loop() calls showLight(redLED): red is ON, the others are OFF, for 4 seconds.
•	Then showLight(yellowLED): yellow is ON for 2 seconds.
•	Then showLight(greenLED): green is ON for 4 seconds.
•	loop() ends and starts again at red. The 10-second cycle repeats forever.
9. Tips
•	To change a duration, edit the number inside delay(). 1000 equals 1 second.
•	To change a pin, edit only the three const int lines at the top.
PROJECT 2
LDR LIGHT SENSOR
Automatic Light Control with Arduino Uno
Made by Sir Anwar Siraj, DS & AI Robotics
1. Project Overview
This project uses a Light Dependent Resistor (LDR) to detect light. Arduino reads the light level through pin A0 and switches an LED on when it is dark and off when it is bright, like an automatic street light.
2. What Is an LDR?
Definition
An LDR is a passive semiconductor device whose resistance decreases as light intensity increases.
Working Principle (Photoconductivity)
An LDR works on the principle of photoconductivity: light gives energy to electrons, so the material conducts better.
Step	What happens
Step 1 – No Light (Dark Condition)	Very few electrons are free, so current cannot flow easily. Resistance becomes very high and current is low.
Step 2 – Light Falls on the LDR	Photons strike the semiconductor material. Electrons gain energy and more free electrons are created.
Step 3 – Conductivity Increases	More free electrons are available, so current flows more easily and resistance decreases rapidly.
Step 4 – Arduino Reads the Voltage	The LDR and the 10 kΩ resistor form a voltage divider. Arduino reads the voltage at A0, compares it with the threshold and controls the LED.

Voltage Divider Result
Condition	LDR resistance	Value at A0	LED (pin 13)
Dark	High	Low (70 or below)	ON
Bright	Low	High (above 70)	OFF

Note: This result is for this circuit, where the LDR is on the 5V side and the 10 kΩ resistor is on the GND side. If you swap their positions, the readings are reversed.
3. Components Required
#	Component	Quantity	Note
1	Arduino Uno with USB cable	1	Controller
2	LDR (photoresistor)	1	Light sensor
3	10 kΩ resistor	1	Voltage divider
4	LED (any color)	1	Output
5	220 Ω resistor	1	Protects the LED
6	Breadboard and jumper wires	1 set	Connections
4. Circuit Diagram
 
Connection Table
Component / leg	Arduino connection	Role
LDR leg 1	5V (positive)	Supply side of the voltage divider
LDR leg 2	Junction with 10 kΩ resistor and pin A0	Signal point read by analogRead()
10 kΩ resistor leg 1	Same junction as LDR leg 2 and A0	Pull-down resistor of the divider
10 kΩ resistor leg 2	GND (negative)	Completes the divider to ground
LED long leg (+)	Pin D13 through a 220 Ω resistor	Output indicator
LED short leg (−)	GND (negative)	Return path

Important Points
•	LDR has no polarity. Either leg can go to 5V. One leg goes to 5V (positive) and the other goes to the A0 junction.
•	A0 is connected at the point between the LDR and the 10 kΩ resistor.
•	The 10 kΩ resistor goes from the A0 junction to GND (negative).
•	LED: the long leg (+) goes toward pin 13 through a 220 Ω resistor; the short leg (−) goes to GND.
5. Complete Arduino Code
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
6. Line-by-Line Code Explanation
The line numbers below count the lines in the code above (blank lines included).
Line	Code	Explanation
Step A – Credit and variables
1	// MADE BY ...	A comment. The compiler ignores it. It credits the author.
3	int ldrPin = A0;	Creates a variable named ldrPin and stores analog pin A0, where the LDR voltage divider is connected.
4	int led = 13;	Stores pin 13, where the LED is connected through a 220 Ω resistor.
5	int threshold = 70;	The limit value. Readings of 70 or below mean it is dark. Change it to adjust sensitivity.
Step B – setup() runs once at start
7	void setup()	Starts the setup function. Arduino runs it one time after power-on or reset.
8, 11	{  and  }	Opening and closing braces that mark the start and end of the function.
9	Serial.begin(9600);	Starts serial communication at 9600 baud so values can be shown on the Serial Monitor.
10	pinMode(led, OUTPUT);	Sets pin 13 as an output so Arduino can switch the LED on and off. (A0 is an input by default.)
Step C – loop() runs again and again
13	void loop()	Starts the main function. Arduino repeats everything inside it continuously.
15	int data = analogRead(ldrPin);	Reads the voltage at A0 and converts it to a number from 0 to 1023. The number is saved in data.
Step D – Showing the value on the Serial Monitor
16	Serial.println("");	Prints an empty line, so each new reading starts on a new line.
17	Serial.print("Light Sensor ");	Prints the text Light Sensor without moving to a new line.
18	Serial.print("Value = ");	Prints the text Value = on the same line.
19	Serial.print(data);	Prints the reading stored in data. Example: Light Sensor Value = 45.
Step E – Decision: control the LED
20	if(data <= threshold)	Checks if the reading is less than or equal to 70 (dark). If true, the next block runs.
22	digitalWrite(led, HIGH);	Sends 5V to pin 13, so the LED turns ON in the dark.
24	else	Runs when the condition is false, meaning the reading is above 70 (bright).
26	digitalWrite(led, LOW);	Sends 0V to pin 13, so the LED turns OFF in the light.
27–28	}	The closing brace of the else block, then of loop(). The program jumps back to the start of loop().

7. Working of the Program
•	Arduino reads the light level from A0 as a number (0 to 1023).
•	The number is printed on the Serial Monitor.
•	If the number is 70 or below, it is dark and the LED turns ON.
•	If the number is above 70, it is bright and the LED turns OFF.
•	The loop repeats continuously.
8. Tips
•	Open the Serial Monitor (9600 baud) and cover the LDR to see the values drop. Change threshold to match your room.
•	Optional: add delay(200); at the end of loop() to make the Serial Monitor easier to read.
•	Use the same pin order shown in the circuit diagram to avoid wrong readings.
GITHUB README
GitHub README Text
Copy everything inside the box below and paste it into the README.md editor on GitHub. Then upload these three picture files to the same folder, keeping the names exactly: traffic-circuit-diagram.png, ldr-circuit-diagram.png and module-setup.jpg.
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
 

