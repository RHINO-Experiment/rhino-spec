Power supply
------------

_The power supply system for powering the various components_

Last updated: 2026-06-07

The primary power supply goes to the backend box via a mains connection (240V AC, 50 Hz), 
which has a UK mains plug going to an IEC C13 connector. The C13 input has a filter. This 
is then wired directly to a double UK wall socket in a back-box that is bolted to the base 
of the backend box.

One of the sockets is occupied by the plug for the Odroid N2+ mini-computer. The other is 
connected to a TDK-Lambda DPP240-24-1 24V DC / 10A (i.e. 240W) encapsulated switching power 
supply 
[datasheet](https://product.tdk.com/system/files/dam/doc/product/power/switching-power/ac-dc-converter/catalog/dpp120-240_e.pdf), 
which has an adjustable output voltage between 22.5 - 28.5V using a screw adjustment on 
the front. It is designed for mounting on a DIN rail.

The output is set to 28V, and passed into a custom power board soldered onto copper 
veroboard. This uses a series of linear voltage regulators to step down from 28V to 12V. 
The steps are 28 - 24V (7824 linear voltage regulator), 24 - 18V (7818), 18 - 15V (7815), 
and 15 - 12V (7812). The board has 0.33 uF capacitors on the input and output of each 
voltage regulator to help improve stability.

The 78xx chips have a minimum dropout voltage of around 2 - 2.5V and are typically rated 
for a current of 1.5A maximum. They use a TO-220 package with a small integrated heatsink 
tab, to which we have attached extruded aluminium heatsinks to improve the heat dissipation 
to a few Watts.

The main loads on the voltage regulators are two Minicircuits ZKL-2+ LNAs that draw about 
120mA at 12V each, and a 24V noise diode with a few tens of mA draw at 24V. For a total 
current draw of up to 300mA, the heat dissipation through the voltage regulators is 
(28 - 12V) x 0.3A = 4.8W. The biggest drop is from 24 - 18V, i.e. 6V x 0.3A = 1.8W. The 
12V and 24V regulated outputs are fed through a single parallel cable from the backend box 
to the frontend box.

A potential divider circuit with a high-power 16 Ohm (100W-rated) resistor and heater 
(to provide a hot calibration load) is also connected directly to the 28V supply, without 
passing through a voltage regulator. The main choice of heater is a 24V / 40W cartridge 
heater, which is run at a lower voltage to produce only about 10W of heat. The heater is 
basically a 14.4 Ohm resistor in a high-temperature stainless steel capsule. In a 16 Ohm 
potential divider fed by 28V DC, this results in 13.3V across the heater, for a power draw 
of (13.3 V)^2 / 14.4 Ohm = 12.3W.

The total current draw across the potential divider is 0.92A, for a total power draw of 
25.8W, all of which is dissipated as heat. About half of that is dissipated by the 
high-power resistor in the backend box, while the rest goes through the cartridge heater 
which is in the frontend box. The 13.3V / 0.92A output for the heater is fed through the 
parallel cable connecting the backend and frontend boxes.

The Odroid-N2+ computer is rated for up to 12V / 2A, but also powers multiple USB ports. 
One of these is connected to an Arduino Due board in the backend box, which could draw up 
to 800mA at 5V (=4W). This controls and powers various other boards in the frontend box, 
with control and power lines fed through the same parallel cable. Another is connected to 
a USB storage device (a USB3 SSD in a memory stick form factor), and another is connected 
to the SDR in the frontend box. For the RSPdx SDR, the maximum power draw is expected to 
be about 190mA at 5V, but could be higher. For the LimeSDR Mini 2.0, up to 400mA at 5V is 
the maximum expected.

The backend box is currently an enclosed metal case, with no internal airflow or heatsinks. 
It is not clear yet whether active cooling will be needed inside the case. The same is 
true of the frontend box. Both boxes will be producing tens of Watts of heat internally.

<img width="30%" alt="PXL_20260604_150919978" src="https://github.com/user-attachments/assets/dc7bffa8-127b-402c-8806-236a72182372" />
<img width="30%" alt="PXL_20260519_150711902" src="https://github.com/user-attachments/assets/e087eae3-e271-42c2-b1ef-5312e8b39002" />

