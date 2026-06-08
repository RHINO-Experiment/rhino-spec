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
