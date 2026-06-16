Data acquisition
================
_The software for acquiring data from the SDR, Arduino Due, and storing the data_

Last updated: 2026-06-16

The rhino-daq code uses the Soapy SDR interface via Python to control the SDR acquire raw IQ data. It then channelises using an FFT/PFB and stores the data in a HDF5 file along with metadata and sensor readings from an Arduino Due.

Observation settings regarding the hardware are edited in the [obs_config.yaml](https://github.com/RHINO-Experiment/rhino-daq/blob/main/obs_config.yaml) prior to observations.

This is split into several groups regarding each piece of hardware.

## observationParams

runLength: Length of an observation block in seconds.

obsCachePath: Directory of the obervation cache for .npy files prior to saving to .hdf5

dataDirectory: Directory of the final .hdf5 files with all associated observational data.

optimisedObserving: Bool for enabling fractional observing (currently not implemented, defaults to equal time between Dicke sources)

customName: Custom name for the observation. Defaults to the end time of the observation in the format; YYYY-MM-DD_HH-mm-SS_obs.hdf5

## sdr:
active: bool for enabling (for the case where the auxiliary SDR is used.

centreFrequency: Centre frequency of the LO in Hz.

bandwidth:  Bandwidth / IQ Sample rate of the ADCs in the SDR 

nChannels: Total Number of channels.

sdrDriver: SoapySDR driver label.

sdrLabel: SDR label in SoapySDR.

sdrId: SDR ID, found in SoapySDR.

sampleIntegrationTime: Total integration time per output spectra. (Seconds)

delay: Delay before SDR starts capture. (Seconds)

sdrRFGR: SDR RF gain reduction. Amount of attenuation applied to the SDR amplified signal prior to mixing (dB)

sdrIFGR: SDR IF gain reduction. Amount of attenuation applied to the SDR amplified signal after mixing (dB)

spectrometerMode: Spectrometer Mode (pfb or fft)

pfbParams:

  nTaps: Number of taps used in the PFB
  
  appliedWindow: Applied window function multiplied against the sinc function.
  
fftParams:

  appliedWindow: Applied window function.

## Arduino
active: Active bool for enabling.

comPort: Com-port of the arduino due.

baudRate: Baud rate of the arduino Due

### temperatureMonitoring
active: Enables the temperature Monitoring

nProbes: Number of thermistor probes.

probeLabels: Labels for the thermistors.

unit: Temperature unit.

cadence: Temperature reading cadence (Seconds).

### switches         
 
active: true

optimisedObserving: To be implemented

DickeSwitchCycleLength: Length of each Dicke switch cycle (Seconds)

switchSourceTargets: Ordered list of the primary targets (e.g long_short, antenna,...). Takes the place of source in each Dicke switch cycle

dickeSwitchCycle: List of targets that constitute each Dicke cycle (e.g load, noise_diode source)

switchDictionary: A dictionary designating the label for each source to the switching code passed to the Arduino due (e.g. noise_diode: t1t1e4)

