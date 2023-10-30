# Actuators


## 01 Servo motor
![WechatIMG2430](https://github.com/HHY1111/PCB-class-2023/assets/144415019/092c61cd-85c1-4806-ba49-d18b9dd78ef8)
- The three wires of the servo motor correspond to the following pins.
```
#include <Servo.h>

Servo myServo;  // create a servo object

int const potPin = A0;  // analog pin used to connect the potentiometer
int potVal;             // variable to read the value from the analog pin
int angle;              // variable to hold the angle for the servo motor

void setup() {
  myServo.attach(9);   // attaches the servo on pin 9 to the servo object
  Serial.begin(9600);  // open a serial connection to your computer
}

void loop() {
  potVal = analogRead(potPin);  // read the value of the potentiometer
  // print out the value to the Serial Monitor
  Serial.print("potVal: ");
  Serial.print(potVal);

  // scale the numbers from the pot
  angle = map(potVal, 0, 1023, 0, 179);

  // print out the angle for the servo motor
  Serial.print(", angle: ");
  Serial.println(angle);

  // set the servo position
  myServo.write(angle);

  // wait for the servo to get there
  delay(15);
}
```



## 02 LED display screen
- LiquidCrystal I2C is an LED screen with 16 chars (0-15) and 2 lines (0-1).
- 
![WechatIMG2431](https://github.com/HHY1111/PCB-class-2023/assets/144415019/740854e2-f2a1-455e-8a99-227a9a7dc043)
![WechatIMG2432](https://github.com/HHY1111/PCB-class-2023/assets/144415019/bd0d6b8b-9074-4529-950e-8501219cbda7)
···
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,20,4);  // set the LCD address to 0x27 for a 16 chars and 2 line display

void setup()
{
  lcd.init();                      // initialize the lcd 
  lcd.init();
  // Print a message to the LCD.
  lcd.backlight();                // Turn on lcd backlight
  lcd.setCursor(3,0);             // Turn on lcd backlight
  lcd.print("Hello, world!");
  lcd.setCursor(2,1);
  lcd.print("Ywrobot Arduino!");
   lcd.setCursor(0,2);
  lcd.print("Arduino LCM IIC 2004");
   lcd.setCursor(2,3);
  lcd.print("Power By Ec-yuan!");
}


void loop()
{
}
···
