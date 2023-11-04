# Assignment's Title

```
#include <CapacitiveSensor.h>

/*
 * CapitiveSense Library Demo Sketch
 * Paul Badger 2008
 * Uses a high value resistor e.g. 10M between send pin and receive pin
 * Resistor effects sensitivity, experiment with values, 50K - 50M. Larger resistor values yield larger sensor values.
 * Receive pin is the sensor pin - try different amounts of foil/metal on this pin
 */
long randNumber;        //Randomly generate random numbers from 1-5，using a random seed: and a different random number each time the program is launched

CapacitiveSensor   cs_7_2 = CapacitiveSensor(7,2);        // 10M resistor between pins 4 & 2, pin 2 is sensor pin, add a wire and or foil if desired, flower 1
CapacitiveSensor   cs_7_3 = CapacitiveSensor(7,3);        // 10M resistor between pins 4 & 3, pin 6 is sensor pin, add a wire and or foil, flower 2
CapacitiveSensor   cs_7_4 = CapacitiveSensor(7,4);        // 10M resistor between pins 4 & 4, pin 8 is sensor pin, add a wire and or foil, flower 3
CapacitiveSensor   cs_7_5 = CapacitiveSensor(7,5);        // 10M resistor between pins 4 & 4, pin 8 is sensor pin, add a wire and or foil, flower 4
CapacitiveSensor   cs_7_6 = CapacitiveSensor(7,6);        // 10M resistor between pins 4 & 4, pin 8 is sensor pin, add a wire and or foil, flower 5

void setup()                    
{
   cs_7_2.set_CS_AutocaL_Millis(0xFFFFFFFF);     // turn off autocalibrate on channel 1 - just as an example
   Serial.begin(9600);

   pinMode(8, OUTPUT); // connect solenoid1 to the pin 8, flower 1 release scent
   pinMode(9, OUTPUT); // connect solenoid2 to the pin 9, flower 2 release scent
   pinMode(10, OUTPUT); // connect solenoid3 to the pin 10, flower 3 release scent
   pinMode(11, OUTPUT); // connect solenoid4 to the pin 11, flower 4 release scent
   pinMode(12, OUTPUT); // connect solenoid5 to the pin 12, flower 5 release scent

}

void loop()                    
{
    randNumber = random(1, 5);    // Generate random numbers between 1-5
    Serial.println(randNumber);

    long start = millis();
    long Sensor1 =  cs_7_2.capacitiveSensor(30);
    long Sensor2 =  cs_7_3.capacitiveSensor(30);
    long Sensor3 =  cs_7_4.capacitiveSensor(30);
    long Sensor4 =  cs_7_5.capacitiveSensor(30);
    long Sensor5 =  cs_7_6.capacitiveSensor(30);

    Serial.print(millis() - start);        // check on performance in milliseconds
    Serial.print("\t");                    // tab character for debug windown spacing

    Serial.print(Sensor1);                  // print sensor output 1
    Serial.print("\t");
    Serial.print(Sensor2);                  // print sensor output 2
    Serial.print("\t");
    Serial.print(Sensor3);                // print sensor output 3
    Serial.print("\t");
    Serial.print(Sensor4);                // print sensor output 4
    Serial.print("\t");
    Serial.println(Sensor5);                // print sensor output 5

    if (Sensor1 > 99) {    // trigger a solenoid1，flower 1
    randNumber = random(1, 5);    // Generate random numbers between 1-5
    Serial.println(randNumber);
    Digital.Write(randNumber,HIGH);   // trigger a solenoid in addition to the solenoid1，make any flower other than flower1 release its scent
    }

    else if (Sensor2 > 99) {    // trigger a solenoid2，flower 2
    
    }
    else { // temperature < 60
    // Safe! Continue usual tasks.
    }

    delay(50);                             // arbitrary delay to limit data to serial port 
}
```
