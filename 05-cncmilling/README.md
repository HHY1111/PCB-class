# CNC milling

## Step 1 - Schematic File
1. Finding the right component in the library.
2. Connect the components to each other.
3. Name the wires.(5V/GND/PinX...)
![](https://github.com/HHY1111/PCB-class-2023/blob/main/05-cncmilling/CNC%20file%20images/SCH_Schematic1_1-P1_2023-10-05.png)

**Notes**

- SMD(surface mount components)，Components soldered directly to the board, for PCB design
  THC （Thought hole components）Components with pins to be plugged into the board
- All component specifications should be selected **1206** for its size.
- It doesn't matter if the capacitance of the capacitor is a little different （1nF≈1.1nF）
- If you can not find a suitable mF capacitance, in accordance with the formula, converted to nF
- DC connector/ power jack电池接口 (The three pins are vin, gnd and vcc.)

## Step 2 - Board File
1. Connect the components in the board file according to the schematic file and the blue line.
2. Modify line thickness
3. Check for proper connection
4. Changing the Outline Shape
![](https://github.com/HHY1111/PCB-class-2023/blob/main/05-cncmilling/CNC%20file%20images/截屏2023-10-05%2022.01.50.png)


## Step 3 - Exporting layers
1. Exporting the file from Jialichuang Platform as pdf
2. Editing the file in illustrator. (The black part is the part to be milled, the white part is not.)
3. Exporting 3 Layers as a wire PNG, a hole PNG and the outline PNG
<img width="347" alt="截屏2023-10-30 16 21 24" src="https://github.com/HHY1111/PCB-class-2023/assets/144415019/3e251eb7-4436-429a-bd77-67b1907b8282">

## Step 4 - Generating CNC files
[1. check if size of the PNG in modsporject is the same as the one in the Jialichuang EDA!
2. ](http://modsproject.org（program-roland-SRM20-PCB）
1. Exporting the file from Jialichuang Platform as pdf
2. Set the mill raster 2D, make sure the cut depth is thicker than the copper to cut through the copper (0.15mm)
3. Set the speed of the mill, and set the jog height of the mill(The depth of the cut-through is different from the depth of the non-cut-through！)
4. Open saving to file, and close connect to laptop
5. Click “calculate” and check the movement of the drill bit.（If there is a cut-through path, it will be cut around in several layers）
<img width="2046" alt="截屏2023-10-14 00 40 00" src="https://github.com/HHY1111/PCB-class-2023/assets/144415019/c73d3af6-0c21-417f-9a0a-35d0084e0f9f">


## Step 5 - CNC milling & finishing the board
1. Cut the wire first（1/64bit）, then the holes（1/32bit）, and finally the outer contour（1/32bit）.
2. Calculate locations to maximize material savings
3. After cutting, carefully pry up the PCB with a tool and polish it with a hobby knife and iron cotton to prevent inter-wire connections.
![WechatIMG2427](https://github.com/HHY1111/PCB-class-2023/assets/144415019/935b98a6-e3f1-4edd-a548-1bed0241f495)
![WechatIMG2428](https://github.com/HHY1111/PCB-class-2023/assets/144415019/8ca6af3a-d439-45ec-b3fa-51b94f97f742)
![WechatIMG2423](https://github.com/HHY1111/PCB-class-2023/assets/144415019/14c2c9af-fa58-47b7-8fd5-62501e33c54d)

## Step 6 - Solding components
1. go in with the solder iron (wait for 3 seconds)
2. go in with the solder wire (wait for 3 seconds)
3. stay the solder (wait for 3 seconds)
4. leave the solder iron
**good soldering looks like a shiny volcano**
![WechatIMG2420](https://github.com/HHY1111/PCB-class-2023/assets/144415019/6cb63d6f-cb08-4607-a113-aec2085d4cd2)
![WechatIMG2421](https://github.com/HHY1111/PCB-class-2023/assets/144415019/51cd881c-1991-40f3-a728-d33fa7ea70ee)

## Step 7 - Testing
![WechatIMG2419](https://github.com/HHY1111/PCB-class-2023/assets/144415019/b55745a6-f05e-4ffd-9fd6-b918c43c0e80)


**Notes**

- Check if the solder joints are not too close together or too small to be soldered
（ You can change the size of the solder joints in the schematic diagram motor components, click on the right side of the package“ ...” three small dots, click on the black small figure above the“ ✏️”icon）
- The shape of the board can be changed by importing a DXF file. (draw with Rhino)
- The wire for the power（5V） supply needs to be thicker.
- The drill size for cutting the outer edge is 1/32 inch (0.8mm) and the drill size for milling the inner point line is 1/64 inch (0.4mm).
  So set the safety distance according to this
