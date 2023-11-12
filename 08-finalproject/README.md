#最终最终的代码！！
```
#include <CapacitiveSensor.h>
#include <Servo.h>

//Servo servo1; // 伺服电机1，对应针脚3
//Servo servo2; // 伺服电机2，对应针脚5
//Servo servo3; // 伺服电机3，对应针脚6

Servo servos[] = {Servo(), Servo(), Servo()}; // 伺服电机数组
int servoPins[] = {3, 5, 6}; // 伺服电机对应的针脚数组

int pos = -20;    // variable to store the servo position
int i;

long randNumber;        //Randomly generate random numbers from 1-5，using a random seed: and a different random number each time the program is launche

CapacitiveSensor   cs_7_8 = CapacitiveSensor(7,8);        // 10M resistor between pins 7 & 8, pin 2 is sensor pin, add a wire and or foil if desired, flower 1
CapacitiveSensor   cs_7_9 = CapacitiveSensor(7,9);        // 10M resistor between pins 7 & 9, pin 2 is sensor pin, add a wire and or foil if desired, flower 2
CapacitiveSensor   cs_7_10 = CapacitiveSensor(7,10);        // 10M resistor between pins 7 & 10, pin 2 is sensor pin, add a wire and or foil if desired, flower 3

int pins[3][2] = {   // int pins【共3组数组】【每个数组中有2个数】，使用数组来对应servo和LED的针脚
 {3, 2},    // flower1 servo针脚PIN3，对应LED针脚PIN2
 {5, 4},    // flower1 servo针脚PIN5，对应LED针脚PIN4
 {6, 11},     // flower1 servo针脚PIN6，对应LED针脚PIN11
 // 3针脚对应2针脚，5针脚对应4针脚，6针脚对应11针脚
};

void setup()                    
{
   randomSeed(analogRead(0));   //初始化随机数
   for (int i = 0; i < 3; i++) {
    servos[i].attach(servoPins[i]);
  }

   servos[i].attach(servoPins[i]);

   servos[i].write(-10);    //定义servo的初识角度是-10

   cs_7_8.set_CS_AutocaL_Millis(0xFFFFFFFF);     // turn off autocalibrate on channel 1 - just as an example
   cs_7_9.set_CS_AutocaL_Millis(0xFFFFFFFF);     // turn off autocalibrate on channel 1 - just as an example
   cs_7_10.set_CS_AutocaL_Millis(0xFFFFFFFF);     // turn off autocalibrate on channel 1 - just as an example

   pinMode(2, OUTPUT);  // LED output，flower 1
   pinMode(4, OUTPUT);  // LED output，flower 2
   pinMode(11, OUTPUT);  // LED output，flower 3

   Serial.begin(9600);

}

void loop()                    
{

    long start = millis();
    long Sensor1 =  cs_7_8.capacitiveSensor(30);
    long Sensor2 =  cs_7_9.capacitiveSensor(30);
    long Sensor3 =  cs_7_10.capacitiveSensor(30);

    Serial.print(Sensor1);                  // print sensor output 1
    Serial.print("\t");
    Serial.print(Sensor2);                  // print sensor output 2
    Serial.print("\t");
    Serial.print(Sensor3);                // print sensor output 3
    Serial.println("\t");

   if (Sensor1 < 20) {    // trigger a solenoid1，flower 1, !! "99" need to be tested!!
        do {
        randNumber = random(3, 7); // 生成3到6之间的随机数
        } while (randNumber == 3 || randNumber == 4); // 如果随机数等于3或4，重新生成
        // Generate random numbers between 3-6 except for 4、3

        int i = randNumber;                            // 将randNumber付值给i
        int LEDpin = (pins[i][1]);                      // pin[i][1]
        Serial.println(randNumber);

         for (int i = 0; i < 3; i++) {
         if (randNumber == servoPins[i]) {
            servos[i].write(80);
            digitalWrite(LEDpin,HIGH);
            delay(300);                                     //   the solenoid keep pushing the bubble for 300 to release the scent
            servos[i].write(-10);   //   转回初识角度
            digitalWrite(LEDpin,LOW);                      //   关灯
            delay(50);  
          } 
        }
     }

   else if (Sensor2 < 20) {    // trigger a solenoid2，flower 2
        do {
        randNumber = random(3, 7); // 生成3到6之间的随机数
        } while (randNumber == 5 || randNumber == 4); // 如果随机数等于5或4，重新生成
        // Generate random numbers between 3-6 except for 4、5

        int i = randNumber;                            // 将randNumber付值给i
        int LEDpin = (pins[i][1]);                      // pin[i][1]
        Serial.println(randNumber);

         for (int i = 0; i < 3; i++) {
         if (randNumber == servoPins[i]) {
            servos[i].write(80);
            digitalWrite(LEDpin,HIGH);
            delay(300);                                     //   the solenoid keep pushing the bubble for 300 to release the scent
            servos[i].write(-10);   //   转回初识角度
            digitalWrite(LEDpin,LOW);                      //   关灯
            delay(50);  
          } 
        }
     }
    
     else if (Sensor3 < 20) {                          // trigger a solenoid3，flower 3
         do {
         randNumber = random(3, 7); // 生成3到6之间的随机数
         } while (randNumber == 6 || randNumber == 4); // 如果随机数等于6或4，重新生成
         // Generate random numbers between 3-6 except for 4、6

         int i = randNumber;                            // 将randNumber付值给i
         int LEDpin = (pins[i][1]);                      // pin[i][1]
         Serial.println(randNumber);

         for (int i = 0; i < 3; i++) {
         if (randNumber == servoPins[i]) {
            servos[i].write(80);
            digitalWrite(LEDpin,HIGH);
            delay(300);                                     //   the solenoid keep pushing the bubble for 300 to release the scent
            servos[i].write(-10);   //   转回初识角度
            digitalWrite(LEDpin,LOW);                      //   关灯
            delay(50);  
          } 
        }
     }
    
    delay(100);                             // arbitrary delay to limit data to serial port 
}
```





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



