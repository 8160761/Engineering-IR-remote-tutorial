# Engineering-IR-remote-tutorial

Firstly we need to add the IR remote library.

You need to add the IR library to the list of libraries in the arduino coding software.
The library can be found 
[here](https://github.com/z3t0/Arduino-IRremote) 
then added to arduino by selecting sketch >> include library >> add zip library

```cpp

#include <IRremote.h>

```
Then we need to define the pins.

```cpp
//Define Pins
int redLed = 2;
int greenLed = 4;
int blueLed = 3;
int RECV_PIN = 11;

```
Specify items from the IR library which will be used in this code

```cpp
IRrecv irrecv(RECV_PIN);
decode_results results;
```
Set pin LED's to output and

```cpp
void setup()
{
 
  pinMode(redLed, OUTPUT);
  pinMode(greenLed, OUTPUT);
  pinMode(blueLed, OUTPUT);
  
 ```
 Enable the IR signal in
 ```cpp
 
  Serial.begin(9600);
  Serial.println("Enabling IRin");
  irrecv.enableIRIn();
  Serial.println("Enabled IRin");
}
```

We need to change the value to an unasigned int to that switch case may be used
Switch case allows you to run multiple conditions after each other, checking each one to see if its true.
```cpp

void loop() {
  if (irrecv.decode(&results))
    unsigned int value = results.value;
    Serial.println(value);
    
```
These statements check to see if each one is true before moving on to the next. for example if the value = 2295 then the red light will turn on for half a second.
```cpp
   
    switch (value) {
      case 2295:
        digitalWrite(redLed, HIGH);
        delay(500);
        digitalWrite(redLed, LOW);
        break;
          
      case 18615:
        digitalWrite(greenLed, HIGH);
        delay(500);
        digitalWrite(greenLed, LOW);
        break;
     
      case 10455:
        digitalWrite(blueLed, HIGH);
        delay(500);
        digitalWrite(blueLed, LOW);
    }
   
   
    irrecv.resume();
  }
}
```
