This paper proposes an Internet of Things (IoT) based solution for power management in rooms, aiming to minimize energy wastage when spaces are unoccupied. The system employs a network of sensors to detect human presence within a room. Upon detecting no occupants, it triggers an automatic shutdown of non-essential electrical devices and lighting to conserve energyThe implementation involves using sensors such as passive infrared (PIR) sensors or ultrasonic sensors to detect the presence of a person within the room. When a person enters the room, the sensor detects the motion or presence and triggers a microcontroller-based control unit. This control unit is programmed to actuate a relay or switch mechanism that disconnects the power supply to the room's electrical outlets.Conversely, when the room is empty, and no motion or presence is detected for a specified period, the control system reverts to its default state, restoring power to the outlets.

HARDWARE SPECIFICATIONS FOR APPLICATION
  Processor : Pentium IV Or Higher
  Memory Size : 256 GB (Minimum)
  HDD : 40 GB (Minimum)
SOFTWARE SPECIFICATIONS
  Operating System : WINDOWS 10
  Application : ARDUINO IDE
HARDWARE COMPONENTS FOR PROTOTYPE
  Sensor : PIR-Sensor
  Board : Arduino Uno
 H Bridge motor :Motor




CODE EXPLAINATION
This Arduino code is designed to perform specific tasks based on the analog input read from pin A0. Let's break down each section to understand its functionality:

### setup() Function

cpp
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  pinMode(2,OUTPUT);
  pinMode(3,OUTPUT);
  pinMode(4,OUTPUT);
  pinMode(5,OUTPUT);
  digitalWrite(5,HIGH);
}


- Serial.begin(9600);: Initializes the serial communication at a baud rate of 9600 bits per second. This allows the Arduino to communicate with the computer or other serial devices.
- pinMode(2,OUTPUT);, pinMode(3,OUTPUT);, pinMode(4,OUTPUT);, pinMode(5,OUTPUT);: Sets digital pins 2, 3, 4, and 5 as output pins. This configuration allows these pins to send signals.
- digitalWrite(5,HIGH);: Sets digital pin 5 to HIGH, which turns it on (provides 5V). This could be used to indicate an initial state or to control a connected device.

### loop() Function

cpp
void loop() {
  Serial.println(analogRead(A0));
  if(analogRead(A0)>400)
  {
    analogWrite(3,60);
    digitalWrite(5,LOW);
    delay(2000);
    analogWrite(3,0);
    digitalWrite(5,HIGH);
    delay(2000);
  }
}


- Serial.println(analogRead(A0));: Reads the analog value from pin A0 and prints it to the serial monitor. This is useful for debugging or monitoring the analog input.
- if(analogRead(A0)>400): Checks if the analog value read from pin A0 is greater than 400. If the condition is true, the following code block executes:
  - analogWrite(3,60);: Sends a PWM signal with a duty cycle of approximately 23.5% (60 out of 255) to pin 3. This can be used to control the speed of a motor or the brightness of an LED.
  - digitalWrite(5,LOW);: Sets digital pin 5 to LOW, turning it off (0V).
  - delay(2000);: Pauses the program for 2000 milliseconds (2 seconds).
  - analogWrite(3,0);: Stops the PWM signal to pin 3, effectively turning off whatever is connected to it.
  - digitalWrite(5,HIGH);: Sets digital pin 5 back to HIGH, turning it on again.
  - delay(2000);: Pauses the program for another 2000 milliseconds (2 seconds).

### Explanation

This code continuously monitors the analog input from pin A0. If the input exceeds a threshold value of 400, it performs a sequence of actions: 

1. It writes a PWM signal to pin 3 (could be controlling a motor or an LED).
2. Turns off pin 5.
3. Waits for 2 seconds.
4. Stops the PWM signal to pin 3.
5. Turns on pin 5.
6. Waits for another 2 seconds.

This sequence repeats as long as the condition (analog value greater than 400) is met. The Serial.println(analogRead(A0)); statement allows for real-time monitoring of the analog input values through the serial monitor, which can help in understanding and debugging the system's behavior.