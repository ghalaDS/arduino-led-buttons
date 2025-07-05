# arduino-led-buttons
A simple interactive Arduino UNO project to control 3 LEDs (Blue, Red, Yellow) using 3 push buttons.  
Each button is wired to either turn ON or OFF a specific LED.

---

# Project Preview

Below are screenshots of the project simulation in Tinkercad:

# All LEDs OFF
![OFF](OFF.png)

# LEDs ON After Button Press
![ON](ON.png)

---

# Try It Yourself

You can try the full simulation here:  
[View on Tinkercad](https://www.tinkercad.com/things/0PPjGCHGqF2-exquisite-gaaris-fyyran)

Click "**Start Simulation**" to see how the buttons control each LED.

---

# Components Used

- 1x Arduino UNO
- 3x LEDs (Blue, Red, Yellow)
- 3x Push Buttons
- 3x 470Ω Resistors
- Breadboard
- Jumper Wires

---

# Arduino Code Example

This example shows the full logic to toggle 3 LEDs using 3 push buttons:

```cpp
const int buttonPins[] = {2, 3, 4};
const int ledPins[] = {9, 10, 11};
bool ledStates[] = {false, false, false};
bool lastButtonStates[] = {HIGH, HIGH, HIGH};

void setup() {
  for (int i = 0; i < 3; i++) {
    pinMode(buttonPins[i], INPUT);
    digitalWrite(buttonPins[i], HIGH); // enable internal pull-up
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  for (int i = 0; i < 3; i++) {
    bool currentButton = digitalRead(buttonPins[i]);
    if (currentButton == LOW && lastButtonStates[i] == HIGH) {
      ledStates[i] = !ledStates[i];
      digitalWrite(ledPins[i], ledStates[i]);
      delay(10); // simple debounce
    }
    lastButtonStates[i] = currentButton;
  }
}
