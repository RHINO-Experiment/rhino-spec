Calibration loads
=================
_Sources used to provide calibration references_

Last updated: 2026-06-07

Heated termination (cartridge heater)
-------------------------------------
A 50 Ohm termination with an SMA connector is inserted into a small aluminium block, 
roughly 4.5cm on each side. A snugly-fitting hole has been drilled into one face of 
the block for the termination, with another, smaller, hole for a Pt-1000 thermistor 
next to it. Next to this is another hole that fits a cartridge heater with max. 40W 
power output at 24V DC. This is essentially a 14.4 Ohm resistor, which can be 
powered at a lower voltage to reduce the power output. The cartridge heater gets 
red hot if used at maximum power. It is of the kind used for 3D printers.

The aluminium block is contained within a diecast metal box with an SMA connector, 
and power and thermistor input holes on the front. The block rests on about 1 inch 
thick glass fibre insulation with foil backing (foil facing the outside of the box). 
The block is loosely covered by the insulation on all sides. The wires poke through 
a gap in the strips of insulation. We have tested it to about 150 deg C and the 
glass fibre insulation seems essentially unaffected by the heat.

The box is closed with bolts at the top. The aluminium block gets very hot during 
operation, and must not be touched - it will boil water drops on contact.

<img width="25%" alt="1000077903" src="https://github.com/user-attachments/assets/021c5307-f1b8-42fd-b304-932229162d88" />
<img width="25%" alt="1000077906" src="https://github.com/user-attachments/assets/4c673915-d95e-4375-ba34-4538f42a1ecf" />
<img width="25%" alt="1000078806" src="https://github.com/user-attachments/assets/9cfa2002-428c-463e-b291-381131fe834b" />
<img width="25%" alt="1000078807" src="https://github.com/user-attachments/assets/71fb35b5-20d7-464d-9f90-cd762a54b85e" />

Heated termination (PTC heater)
-------------------------------
Similar to the above but using a PTC thermistor heater pad instead. This self-
regulates its temperature.

Currently on 5 V supply with maximum current draw of 1 A

Noise diode
-----------
Prior to 2026/08/25 the noise diode being used (silver) had the following ENR spectrum.

<img width="25%" alt="10000788015" src="https://github.com/user-attachments/assets/1a411173-daa1-4180-a30e-1444bc138461" />
It has since been replaced with a new noise-diode (blue) with the following ENR spectrum.

<img width="25%" alt="10000788156" src="https://github.com/user-attachments/assets/4d43d244-7f9e-430f-84cd-f9d06247428c" />


Current Draw: 4 mA

BNC Connection and SMA output.

Reflection (VNA) calibrators
----------------------------
A SOLT kit that came with the NanoVNA.

Long cable with an open and short on the end of SPDT switch for delay.
