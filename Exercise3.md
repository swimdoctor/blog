# Exercise 3: Love-o-Meter

For this project, we’re moving into the world of analog sensors and temperature readings. The goal here is to measure the ambient temperature of the room and then use LEDs to visualize how much warmer things get when you touch the sensor. Before we jump in, here’s what we’ll be using:

- 3 LEDs  
- 3× 220 Ohm Resistors  
- 1 TMP36 Temperature Sensor  
- Breadboard  
- Assorted Jumper Wires  

As usual, we’ll start by wiring up power and ground from the Arduino to the + and – rails on the breadboard. Each LED’s cathode (short leg) is connected to ground through a 220 Ohm resistor, while the anodes are connected to pins 2, 3, and 4 on the Arduino. These LEDs will act as our temperature indicators.

Next up is the TMP36 temperature sensor. Orientation matters here, so we place it with the rounded side facing away from the Arduino. The left pin connects to 5V, the right pin connects to ground, and the center pin goes to A0, which is our analog input pin.

![Alt Text - Exercise3a.jpg](./Images/Exercise3a.jpg)

Once everything is wired up, we can make things a bit more fun by creating a simple interface. The book suggests using a paper cutout—like a hand or a pair of lips—that sits over the sensor and LEDs. Pressing or holding the sensor changes its temperature, which the Arduino can detect.

![Alt Text - Exercise3b.jpg](./Images/Exercise3b.jpg)

With the hardware finished, it’s time to look at the code. We start by defining a couple of constants: one for the sensor pin, and one for the **baseline temperature**. This baseline represents the room temperature before anyone touches the sensor.

```cpp
const int sensorPin = A0;
const float baselineTemp = 20.0;
