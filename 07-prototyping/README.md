# Nature Ecosystem Between Flowers and Pollinator

## 01 Initial Ideation
**An interaction installation which imitates how flowers using volatile organic compounds(VOCs) to communicate with pollinators and other flowers**
![WechatIMG2429](https://github.com/HHY1111/PCB-class-2023/assets/144415019/d8f31dfc-cd07-4022-93f6-4dad8f01fe41)
The whole process simulates the phenomenon in nature that when pollinators such as bees are close to a flower, the flower starts to release fragrance, and the fragrance released by the flower affects the flowers around it to release fragrance at the same time, in order to increase the pollination rate.



## 02 Whatchamacallit(two hours' quick prototyping)
<img width="1473" alt="截屏2023-10-30 15 24 46" src="https://github.com/HHY1111/PCB-class-2023/assets/144415019/46129271-79e5-4314-b54a-273825f81595">
Interconnected interacting flowers, with an alcohol sensor in the first one (to replace the CO2 sensor) and a servomotor inside the second multi (to replace the fan). When blowing alcohol to the first flower, the second flower will start to rotate.

``#include <Servo.h>
Servo myServo;  // create a servo object
int pos = 0;
int ALCOHOL_sensor = 13;// MQ-6 SENSOR  
int ALCOHOL_detected;  
      void setup()  
       {  
         Serial.begin(9600);  
         pinMode(ALCOHOL_sensor, INPUT); 
          myServo.attach(12);   // attaches the servo on pin 9 to the servo object
          Serial.begin(9600);  // open a serial connection to your computer
        }  
       void loop()  
       {  
         ALCOHOL_detected = digitalRead(ALCOHOL_sensor);  
          Serial.println(ALCOHOL_detected);  
         if (ALCOHOL_detected == 1)  
         {  
           Serial.println("ALCOHOL detected..."); 
           pos = 180;
            myServo.write(pos); 
               // in steps of 1 degree
            delay(15);      
         }  
       }``


## 03 Research
The scent of a flower typically contains volatile organic compounds(VOCs) that can disperse in the air and be detected by other nearby flowers. This dispersion helps attract more pollinators because insects, butterflies, and bees often rely on scent to locate flowers. 

**Different aspects related to the impact of a flower's fragrance on surrounding flowers:** 

1. **Scent-Mediated Attraction**: When one flower emits a scent, nearby flowers may be attracted as pollinators, drawn by the fragrance of one flower, tend to continue searching for other flowers emitting similar scents, thus increasing the chances of pollination. (Some flowers will wait for pollination to approach before releasing their scent to preserve their limited perfume. They sense that pollinating insects are nearby by sensing their electrical charges.)
    
    [https://phys.org/news/2021-09-perfume-response-electricity-bee.html#:~:text=New research has found that the electrical charge,its attractive perfume—increasing its chances of being visited](https://phys.org/news/2021-09-perfume-response-electricity-bee.html#:~:text=New%20research%20has%20found%20that%20the%20electrical%20charge,its%20attractive%20perfume%E2%80%94increasing%20its%20chances%20of%20being%20visited).

![research1](https://github.com/HHY1111/PCB-class-2023/assets/144415019/d4569724-9bac-4c7e-9e80-4024003a858c)
- When a small, electrically charged hammer comes near a petunia the petunia releases a scent.

2. **Cooperative Flowers**: In certain plant species, multiple flowers may cooperate by releasing scent to attract more pollinators. This cooperation enhances overall pollination efficiency, particularly in cases where self-pollination is unfavorable. (Chemical signal is in the blend: bases of plant-pollinator encounter in a highly specialized interaction | Scientific Reports (nature.com))
   
![research2](https://github.com/HHY1111/PCB-class-2023/assets/144415019/bdb93a61-5cca-4fc2-bc99-f9b3326b01ad)
- Life cycles of male and female tree of Ficus carica (respectively on the left and right side) and Blastophaga psenes in southern France.

3. **Competing Flowers**: Some plants may compete by releasing scent to attract pollinators to their own flowers rather than those of neighboring plants. This competition helps ensure that their own flowers receive more pollination services.

- **There are many types of flowers that use VOCs to attract pollinators, and there are many types of insects that are attracted to them.**
    
    (https://www.km-bw.de/pb/site/pbs-bw-new/get/documents/MLR.LEL/PB5Documents/lvg/Versuchswesen/Zierbau/Projekte/Attractiveness%2Bof%2Bornamental%2Bflowers%2Bfor%2Bpollinating%2Binsects%2Bin%2Ban%2Burban%2Barea.pdf)
