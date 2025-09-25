# Exercise 2: Spaceship Interface

Time to start using the power of the Arduino! Before we get started with programming, lets go over our materials for this section:
 - 3 LEDs (2 red, 1 green)
 - Push Button
 - 3x 220 Ohm Resistor
 - 1x 10 kOhm Resistor

[Picture of all the components]

We’re gonna start by wiring up all of our LEDs and our button. First, our LEDs. We wire each one so that the anode is connected to a pin on the Arduino (We’ll use pins 3-5 for this) and the other side is connected through a 220 Ohm resistor to ground. This will allow us to control when the LEDs receive power from the Arduino. We also connect the button to the board, connecting one side to 5V and the other side to a pin on the Arduino. This way, when the button is pressed, it completes the circuit, which the Arduino can then detect and react to. The final step is to add the 10kOhm resistor between the output of the switch and the ground lane. This is called a pull-down resistor, making sure the Arduino detects a LOW signal when the button is open.

[Picture of the static circuit] [Circuit Diagram]

Now we have our circuit, but the Arduino doesn’t know what to do yet! Let’s take a look at our code for this project. As a quick overview, most Arduino projects will have 2 main functions: setup(), which runs once when the program is first started, and loop(), which runs itself repeatedly while the Arduino is on.

To start, we’ll make a variable to store if we’re pressing the button

```cpp
int switchState = 0;
```

Then in setup, we'll tell the Arduino what we're using the pins for. We have the LEDs in pins 3, 4, and 5, so those will be marked as Output pins. The switch in pin 2 will be marked as Input.
```cpp
void setup() {
  // put your setup code here, to run once:
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(2, INPUT);
}
```

void loop() {
  // put your main code here, to run repeatedly:
  switchState = digitalRead(2);

  if(switchState == LOW) {
    digitalWrite(3, HIGH);
    digitalWrite(4, LOW);
    digitalWrite(5, LOW);
  }
  else {
    digitalWrite(3, LOW);
    digitalWrite(4, LOW);
    digitalWrite(5, HIGH);
    delay(250);
    
    digitalWrite(4, HIGH);
    digitalWrite(5, LOW);
    delay(250);
  }
}