## 02  只有三朵花 CapacitiveSensor + Servo motors + LEDs最终代码
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

CapacitiveSensor   cs_7_8 = CapacitiveSensor(7,8);        // 10M resistor at Pin8, Pin7 is the input to receive the signal from the capacitive sensor
CapacitiveSensor   cs_7_9 = CapacitiveSensor(7,9);        // 10M resistor at Pin9, Pin7 is the input to receive the signal from the capacitive sensor
CapacitiveSensor   cs_7_10 = CapacitiveSensor(7,10);        // 10M resistor at Pin10, Pin7 is the input to receive the signal from the capacitive sensor

int pins[3][2] = {   // int pins【共3组数组】【每个数组中有2个数】，使用数组来对应servo和LED的针脚
 {3, 2},    // flower1 servo针脚PIN3，对应LED针脚PIN2
 {5, 4},    // flower1 servo针脚PIN5，对应LED针脚PIN4
 {6, 11},     // flower1 servo针脚PIN6，对应LED针脚PIN11
 // 3针脚对应2针脚，5针脚对应4针脚，6针脚对应11针脚
};


void setup()                    
{
   //cs_7_2.set_CS_AutocaL_Millis(0xFFFFFFFF);     // turn off autocalibrate on channel 1 - just as an example
   Serial.begin(9600);

   pinMode(8, OUTPUT); // connect solenoid1 to the pin 8, flower 1 release scent
   pinMode(9, OUTPUT); // connect solenoid2 to the pin 9, flower 2 release scent
   pinMode(10, OUTPUT); // connect solenoid3 to the pin 10, flower 3 release scent

   pinMode(2, OUTPUT);  // LED output，flower 1
   pinMode(4, OUTPUT);  // LED output，flower 2
   pinMode(11, OUTPUT);  // LED output，flower 3

}

void loop()                    
{
    randNumber = random(8, 10);    // Generate random numbers between 8-10
    Serial.println(randNumber);

    long start = millis();
    long Sensor1 =  cs_7_8.capacitiveSensor(30);
    long Sensor2 =  cs_7_9.capacitiveSensor(30);
    long Sensor3 =  cs_7_10.capacitiveSensor(30);

    Serial.print(millis() - start);        // check on performance in milliseconds
    Serial.print("\t");                    // tab character for debug windown spacing

    Serial.print(Sensor1);                  // print sensor output 1
    Serial.print("\t");
    Serial.print(Sensor2);                  // print sensor output 2
    Serial.print("\t");
    Serial.print(Sensor3);                // print sensor output 3
    Serial.print("\t");

    if (Sensor1 < 1000) {    // trigger a solenoid1，flower 1, !! "99" need to be tested!!
        do {randNumber = random(8, 10);
        } while (randNumber != 8);
        // Generate random numbers between 8-10 except for 8
           int i = randNumber;                            // 将randNumber付值给i
           int LEDpin = (pins[i][1]);                      // pin[i][1]
           Serial.println(randNumber);
           digitalWrite(i,HIGH);                          //伺服电机
           pos = 20;                                      // 设置伺服电机的目标位置为20度
           myservo.write(pos);  
           digitalWrite(LEDpin,HIGH);
           delay(50);                                     //   the solenoid keep pushing the bubble for 300 to release the scent
           pos = -10;                                     //   转回初识角度
           digitalWrite(LEDpin,LOW);                      //   关灯
    }

    else if (Sensor2 < 1000) {    // trigger a solenoid2，flower 2
        do {randNumber = random(8, 10);
        } while (randNumber != 9);
        // Generate random numbers between 8-10 except for 9
         int i = randNumber;                            // 将randNumber付值给i
         int LEDpin = (pins[i][1]);                     // pin[i][1]
         Serial.println(randNumber);
         digitalWrite(i,HIGH);                          //伺服电机
         pos = 20;                                      // 设置伺服电机的目标位置为20度
         myservo.write(pos);
         digitalWrite(LEDpin,HIGH);
         delay(50);                                     //   the solenoid keep pushing the bubble for 300 to release the scent
         pos = -10;                                     //   转回初识角度
         digitalWrite(LEDpin,LOW);                      //   关灯
    }
    
    else if (Sensor3 < 1000) {                          // trigger a solenoid3，flower 3
        do {randNumber = random(8, 10);
        } while (randNumber != 10);
        // Generate random numbers between 8-10 except for 10
         int i = randNumber;                            // 将randNumber付值给i
         int LEDpin = (pins[i][1]);                      // pin[i][1]
         Serial.println(randNumber);
         digitalWrite(i,HIGH);                          //伺服电机
         pos = 20;                                      // 设置伺服电机的目标位置为20度
         myservo.write(pos);
         digitalWrite(LEDpin,HIGH);
         delay(50);                                     //   the solenoid keep pushing the bubble for 300 to release the scent
         pos = -10;                                     //   转回初识角度
         digitalWrite(LEDpin,LOW);                      //   关灯
    }
    
    delay(50);                             // arbitrary delay to limit data to serial port 
}
```
