# Joystick-and-servo-motor
This code you can control servo with a joystick with a help of arduino uno
->#include <Servo.h>

// Joystick pins
const int xPin = A0;
const int yPin = A1;        // not used yet, but kept
const int buttonPin = 2;

// Servo
Servo myServo;
const int servoPin = 7;

void setup() {
  Serial.begin(9600);

  pinMode(buttonPin, INPUT_PULLUP);

  myServo.attach(servoPin);   // servo on pin 7
}

void loop() {
  int xValue = analogRead(xPin);   // 0–1023
  int buttonState = digitalRead(buttonPin);

  // Map joystick X to servo angle (0–180)
  int angle = map(xValue, 0, 1023, 0, 180);
  myServo.write(angle);

  // Debug
  Serial.print("X: ");
  Serial.print(xValue);
  Serial.print(" | Servo angle: ");
  Serial.print(angle);
  Serial.print(" | Button: ");

  if (buttonState == LOW) {
    Serial.println("PRESSED");
  } else {
    Serial.println("RELEASED");
  }

  delay(15); // smooth movement
}
