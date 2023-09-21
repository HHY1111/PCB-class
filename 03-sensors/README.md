# 03-Sensors

# 1. DHT11 Temperature and Humidity Sensor
(analogy)
The DHT11 is a common low-cost temperature and humidity sensor that can measure temperatures from 0°C to 50°C and relative humidity from 20-90%.
### Connection
The pins of the DHT11 Sensor
![The pins of the DHT11 Sensor](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/1.jpg)

Connect the signal pin to digital pin 2 and the other two pins to VCC and GND.
![Connect the signal pin to digital pin 2 and the other two pins to VCC and GND.
](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/2.jpg)

### Coding
The library ** <DHT.h>** needs to be included when using DHT11 Sensor
```
#include <DHT.h>//调用DHT库

#define DHTPIN 2          //连接到Arduino的数字输入引脚
#define DHTTYPE DHT11     //使用DHT11温湿度传感器

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  delay(2000);
  
  float humidity = dht.readHumidity();     //读取湿度数据
  float temperature = dht.readTemperature();   //读取温度数据，单位为摄氏度

  Serial.print("湿度：");
  Serial.print(humidity);
  Serial.print("%，  温度：");
  Serial.print(temperature);
  Serial.print(" ℃\n");
}
```
Room temperature and humidity
![Room temperature and humidity](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/4.jpeg)

Temperature and humidity both elevated when holding the sensor with a wet hand
![Temperature and humidity both elevated when holding the sensor with a wet hand](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/5.jpeg)

Temperature and humidity will be changed accordingly in the serial monitor
![Temperature and humidity will be changed accordingly in the serial monitor
](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/3.png)

### Reference
Arduino开发板传感器模块——温湿度传感器模块篇——DHT11/DHT22以及DHT11/DHT22之间的对比与选择。
https://zhuanlan.zhihu.com/p/636814848

# 2. Optical Sensor
(digital)
An optical sensor converts light rays into electronic signals. It measures the physical quantity of light and then translates it into a form that is readable by an instrument.

## Connection
The pins of the optical sensor
![](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/optical%20sensor_photos/optical1.jpeg)

Connect the Signal pin to the digital pin 2, connect VCC to VCC and GND to GND.
![[(https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/optical%20sensor_photos/optical3.jpg)

## Testing
In normal conditions,the light is on, the optical sensor, showing "0" in the serial monitor
![In normal conditions the optical sensor show "1" in the serial monitor](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/optical%20sensor_photos/optical1.jpeg)

When putting a finger between the optical sensor,the light is off, showing "1" in the serial monitor.
![](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/optical%20sensor_photos/optical2.jpg)


## Coding
```
int opticalvalue = 0;
void setup() {
  pinMode(2,INPUT);
  Serial.begin(9600);
}
void loop() {
  opticalvalue=digitalRead(2);
  Serial.println(opticalvalue);
  delay(50);
}
```
