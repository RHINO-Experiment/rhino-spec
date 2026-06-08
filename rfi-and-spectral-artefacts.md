RFI and spectral artefacts
==========================
_A "bestiary" of observed RFI, EMI, and other spectral artefactss that have been observed, along with notes on solutions and diagnostics_

Last updated: 2026-06-08

Template report
---------------
 * **Observed:** 2026-06-08
 * **Reporter:** Joe Bloggs
 * **Receiver config:** RSPdx SDR with LNAs switched on/off.
 * **Other config notes:** Frontend box was open.

Description and further notes and plots.

EMI Through Temperature-Switch Circuit Contact
---------------
 * **Observed:** 2026-05-12
 * **Reporter:** Jordan Norris
 * **Receiver config:** RSPdx SDR with full set up.
 * **Other config notes:** Thermistors in contact with SP8T switch. Temp/Switch Circuits in contact with long cable box.

<img width="50%" alt="Note broader band EMI across the spectrum in multiple locations and across calibrators"
     src="https://github.com/user-attachments/assets/d3e46d7e-5263-4bc2-bd80-562026415f65" />

It was found that EMI was leaking into the RF chain through the thermistors as well as contact with the
long cable box and the switch/temperature sensor circuitry.

This was rectified with the placement of insulating material between the circuits and thermistors. See
plot below for the spectra post-fix.

<img width="50%" alt="Spectra of calibrators after adding insulating material. Note the difference in the EMI regions."
     src="https://github.com/user-attachments/assets/25cf6b8b-d723-4e2d-844b-58c509326326" />



Persistent strong and narrow 72 MHz line (RSPdx clock)
------------------------------------------------------
 * **Observed:** Spring 2026
 * **Reporter:** Jordan Norris / Phil Bull
 * **Receiver config:** RSPdx SDR tuned to around 70 MHz
 * **Other config notes:** Any config.

A strong and relatively narrow 72 MHz line is seen persistently with the RSPdx. The internal clock 
frequency is 24 MHz, and 72 = 3 x 24 MHz, so we suspect that this is the clock leaking. There is 
not much that can be done about this. It appears to cause higher-order products at high gain 
settings.


Harmonics around 72 MHz with 400 kHz spacing (Arduino associated)
-----------------------------------------------------------------
 * **Observed:** 2026-06-08
 * **Reporter:** Jordan Norris
 * **Receiver config:** RSPdx SDR with LNAs switched off.
 * **Other config notes:** Arduino switched on and powered via USB to Odroid, but cables not plugged in.

Arduino is leaking a harmonic with 0.4 MHz spacing at quite low level across the band which is most 
noticeable from 70.8 - 72.5 MHz. Plot shows with and without the Arduino plugged in (this is without 
the amplifiers turned on). This may be coming through on the SDR level or after the amplifiers because 
as soon as the amplifiers are turned on it is washed out with noise power and then takes a long 
integration time to reveal it again.

Doing some quick tests I don't think its even leaking through the front-end box. I disconnected the 
D-sub (which has all the arduino connections on) and it still comes through at the same amplitude. I 
suspect its coming over the SDR usb line from the USB hub.

<img width="50%" alt="Note harmonics around 72 MHz. These go away in the bottom part of the waterfall when the Arduino is switched off." 
     src="https://github.com/user-attachments/assets/849120a9-e11c-4c1f-b08f-f36d47b9ae36" />
