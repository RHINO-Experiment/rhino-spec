# Power supply

_The power supply system for powering the various components_

Last updated: 2026-06-20

The primary power supply goes to the backend box via a mains connection (240V AC, 50 Hz), 
which has a UK mains plug going to an IEC C13 connector. The C13 input has a filter. This 
is then wired directly to a double UK wall socket in a back-box that is bolted to the base 
of the backend box.

The backend box is currently an enclosed metal case, with no internal airflow or heatsinks. 
It is not clear yet whether active cooling will be needed inside the case. The same is 
true of the frontend box. Both boxes will be producing tens of Watts of heat internally.

## Power requirements

Some of these are estimated from datasheets. The Odroid in particular needs to be tested 
under different load conditions to establish more accurate values.

* (24V DC / 5 mA) Noise diode with a few tens of mA draw at 24V.
* (24V DC / 800 mA) Cartridge heater (14.4 Ohm) plus power resistor in potential divider
* (12V DC / 120 mA) Minicircuits ZKL-2+ LNAs (x2)
* (12V DC / 1200 mA max.) Odroid mini-computer with USB devices (estimated max. load of
  about 1.2 A, but could spike slightly at start-up)
  * (5V DC / 200 mA max.) RSPdx SDR via USB 3 interface
  * (5V DC / 150 mA max.) Arduino Due control board via USB interface (this powers a
    number of small sensors and other devices)
  * (5V DC / 900 mA max.) SSD USB 3 memory stick, estimated peak power draw

For the RSPdx SDR, the maximum power draw is expected to be about 190mA at 5V, but 
could be higher. For the LimeSDR Mini 2.0, up to 400mA at 5V is the maximum expected.

## Power distribution board

There is a custom-made power distribution board, soldered onto copper veroboard using 
through-hole components. The input is from a 240V AC to 24V DC linear power supply, 
rated up to 2.2 A output (TBC). There are three outputs:

 1. 12V DC, current <300 mA, for the 2x LNAs
 1. 12V DC, current up to 1400 mA, for the Odroid and attached devices
 1. 24V DC, direct from the linear power supply, for the noise diode and heater

The 12V and 24V regulated outputs are fed through a single parallel cable from the 
backend box to the frontend box. 

**Linear power supply:** The input from the power supply has a large electrolytic 
capacitor across it, and then splits into the three output paths. The power supply 
has an open case, over which we have bolted a custom cover made of expanded mesh bent 
into shape, and attached with bolts with a few mm standoff from the live components. 

**THIS COMPONENT IS DANGEROUS** 
and must not be handled without assistance. In particular, watch out for remaining 
charge in the large capacitors; it is best to keep a resistor connected across the 
output terminals to discharge these while working on the power supply. The power supply 
is connected to the mains via a normal UK 3-pin plug, with a fuse rated for 1A (but 
would ideally be replaced with a 0.75A slow-blow fuse, as per the datasheet). There 
are adjustment screws on the power supply board to tune the output voltage as well 
as the output current limit; the top has fallen off the voltage one, but can still 
be adjusted with a screwdriver.

**Output (1):** The first 12V output has a series of linear voltage regulators, a 
7818, 7815, and 7812. Each has a tantalum capacitor (0.33 uF, TBC) across its output 
to help reduce oscillations and to generally stabilise the output. The 78xx chips 
have a minimum dropout voltage of around 2 - 2.5V and are typically rated for a 
current of 1.5A maximum. They use a TO-220 package with a small integrated heatsink 
tab, to which we have attached extruded aluminium heatsinks to improve the heat 
dissipation to a few Watts. Note that the heatsink on the regulators is connected 
to the ground pin, and we have not isolated them. The anticipated voltage drops are 
6V, 3V, and 3V across the regulators, which means the brunt of the heat dissipation 
is through the first. For a peak load of 300 mA from 2x LNAs, this is 1.8 W, which 
should be comfortable with the aluminium heatsink attached. A TVS diode should be 
included to protect the LNAs from voltage spikes.

**Output (2):** This follows a similar design to Output (1), but has an initial LM317 
adjustable voltage regulator at the front. This is designed to step down 24V to 
about 21V before going into another chain of 7818 / 7815 / 7812 regulators. This also 
has an extruded aluminium heatsink attached, but has a nylon isolator grommet on the 
bolt that attaches the heatsink to the TO-220 package. This is because the pinout of 
the LM317 is different to the 78xx series regulators; the integrated heatsink is 
attached to the output pin! A voltage divider connects the output and adjust pins 
(there is no ground pin), and uses the equation $V_{\rm out} = 1.25 V (1 + R_2 / R_1)$, 
where R1 is the resistor across $V_{\rm out}$ and $V_{\rm adj}$ and R2 is across 
$V_{\rm adj}$ and ground. For an output of 21V, we use R1 = 100 Ohm and R2 = 1 kOhm + 
470 Ohm + 100 Ohm = 1570 Ohm.

The total voltage drop across each regulator should then be about 3V, which for a peak 
current of 1.4 A gives 4.2W per regulator. This means that they will run very hot, 
but the extra heatsinks are hopefully enough. Testing in a closed box environment will 
help establish whether passive cooling is enough; otherwise we will need a small DC fan 
and ventilation holes in the box. A TVS diode should be included to protect the Odroid 
from voltage spikes in case of the voltage regulators failing.

**Output (3):** This has no voltage regulators as the total current drawn will be large. 
We are relying on the smoothness of the linear power supply output to keep the noise 
diode stable, but this probably needs to be revisited. The heater is attached via a 
potential divider with a power resistor capable of dissipating 100 W. It is not attached 
yet, but it would be useful to connect these components via a MOSFET that can be 
controlled by the Arduino. This would allow switching the heater on and off for safety. 
It would also allow use of PWM to adjust the heater voltage and control its temperature, 
although would introduce a new source of EMI.


## Older switched-mode version (pre-June 2026)

One of the power sockets is occupied by the plug (switched-mode power supply) for the 
Odroid N2+ mini-computer. The other is connected to a TDK-Lambda DPP240-24-1 24V DC / 10A 
(i.e. 240W) encapsulated switching power supply 
[datasheet](https://product.tdk.com/system/files/dam/doc/product/power/switching-power/ac-dc-converter/catalog/dpp120-240_e.pdf), 
which has an adjustable output voltage between 22.5 - 28.5V using a screw adjustment on 
the front. It is designed for mounting on a DIN rail.

The output is set to 28V, and passed into a custom power board soldered onto copper 
veroboard. This uses a series of linear voltage regulators to step down from 28V to 12V. 
The steps are 28 - 24V (7824 linear voltage regulator), 24 - 18V (7818), 18 - 15V (7815), 
and 15 - 12V (7812). The board has 0.33 uF capacitors on the input and output of each 
voltage regulator to help improve stability.

<img width="30%" alt="PXL_20260604_150919978" src="https://github.com/user-attachments/assets/dc7bffa8-127b-402c-8806-236a72182372" />
<img width="30%" alt="PXL_20260519_150711902" src="https://github.com/user-attachments/assets/e087eae3-e271-42c2-b1ef-5312e8b39002" />
<img width="30%" alt="1000079220" src="https://github.com/user-attachments/assets/decf4c83-ef44-47ad-b339-6419818a3920" />
<img width="30%" alt="1000079410" src="https://github.com/user-attachments/assets/9e71c5a4-f9a4-4d4a-8f1e-babe30ecc4cd" />



