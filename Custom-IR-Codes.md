# Adding Custom IR Codes

1. Open `general.h` in your favourite text editor
2. make a copy of any IR code set and paste it, iterating the parameter `IR_BUTTON_SET`
3. Use [IRrecvDumpV2](https://github.com/markszabo/IRremoteESP8266/tree/master/examples/IRrecvDumpV2) to get IR Codes , You'd get something like this :
`Timestamp : 002222.937
Encoding : NEC
Code : FFE01F (32 bits)
Library : v2.3.2

Raw Timing[71]:

10816, - 4494, + 674, - 572, + 674, - 572, + 672, - 572,
672, - 572, + 672, - 600, + 646, - 572, + 672, - 572,
672, - 572, + 676, - 1678, + 668, - 1680, + 666, - 1708,
644, - 1682, + 670, - 1682, + 672, - 1680, + 678, - 1682,
674, - 1682, + 676, - 1704, + 658, - 1680, + 682, - 1682,
686, - 574, + 684, - 574, + 682, - 574, + 744, - 518,
670, - 570, + 668, - 570, + 672, - 572, + 676, - 572,
676, - 1678, + 678, - 1680, + 676, - 1680, + 676, - 1680,
680, - 1682, + 746, - 40008, + 10806, - 2228, + 668
uint16_t rawData[71] = {10816, 4494, 674, 572, 674, 572, 672, 572, 672, 572, 672, 600, 646, 572, 672, 572, 672, 572, 676, 1678, 668, 1680, 666, 1708, 644, 1682, 670, 1682, 672, 1680, 678, 1682, 674, 1682, 676, 1704, 658, 1680, 682, 1682, 686, 574, 684, 574, 682, 574, 744, 518, 670, 570, 668, 570, 672, 572, 676, 572, 676, 1678, 678, 1680, 676, 1680, 676, 1680, 680, 1682, 746, >40008, 10806, 2228, 668}; // NEC FFE01F
uint32_t address = 0x0;
uint32_t command = 0x7;
uint64_t data = 0xFFE01F;`

the **uint64_t data** value is useful to us. 
5. Change `IR_BUTTON_COUNT` to number of buttons defined
4. replace the codes inside the new IR codes set you created 
![Screenshot](https://thumb.ibb.co/kfC0B7/Screenshot_from_2018_05_02_13_49_28.png)

5. change the `IR_BUTTON_SET' of the board of your choice in `hardware.h` 
![Screenshot](https://thumb.ibb.co/mJCdyn/Screenshot_from_2018_05_02_13_49_59.png)

6. Done! 

