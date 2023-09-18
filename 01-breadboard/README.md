# Building an Arduino on a Breadboard

This document documents how to build an Arduino board on a breadboard.

## Basic Parts for wiring up Arduino

1. A breadboard
2. 22 AWG wire
3. 7805 Voltage regulator
4. 2 LEDs
5. 2 220 Ohm resistors
6. 1 10k Ohm resistor
7. 2 10 uF capacitors
8. 16 MHz clock crystal
9. 2 22 pF capacitors
10. Atmega Chip

## Circuitry in the breadboard
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/1.jpeg)
The holes in the center of the breadboard are connected vertically and the sides of the notch are not connected. Positive and negative power connectors on both sides, connected vertically.

## ****wiring up Arduino****

1. Add power and ground wires.
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/2.jpeg)

2. 添加 7805 电源调节器和为电路板供电的线路，并在两端各添加一个电容器。
   Add the 7805 power regulator and the lines to power the board and add a capacitor at each end.
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/3.jpeg)

**Voyage regulator 稳压器** 
The role of the voltage regulator is to adjust the voltage to ensure the smoothness of the circuit and the normal use of electrical appliances稳压器的作用是调整电压，保证电路的通畅和电器的正常使用）

**Capacitor 电容**
Capacitors are similar to batteries in that they can store charge and release charge to absorb excess charge in a circuit and replenish deficiencies, and the voltage will be more stable after going through a capacitor.
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/3.1.jpeg)
黑色的方盒是电容的正面，金属是背面，三根针脚分别是电流进入，接地和电流出。
The black square box is the front of the capacitor, the metal is the back, and the three pins are current in, ground and current out.
电容分别接在稳定器的电压进入、接地和电压出、接地针脚上。
The capacitors are connected to the voltage in, ground and voltage out, ground pins of the stabilizer.

3. Add the ATMEGA 168 in the middle of the board
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/4.jpeg)
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/4.1.png)
Each pin on the ATMEGA has a different meaning, the ones on the Arduino are simplified versions of the numbers
ATMEGA上的每一个针脚都有不同的意义，Arduino上的是编号简化过的版本

4. Inserting a crystal on the two crystal pins of the ATMEGA and add capacitors on both sides of it to make the crystal more accurate
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/5.jpeg)
** Crystal 晶振**
A crystal oscillator is a resonant device that utilizes the piezoelectric effect of quartz crystals, which uses the mechanical resonance of the vibrating crystals of the piezoelectric material to generate electrical signals with a very accurate frequency.
石英晶体振荡器是利用石英晶体的压电效应制成的一种谐振器件，它利用压电材料的振动晶体的机械共振来产生具有非常精确频率的电信号

5. Add an LED on pin 13
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/6.jpeg)

6. Connect an LED in parallel with a resistor in the circuit to test if the circuit is successfully energized
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/7.jpeg)

## adding the USB
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/8.jpeg)
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/9.jpeg)
![](https://github.com/HHY1111/PCB-class-2023/blob/main/01-breadboard/images-breadboard/10.jpeg)
-GND-GND
-VCC-5V
-TX-RX
-RX-TX
-DTR-RESET

## coding

1. Define variable

``

```
int Scale = 0;
int inputvalue = 0;
```

1. Defines whether the mode of the pin is input or output in ``void setup()`` 

```
void setup() {
  pinMode(9, OUTPUT);
  pinMode(10, INPUT);
```

1. Enter the instructions to be executed in a loop in void loop()

```
void loop() {
  inputvalue = digitalRead(10);
if(inputvalue ==1){
  digitalWrite(13,HIGH);
  Serial.println("On");}
  else{
    digitalWrite(13,LOW);
    Serial.println("Off");}
```

- pinMode(9, output);
- 定义9号引脚为输出信号

- digitalWrite(13, HIGH);
   定义13号针脚高电平1/定义低电平0，控制小灯的开关
    
- digitalRead(10);
 读取针脚10的数据
    

- analogWrite();
- analogRead();
 PWM模拟值，区别于digital的只有非黑即白的0/1，analog可以从0-255以调整小灯的亮度
    

- Serial.begin(9600);
以9600的频率向电脑发送信息，这段命令要写在void setup();里
    
- Serial.println(’’word’’);
串口监视器换行显示
    
- Serial.print(“word”);
串口监视器不换行显示
    

- delay(20);
延迟20毫秒

