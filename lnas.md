# Low noise amplifiers

_Low-noise amplifiers in the frontend, plus notes on amplification in the SDRs_

Last updated: 2026-06-21

## Minicircuits ZKL-2+ LNA

There are typically two frontend LNAs, which are SMA-connectorised Minicircuits ZKL-2+ LNAs. These take 12V DC (max. 13 V), with a maximum rated current of 120 mA.

The plot below shows the S-parameters, with a forward gain of approx 33 dB. Full S-parameters, measured with the high-end (but wobbly) VNA in John's lab can be found in the [sparams repo](https://github.com/RHINO-Experiment/rhino-sparams/blob/main/RecBlock/LNA0.s2p).

<img width="50%" alt="S-parameter plot of the ZKL-2+ with the lab VNA"
  src="https://github.com/user-attachments/assets/8252528c-b748-49be-9625-3303bddd5045" />

## Amplifiers in the RSPdx

The RSPdx SDR has multiple amplification stages on board. The gain can be controlled by setting attenuation parameters in the software, rather than changing the LNA gain directly.
