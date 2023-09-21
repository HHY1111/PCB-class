# 03-Sensors

## 1. DHT11 Temperature and Humidity Sensor
(analogy)
The DHT11 is a common low-cost temperature and humidity sensor that can measure temperatures from 0°C to 50°C and relative humidity from 20-90%.
### Connection
![The pins of the DHT11 Sensor](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/1.jpg)

![Connect the signal pin to digital pin 2 and the other two pins to VCC and GND.
](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/2.jpg)

### Coding
The library ** <DHT.h>** needs to be included when using DHT11 Sensor
```
#include <DHT.h>//

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
![Room temperature and humidity](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/4.jpeg)

![Temperature and humidity both elevated when holding the sensor with a wet hand](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/5.jpeg)

![Temperature and humidity will be changed accordingly in the serial monitor
](https://github.com/HHY1111/PCB-class-2023/blob/main/03-sensors/DHT11%20Temperature%20and%20Humidity%20Sensor-photos/temperature%20and%20humidity%20sensor/3.png)

### Reference
Arduino开发板传感器模块——温湿度传感器模块篇——DHT11/DHT22以及DHT11/DHT22之间的对比与选择。
https://zhuanlan.zhihu.com/p/636814848

## 2. Optical Sensor
(digital)
