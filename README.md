# Engineering-IR-remote-tutorial
#Tutorial
```cpp

#include <IRremote.h>
//Define Pins
int redLed = 2;
int greenLed = 4;
int blueLed = 3;
int RECV_PIN = 11;

IRrecv irrecv(RECV_PIN);
decode_results results;


void setup()
{
 
  pinMode(redLed, OUTPUT);
  pinMode(greenLed, OUTPUT);
  pinMode(blueLed, OUTPUT);
 
  Serial.begin(9600);
  Serial.println("Enabling IRin");
  irrecv.enableIRIn();
  Serial.println("Enabled IRin");
}

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
