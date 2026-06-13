Control cable and board
=======================
_The Arduino control board and parallel cable connecting the frontend and backend boxes with power and control signals_

Last updated: 2026-06-13

We use an Arduino Due board [(Datasheet PDF)](https://docs.arduino.cc/resources/datasheets/A000062-datasheet.pdf) for control. It is powered via a USB connection to the Odroid N2+ computer, which also permits serial communication with the board. The board itself has 54 IO pins and an 84 MHz 32-bit processor. There are 12 analogie pins and 2 DAC pins. It also supports SPIO, which is useful for some of the other control boards. Note that the Arduino is suspected to contribute to EMI, potentially transmitted over the data lines.

There is a 25-pin D-SUB (DB25) cable connecting the frontend and backend boxes. It is intended to be a shielded cable for carrying power, control, and monitoring signals only, primarily to interface the Arduino Due control board with other devices.

Both boxes have DB25 to screw terminal block boards, allowing control wires to be attached arbitrarily to different pins. The below diagram shows the current pin assignments.
The particular model of terminal block that we are using is from [Amazon](https://www.amazon.co.uk/dp/B0D1QT87CC), purchased in March 2026, and does not have a datasheet. Typical connectors are rated for 1A or so per pin (typically 2-3A per pin) however.

<img width="80%" alt="Pin assignments for the 25-pin D-SUB cable" src="https://github.com/user-attachments/assets/f10eb6ad-a43c-4cd7-8787-b3267d0387dc" />
