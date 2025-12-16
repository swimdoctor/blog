Exercise 1: Introduction and Setup

Alright, we have all the parts and now it’s time to start putting them together. For this exercise, alongside the Arduino and a breadboard, we’ll be using:
 - 1 LED
 - 2 Push Buttons
 - 1 220 Ohm Resistor
 - Assorted Jumper Wires 

For this first exercise, we’ll only be using the Arduino as a power source, so we’ll start by plugging its 5V and ground pins to the + and - rows on the breadboard. We’ll then place the LED, resistor, and push button on the breadboard, creating a simple circuit as shown below. When the switch is pressed, it will complete the circuit, letting power flow through the resistor and light up the LED. 

![Single Circuit](./Images/Exercise1a.gif)

The resistor is important here, as it lowers the current, making it safe for us to power the LED. If we connected the LED directly to 5V, the LED would receive too much current, and get hot and eventually break. 

Next, we’re gonna attach the other push button in series. This means that we have to close both switches in order to fully complete the circuit and turn on the LED. This is what’s known as an AND gate, where both input 1 AND input 2 must be pressed in order to complete the circuit. You can see the circuit in action here:

![Series Circuit](./Images/Exercise1b.jpg)

Now what if we want the LED to turn on if we press just one of the buttons? For that, we can connect the switches in parallel, where either switch can be pressed to create a closed circuit to light up the LED. This is called an OR gate, where either input 1 OR input 2 must be pressed.

![Parallel Circuit](./Images/Exercise1c.jpg)

That’s all for this first exercise. This is my first time using jumper cables that are pre-cut to size, and it makes the circuits we build look so much cleaner and professional. These first circuits are just the building blocks we can use going forwards, and I’m super excited to see what’s next. In the next exercise, we’ll try programming the arduino for the first time to let it control our LEDs.
