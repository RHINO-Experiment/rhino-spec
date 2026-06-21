RF filters and attenuators
==========================
_Filters and attenuators used in the front end, plus notes on the built-in filters in the SDRs_

Last updated: 2026-06-21

FM notch filter
---------------
A Nooelec Flamingo+ (Check: or is it Flamingo?) ([Datasheet PDF](https://www.nooelec.com/store/downloads/dl/file/id/96/product/320/flamingo_fm_filter_datasheet_revision_1.pdf)) bandstop filter is included in the frontend, to suppress the bright FM radio band. It is a passive SMA-connectorised device.

Measured S-parameters can be found listed under the `FM notch ' device in the [sparams repo](https://github.com/RHINO-Experiment/rhino-sparams/tree/main/RecBlock). According to the datasheet it is expected to provide around 70 dB suppression across most of the FM band (88 - 108 MHz), with quite a steep roll-off. This is mostly observed in the VNA measurements in the lab, using John's high-end (but wobbly...) VNA; the figure below shows the gain.

<img width="1000" height="600" alt="FMNotch3Rev" src="https://github.com/user-attachments/assets/00af9e57-f14e-4867-8c0e-00140828205d" />


Minicircuits bandpass filter
----------------------------
A Mini-circuits SBP-70+ SMA-connectorised filter is the main bandpass filter in the frontend. Measured S-parameters can also be found in the [sparams repo](https://github.com/RHINO-Experiment/rhino-sparams/tree/main/RecBlock). The plot below shows the gain, measure din the lab with John's high-end VNA.

<img width="1000" height="600" alt="BandpassFilRev3" src="https://github.com/user-attachments/assets/ce90087e-bd00-48b3-a773-e31315177abc" />

