Data acquisition
================
_The software for acquiring data from the SDR, channelising/averaging, and storing the data_

Last updated: 2026-06-08

The rhino-daq code uses the Soapy SDR interface via Python to control the SDR acquire raw IQ data. It then channelises using an FFT and stores the data in a HDF5 file along with metadata and sensor readings from an Arduino Due.
