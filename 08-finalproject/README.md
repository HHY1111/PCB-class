## 01  CapacitiveSensor + Solenoid + LEDs最终代码
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

   pinMode(A0, OUTPUT);  // LED output，flower 1
   pinMode(A1, OUTPUT);  // LED output，flower 2
   pinMode(A2, OUTPUT);  // LED output，flower 3
   pinMode(A3, OUTPUT);  // LED output，flower 4
   pinMode(A4, OUTPUT);  // LED output，flower 5

}

void loop()                    
{
    randNumber = random(8, 12);    // Generate random numbers between 1-5
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

    if (Sensor1 < 50) {    // trigger a solenoid1，flower 1, !! "99" need to be tested!!
        do {randNumber = random(8, 12);
        } while (randNumber != 8);
        // Generate random numbers between 8-12 except for 8
        Serial.println(randNumber);
        digitalWrite(randNumber,HIGH);   // trigger a solenoid in addition to the solenoid1，make any flower other than flower1 release its scent
        analogWrite(A0,255);
          if (randNumber == 1){
          anologPin = A0;
        }
        delay(300);   //   the solenoid keep pushing the bubble for 300 to release the scent
        digitalWrite(randNumber,LOW);   //   switch the solenoid off to restore to initial state
        analogWrite(randNumber,LOW);

    }

    else if (Sensor2 < 50) {    // trigger a solenoid2，flower 2
        do {
        randNumber = random(8, 12);
        } while (randNumber != 9);
        // Generate random numbers between 8-12 except for 9
        Serial.println(randNumber);
        digitalWrite(randNumber,HIGH);   // trigger a solenoid in addition to the solenoid2，make any flower other than flower2 release its scent
        delay(300);   //   the solenoid keep pushing the bubble for 300 to release the scent
        digitalWrite(randNumber,LOW);   //   switch the solenoid off to restore to initial state
    }
    
    else if (Sensor3 < 50) {    // trigger a solenoid3，flower 3
        do {
        randNumber = random(8, 12);
        } while (randNumber != 10);
        // Generate random numbers between 8-12 except for 10
        Serial.println(randNumber);
        digitalWrite(randNumber,HIGH);   // trigger a solenoid in addition to the solenoid3，make any flower other than flower3 release its scent
        delay(300);   //   the solenoid keep pushing the bubble for 300 to release the scent
        digitalWrite(randNumber,LOW);   //   switch the solenoid off to restore to initial state
    }

    else if (Sensor4 < 50) {    // trigger a solenoid4，flower 4
        do {
        randNumber = random(8, 12);
        } while (randNumber != 11);
        // Generate random numbers between 8-12 except for 11
        Serial.println(randNumber);
        digitalWrite(randNumber,HIGH);   // trigger a solenoid in addition to the solenoid4，make any flower other than flower4 release its scent
        delay(300);   //   the solenoid keep pushing the bubble for 300 to release the scent
        digitalWrite(randNumber,LOW);   //   switch the solenoid off to restore to initial state
    }

    else if (Sensor5 < 50) {    // trigger a solenoid5，flower 5
        do {
        randNumber = random(8, 12);
        } while (randNumber != 12);
        // Generate random numbers between 8-12 except for 12
        Serial.println(randNumber);
        digitalWrite(randNumber,HIGH);   // trigger a solenoid in addition to the solenoid5，make any flower other than flower5 release its scent
        delay(300);   //   the solenoid keep pushing the bubble for 300 to release the scent
        digitalWrite(randNumber,LOW);   //   switch the solenoid off to restore to initial state
    }
    
    delay(50);                             // arbitrary delay to limit data to serial port 
}
```





## 02  CapacitiveSensor + Servo motors + LEDs最终代码
```
#include <CapacitiveSensor.h>
#include <Servo.h>

Servo myservo;  // create servo object to control a servo
/*
 * CapitiveSense Library Demo Sketch
 * Paul Badger 2008
 * Uses a high value resistor e.g. 10M between send pin and receive pin
 * Resistor effects sensitivity, experiment with values, 50K - 50M. Larger resistor values yield larger sensor values.
 * Receive pin is the sensor pin - try different amounts of foil/metal on this pin
 */
long randNumber;        //Randomly generate random numbers from 1-5，using a random seed: and a different random number each time the program is launched

int pos = -10;    // variable to store the servo position

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

   pinMode(A0, OUTPUT);  // LED output，flower 1
   pinMode(A1, OUTPUT);  // LED output，flower 2
   pinMode(A2, OUTPUT);  // LED output，flower 3
   pinMode(A3, OUTPUT);  // LED output，flower 4
   pinMode(A4, OUTPUT);  // LED output，flower 5

}

void loop()                    
{
    randNumber = random(8, 12);    // Generate random numbers between 1-5
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

    if (Sensor1 < 1000) {    // trigger a solenoid1，flower 1, !! "99" need to be tested!!
        do {randNumber = random(8, 12);
        } while (randNumber != 8);
        // Generate random numbers between 8-12 except for 8
           Serial.println(randNumber);
           analogWrite(randNumber,HIGH);
           pos = 20;  // 设置伺服电机的目标位置为20度
           myservo.write(pos);  
           delay(50);   //   the solenoid keep pushing the bubble for 300 to release the scent
           pos = -10;   //   转回初识角度
           analogWrite(randNumber,LOW);

    }

    else if (Sensor2 < 1000) {    // trigger a solenoid2，flower 2
        do {
        randNumber = random(8, 12);
        } while (randNumber != 9);
        // Generate random numbers between 8-12 except for 9
        Serial.println(randNumber);
         pos = 20;  // 设置伺服电机的目标位置为20度
         myservo.write(pos);
         delay(50);   //   the solenoid keep pushing the bubble for 300 to release the scent
         pos = -10;  //   转回初识角度
    }
    
    else if (Sensor3 < 1000) {    // trigger a solenoid3，flower 3
        do {
        randNumber = random(8, 12);
        } while (randNumber != 10);
        // Generate random numbers between 8-12 except for 10
        Serial.println(randNumber);
         pos = 20;  // 设置伺服电机的目标位置为20度
         myservo.write(pos);
         delay(50);   //   the solenoid keep pushing the bubble for 300 to release the scent
         pos = -10;  //   转回初识角度
    }

    else if (Sensor4 < 1000) {    // trigger a solenoid4，flower 4
        do {
        randNumber = random(8, 12);
        } while (randNumber != 11);
        // Generate random numbers between 8-12 except for 11
        Serial.println(randNumber);
         pos = 20;  // 设置伺服电机的目标位置为20度
         myservo.write(pos);
         delay(50);   //   the solenoid keep pushing the bubble for 300 to release the scent
         pos = -10;  //   转回初识角度
    }

    else if (Sensor5 < 1000) {    // trigger a solenoid5，flower 5
        do {
        randNumber = random(8, 12);
        } while (randNumber != 12);
        // Generate random numbers between 8-12 except for 12
        Serial.println(randNumber);
         pos = 20;  // 设置伺服电机的目标位置为20度
         myservo.write(pos);
         delay(50);   //   the solenoid keep pushing the bubble for 300 to release the scent
         pos = -10;  //   转回初识角度
    }
    
    delay(50);                             // arbitrary delay to limit data to serial port 
}
```
