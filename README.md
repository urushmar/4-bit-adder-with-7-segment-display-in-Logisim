# 4-bit Adder with 7-Segment Display

A 4-bit binary adder built from basic logic gates in Logisim, with the sum shown on a 7-segment display through a decoder I designed with Karnaugh maps.
## full circuit

<img width="1003" height="400" alt="image" src="https://github.com/user-attachments/assets/4e90560b-8645-43a4-a51e-344b68eabf6b" />

## How it's built
The design is built bottom-up, with each circuit used inside the next one:
## Half adder:
adds two bits. XOR gives the sum, AND gives the carry. 

<img width="478" height="261" alt="image" src="https://github.com/user-attachments/assets/c3e8e403-2095-4bb7-9cd9-577015601c44" />

## Full adder: 
two half adders and an OR gate, so it can also add a carry-in.

<img width="877" height="317" alt="image" src="https://github.com/user-attachments/assets/574523cd-efc3-43b4-b9f8-3e0d35e832ea" />

## 4-bit adder:
four full adders chained together, with each carry-out feeding the next carry-in (ripple carry).

<img width="633" height="618" alt="image" src="https://github.com/user-attachments/assets/42bca868-f4ee-44c8-92ef-e275247c51df" />

## 7-segment decoder:
turns the 4-bit sum into signals for segments a–g. I wrote a truth table for each segment and simplified it with a Karnaugh map, using inputs 10–15 as don't-cares to get shorter expressions. 

<img width="528" height="958" alt="image" src="https://github.com/user-attachments/assets/0f385660-35a5-4b5a-8c54-3e607f216a46" />

```
a = ~i2⋅~i0 + i3 + i1 + i0⋅i2
b = ~i0⋅~i1 + i0⋅i1 + ~i2
c = ~i1 + i0 + i2
d = ~i2⋅~i0 + i2⋅i0⋅~i1 + i3 + i1⋅~i0 + i1⋅~i2⋅~i3
e = ~i2⋅~i0 + i1⋅~i0
f = i2⋅~i0 + ~i1⋅i2 + ~i0⋅~i1 + i3
g = i2⋅~i1 + i3 + i1⋅~i0 + i1⋅~i2
```

## Limitations
The decoder is designed for digits 0–9, so sums from 10 to 15 show undefined patterns. The carry-out is not connected to the display.

## Running on hardware
The circuit was also implemented on a Digilent Basys 3 FPGA board (Xilinx Artix-7). Logisim-evolution generated the HDL and the inputs were mapped to the board's slide switches, with the result shown on its 7-segment display.

## How to run
Open 4bit-adder-7segment.circ in Logisim-evolution (v3.9.0). bonus is the main circuit. Use the Poke tool to toggle the input pins and watch the display
