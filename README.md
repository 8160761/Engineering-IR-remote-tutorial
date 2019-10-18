# Engineering-IR-remote-tutorial
#Tutorial

Firstly we need to add the IR remote library
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

```cpp

void loop() {
  if (irrecv.decode(&results))
    unsigned int value = results.value;
    Serial.println(value);
   
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
