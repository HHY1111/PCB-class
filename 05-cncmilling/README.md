# CNC milling

## Step 1 - Schematic File
1. Finding the right component in the library.
2. Connect the components to each other.
3. Name the wires.(5V/GND/PinX...)
！[](Describe the assignment](https://github.com/HHY1111/PCB-class-2023/blob/main/05-cncmilling/CNC%20file%20images/SCH_Schematic1_1-P1_2023-10-05.png)
**Notes**
- SMD(surface mount components)，Components soldered directly to the board, for PCB design
  THC （Thought hole components）Components with pins to be plugged into the board
- All component specifications should be selected **1206** for its size.
- It doesn't matter if the capacitance of the capacitor is a little different （1nF≈1.1nF）
- If you can not find a suitable mF capacitance, in accordance with the formula, converted to nF
- DC connector/ power jack电池接口 (The three pins are vin, gnd and vcc.)

## Step 2 - Board File
1. Connect the components in the board file according to the schematic file and the blue line.
2. 
![](https://github.com/HHY1111/PCB-class-2023/blob/main/05-cncmilling/CNC%20file%20images/截屏2023-10-05%2022.01.50.png)
**Notes**
-Check if the solder joints are not too close together or too small to be soldered
（ You can change the size of the solder joints in the schematic diagram motor components, click on the right side of the package“ ...” three small dots, click on the black small figure above the“ ✏️”icon）
- The shape of the board can be changed by importing a DXF file. (draw with Rhino)
- The wire for the power（5V） supply needs to be thicker.
- The drill size for cutting the outer edge is 1/32 inch (0.8mm) and the drill size for milling the inner point line is 1/64 inch (0.4mm).
  So set the safety distance according to this

